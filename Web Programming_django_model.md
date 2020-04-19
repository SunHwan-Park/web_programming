# Web Programming_django model

## Model 활용

### 1. model 정의

```python
# django_crud/articles/models.py
class Article(models.Model):
    title = models.CharField(max_length=140)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

* `models.Model` 을 상속받은 클래스를 생성한다.
* 속성은 내가 구성하고 싶은 테이블의 컬럼의 이름을 지정하고, 데이터 타입에 맞춰서 필드를 정의한다.
* `id` 필드는 자동적으로 `pk` 값으로 생성된다.
* 위에서 정의된 필드와 옵션 정보는 다음과 같다.
  * `CharField` :
    * 비교적 짧은 텍스트 받고 싶을 때 사용
    * `max_length` : 필수
  * `TextField`: textarea 만들고 싶을 때 사용
  * `DateTimeField`
    * `auto_now_add` : (선택) 생성시에만 자동으로 해당 시간 값 설정
    * `auto_now` : (선택) 수정시마다 자동으로 해당 시간 값 설정
  * 이외의 필드는 https://docs.djangoproject.com/ko/2.1/ref/models/fields/#field-types 링크에서 확인

### 2. 마이그레이션

> Migrations are Django’s way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema.
>
> 마이그레이션은 django에서 모델의 변경 사항을 **데이터베이스 스키마에 반영**하기 위한 방법이다.
>
> [관련 문서](https://docs.djangoproject.com/en/2.1/topics/migrations/)

* 정의된 모델을 데이터베이스에 반영하기 위해서는 마이그레이션 명령어를 통해 마이그레이션 파일을 생성한다.

  ```bash
  $ python manage.py makemigrations
  Migrations for 'articles':
    articles/migrations/0001_initial.py
      - Create model Article
  ```

* 마이그레이션 파일은 모델의 변경사항은 기록하며, app 별로 있는 `migrations/` 폴더에 기록된다. 최초에 `0001_initial.py` 라는 파일이 생성되어 있을 것이다.

* 생성된 마이그레이션 파일을 데이터베이스에 반영하기 위해서는 아래의 명령어를 입력한다.

  * 아래와 같이 많아 보이는 것은 django가 기본적으로 활용하고 있는 데이터베이스 마이그레이션 파일까지 반영되었기 때문이다. (앞으로는 프로젝트 생성과 동시에 `python manage.py migrate` 를 하자.)

  ```bash
  $ python manage.py migrate
  Operations to perform:
    Apply all migrations: admin, articles, auth, contenttypes, sessions
  Running migrations:
    Applying contenttypes.0001_initial... OK
    Applying auth.0001_initial... OK
    Applying admin.0001_initial... OK
    Applying admin.0002_logentry_remove_auto_add... OK
    Applying admin.0003_logentry_add_action_flag_choices... OK
    Applying articles.0001_initial... OK
    Applying contenttypes.0002_remove_content_type_name... OK
    Applying auth.0002_alter_permission_name_max_length... OK
    Applying auth.0003_alter_user_email_max_length... OK
    Applying auth.0004_alter_user_username_opts... OK
    Applying auth.0005_alter_user_last_login_null... OK
    Applying auth.0006_require_contenttypes_0002... OK
    Applying auth.0007_alter_validators_add_error_messages... OK
    Applying auth.0008_alter_user_username_max_length... OK
    Applying auth.0009_alter_user_last_name_max_length... OK
    Applying sessions.0001_initial... OK
  ```

* 데이터베이스에는 다음과 같은 테이블이 생성되어 있을 것이다.

  ![django_CRUD_1](images/django_CRUD_1.png)

* 정말이다!

  ![django_CRUD_2](images/django_CRUD_2.png)

* 마이그레이션 관련 명령어들은 다음과 같다.

  ```bash
  $ python manage.py makemigrations # 일종의 설계도를 생성
  $ python manage.py showmigrations # migrations 확인
  $ python manage.py migrate # 데이터베이스 스키마에 설계한 migration 반영
  $ python manage.py sqlmigrate article 0001 # 해당 migration의 sql 문을 확인
  ```

  * `migrate` 나 `makemigrations` 명령어도 특정 app의 마이그레이션만 반영하도록 할 수 있다. 
  
* 데이터 스키마가 변경될 때는, 즉 규정한 Model에 변동사항이 있을 경우, 새롭게 `makemigrations`와 `migrate`를 해줘야한다. 단, `method`가 변동될 경우에는 별도 처리가 필요없다.

### 추가) admin 등록

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article
admin.site.register(Article)
```

