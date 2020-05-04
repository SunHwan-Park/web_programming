# 0504_homework

1. Django 는 MTV로 이루어진 Web Framework다. MTV가 무엇의 약자이며 Django에서 각각 어떤 역할을 하고 있는지 작성하시오.

   > - M: Model. 데이터 관리
   > - T: Template. 인터페이스(화면) 관리
   > - V: View. 중간 관리(상호 동작)

2. 기본적으로 ‘/ ’ 페이지에 접속하게 되면 아래 사진처럼 Page not found 에러가 발생한다. ‘/ ’ 페이지에 접속했을 때 index.html 를 렌더링 하고자 한다. 아래 빈칸에 알맞은 코드를 작성하시오. (프로젝트의 이름은 crud이며 app이름은 articles이다. index.html 파일을 렌더링 하는 함수의 이름은 index 라고 가정한다.)
   ![image-20200504182307891](C:\Users\PARK SUNHWAN\online-lecture\0504\homework\images\image-20200504182307891.png)

   ```python
   from django.contrib import admin
   from django.urls import path, include
   from __(a)__ import __(b)__
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('articles/', include('articles.urls')),
       path('', __(c)__)
   ]
   ```

   > - (a) : articles
   > - (b) : views
   > - (c) : views.index

3. Django 프로젝트는 기본적으로 render할 html과 같은 template 파일과 css , js와 같은 static 파일을 앱 폴더 내부의 templates와 static 이름의 폴더에서 찾는다. 만약 해당 위치가 아닌 임의의 위치에 파일을 위치 시키고 싶으면 \_\_(a)\_\_ 파일의 \_\_(b)\_\_과 \_\_(c)\_\_이라는 변수에 담긴 리스트의 요소를 수정하면 된다. 빈칸 (a), (b), (c)에 들어갈 내용을 작성하시오.

   > - (a) : settings.py
   > - (b) : TEMPLATES_DIRS(TEMPLATES - 'DIRS')
   > - (c) : STATICFILES_DIRS

4. 아래는 그림과 같이 Django에서 선언한 Model을 Database에 반영하는 과정에서 사용하는 명령어에 대한 설명이다. 각 설명에 해당하는 명령어를 작성하시오.

   ```PYTHON
   class Post(models.Model):
       title = models.CharField(max_length=100)
       content = models.TextField()
       created_at = models.DateTimeField(auto_now_add=True)
       updated_at = models.DateTimeField(auto_add=True)
   ```

   - 마이그레이션 생성

     > `python manage.py makemigrations`

   - 마이그레이션 DB 반영 여부 확인

     > `python manage.py showmigrations`

   - 마이그레이션에 대응되는 SQL 문 출력

     > `python manage.py sqlmigrate 해당 migration`

   - 마이그레이션 파일의 내용을 DB 에 최종 반영

     > `python manage.py migrate`

5. 아래의 설명을 읽고 T/F 여부를 작성하시오

   - POST 와 GET 방식은 의미론상의 차이이며 실제 동작 방식은 동일하다.

     > False

   - ModelForm과 Form Class의 핵심 차이는 Model의 정보를 알고 있는 지의 여부이다.

     > True

   - AuthenticationForm은 User 모델과 관련된 정보를 이미 알고 있는 ModelForm으로 구성되어 있다.

     > False

   - ModelForm을 사용할 때 Meta 클래스에 fields 관련 옵션은 반드시 작성해야 한다.

     > True

6. 사용자가 업로드한 파일이 저장되는 위치를 Django 프로젝트 폴더(crud) 내부의 /uploaded_files 로 지정하고자 한다. 이 때, settings.py에 작성해야 하는 설정 2가지를 작성하시오.

   > - MEDIA_URL
   >
   >   ```python
   >   MEDIA_URL = '/uploaded_files/'
   >   ```
   >
   > - MEDIA_ROOT
   >
   >   ```python
   >   MEDIA_ROOT = os.path.join(BASE_DIR, 'uploaded_files')
   >   ```

7. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - RDBMS를 조작하기 위해서 SQL문을 사용한다.

     > True

   - SQL에서 명령어는 반드시 대문자 작성해야 동작한다.

     > False

   - 일반적인 SQL문에서는 세미콜론 ( ; ) 까지를 하나의 명령어로 간주한다.

     > True

   - SQLite에서 .tables, .headers on 과 같은 dot( . ) 로 시작하는 명령어는 SQL 문이 아니다.

     > True

   - 하나의 데이터베이스 안에는 반드시 한 개의 테이블만 존재해야 한다.

     > False

8. 게시글과 댓글의 관계에서 댓글이 존재하는 게시글은 삭제할 수 없도록 \__(a)__에 들어갈 코드를 작성하시오. 그리고 이러한 설정이 되어있는 상황에서 Article 객체를 삭제하려고 할 때 발생하는 오류를 작성하시오.

   ```python
   class Article(models.Model):
       title = models.CharField(max_length=100)
       content = models.TextField()
       
   class Comment(models.Model):
       content = models.TextField()
       article = models.ForeignKey(Article, on_delete=models.__(a)__)
   ```

   > - (a) : PROTECT
   > - 발생하는 에러 : ProtectedError

9. Board 모델과 User 모델을 M:N 관계로 설정하여 '좋아요' 기능을 구현하려고 한다. \_\_(a)\_\_와 \_\_(b)\_\_에 들어갈 내용을 작성하시오. 추가적으로 아래의 상황에서 __(b)__를 반드시 작성 해야 하는 이유를 함께 작성하시오.

   ```python
   from django.conf import settings
   
   class Board(models.Model):
       content = models.CharField(max_length=100)
       user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
       like_users = models.__(a)__(settings.AUTH_USER_MODEL, __(b)__='like_boards', blank=True)
   ```

   > - (a) : ManyToManyField
   > - (b) : related_name
   > - M:N 관계에서의 역참조를 진행할 때, 1:N 관계에서의 User -> Board 역참조시 사용하는 `user.board_set`과 코드가 겹치기 때문에 별도의 `related_name`을 반드시 작성해준다.

10. follow 기능을 구현하기 위해 accounts app의 models.py에 아래와 같은 모델을 작성하였다.  Migration 작업 이후에 Database에 만들어지는 테이블의 이름을 작성하고 follow와 관련된 모델의 필드 이름을 각각 작성하시오.

    ```python
    from django.db import models
    from django.conf import settings
    from django.contrib.auth.models import AbstractUser
    
    class User(AbstractUser):
        followers = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='followings')
    ```

    > - 만들어지는 테이블 이름
    >   - `accounts_user`
    >   - `accounts_user_followers`
    >   - `accounts_user_groups`
    >   - `accounts_user_user_permissions`
    > - `accounts_user_followers` 테이블의 필드
    >   - id
    >   - from_user_id
    >   - to_user_id