## Django ORM

> 기본적인 데이터베이스 조작을 CRUD(Create, Read, Update, Delete) operation 이라고 한다.

### ORM

- Object Relation Mapper(객체 관계 조작)
- python DB 메서드 호출

- 원래 DB에 접근하기 위해 SQL문을 사용해야하는데, 그것을 단순화/경량화 해서 python code를 활용해 바로 접근할 수 있게 한 것이 ORM
- 일종의 python code와 서버 간 중간자 역할
- 많은 장점이 있다.
  - 자동 최적화
  - DB 갈아끼우기가 용이하다.(호환시킬 DB만 알려주면 됨)

### 0. django shell

>  python interactive interpreter를 django 프로젝트에 맞게 쓸 수 있는 기능

```bash
$ python manage.py shell
```

* 추가적인 패키지 설치를 통해 편하게 활용할 수 있다.

  ```bash
  $ pip install django-extensions ipython
  ```

  * `django-extensions` 는 django 개발에 있어서 유용한 기능들을 기본적으로 제공한다.
    * https://github.com/django-extensions/django-extensions
  * `ipython` 은 인터렉티브 쉘을 조금 더 편하게 활용하기 위해서 설치.

* 설치 이후에, `settings.py` 에 다음의 내용을 추가한다. (콤마 유의)

  ```python
  # django_crud/settings.py
  INSTALLED_APPS = [
      ...
      'django_extensions',
      'articles',
  ]
  ```

* 그리고 이제부터는 아래의 명령어를 사용한다.

  ```bash
  $ python manage.py shell_plus
  ```

* 쉘 종료 명령어는 `ctrl+d` 이다.

### 1. 생성

```python
article = Article()
article.title = '제목'
article.content = '내용'
article.save()
```

* 생성을 위해서는 아래와 같이도 할 수 있다.

```python
Article.objects.create(title='제목', content='내용')
```

```python
article = Article(title='제목', content='내용')
article.save()
```

### 2. 조회

* 전체 데이터 조회

    ```python
    Article.objects.all()
    >> <QuerySet [<Article: Article object (1)>]>
    ```

* 단일 데이터 조회

  > 단일 데이터 조회는 고유한 값인 id 혹은 pk를 통해 가능하다.

  ```bash
  Article.objects.get(id=1)
  >> <Article: Article object (1)>
  ```

### 3. 수정

```python
a1 = Article.objects.get(id=1)
a1.title = '제목 수정'
a1.save()
```

* 수정이 되었는지  확인하기 위해서 데이터 조회를 다시 해보자.

### 4. 삭제

```python
a1 = Article.objects.get(id=1)
a1.delete()
>> (1, {'articles.Article': 1})
```

## Admin 페이지 활용

### 1. 관리자 계정 생성

```bash
$ python manage.py createsuperuser
사용자 이름 (leave blank to use 'ubuntu'): admin1
이메일 주소:
Password:
Password (again):
Superuser created successfully.
```

### 2. admin 등록

> admin 페이지를 활용하기 위해서는 app 별로 있는 admin.py에 정의 되어야 한다.
>
> 필요한 경우 admin page의 구조와 디자인을 변경할 수 있다.

```python
# django_crud/articles/admin.py
from django.contrib import admin

# Register your models here.
from .models import Article

class ArticleAdmin(admin.ModelAdmin):
    # 메뉴에서 보일 attribute 설정
    list_display = ('pk', 'title', 'content', 'rank')
    
admin.site.register(Article, ArticleAdmin)
```

### 3. 확인

* `/admin/` url로 접속하여, 관리자 계정으로 로그인
