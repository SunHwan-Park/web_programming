# Web Programming_django basic

## django

> The Web framework for perfectionists with deadlines

- web framework based on python

  - 웹 페이지를 개발하는 과정에서 겪는 어려움을 줄이는 것이 주 목적
  - cf ) `flask`는 경량화된 웹 프레임워크

- 웹 개발을 하는 것 == 카페를 만드는 것

  1. A - Z 모두 직접 하기(URL Parsing, DB setting...)
  2. 프랜차이즈 창업(프레임워크 사용)

- 수많은 서비스들이 사용하는 프레임워크

  - Spotify
  - Instagram
  - Dropbox
  - Delivery Hero

- django는 서버에서 클라이언트에 HTML 응답을 보내주기 위한 프레임워크

- 모델-뷰-컨트롤러(MVC): 소프트웨어 디자인 패턴

  | MVC pattern | MTV pattern(django)        |
  | ----------- | -------------------------- |
  | Model       | Model(데이터 관리)         |
  | View        | Template(인터페이스(화면)) |
  | Controller  | View(중간 관리(상호 동작)) |

  ![django_MTV_pattern](images\django_MTV_pattern.png)

## Start django

### 설치

```bash
$ pip install django==2.1.15
```

### django 프로젝트 시작

#### 프로젝트 생성

```bash
$ django-admin startproject {프로젝트명}
```

#### Project Folder

- 전체 프로젝트 폴더 아래에 이름이 같은 폴더가 하나 생기는 데 이것을 'Project Folder'라고 지칭한다.
- init.py
  - 현 프로젝트가 하나의 pagkage 폴더이고, 그 안에 있는 init.py라고 생각하면 됨.
  - 지우거나 그냥 수정하면 X
- setting.py
  - DEBUG: 개발모드, `TRUE` 일때 오류 사항을 웹페이지에서 바로 확인할 수 있다.(default: `TRUE`)
  - **ALLOWED_HOSTS**: 호스트 승인
    - '*' : All
  - **INSTALLED_APPS**: 생성한 앱 등재(주민등록)
  - TEMPLATES
  - DATABASES
  - AUTH_PASSWORD
  - LANGUAGE_CODE: 서버언어 설정
    - 한글로 설정하려면 `'ko-kr'`
  - TIME_ZONE: 서버시간 설정
    - 우리나라 시간으로 설정하려면 `'Asia/Seoul'`
  - USE_I18N: 국제화
  - USE_L10N: 지역화
  - USE_TZ: 타임존
- urls.py: 요청 url 설정
- wsgi.py: Web Server Gateway Interface. 배포 작업할 때 활용. 서버실행

* `django_intro` 폴더의 `settings.py` 파일에 아래와 같이 수정한다.

  ```python
  # 28번째 라인
  ALLOWED_HOSTS = ['*']
  # 혹은
  ALLOWED_HOSTS = ['장고 오류페이지에서 나오는 host 주소(You may need to add)']
  ```

* 반드시 서버 실행시 명령어가 실행되는 디렉토리를 확인할 것.

```bash
~/ $ cd django_intro/
~/django_intro/ $ python manage.py runserver 8080
# manage.py: 명령어 핸들링 하는 파일
```

* 실행된 서버는 우측의 영역의 url을 클릭한다.

  ![django_server_url](images\django_server_url.png)

* 서버 종료는 터미널에서 `ctrl + c` 함께 입력한다.

#### App 생성

* django는 **여러 개의 앱을 가진 하나의 프로젝트**로 구성된다.
  * 일반적으로 하나의 앱 안에 하나의 기능을 부여
  * 커뮤니티를 만든다.
    * 회원과 관련된 app - `accounts`
    * 게시글과 관련된 app -`posts`
  * App을 제거 하고 싶은 경우, 해당 App 폴더를 삭제하거나, `INSTALLED_APPS`에서 등록 해제하면 된다.
  * App 하나가 하나의 package랑 비슷한 것!
    * `from pages import views`

```bash
$ python manage.py startapp {app이름}
```

* app을 생성하고 반드시 `settings.py` 의 `INSTALLED_APPS` 에 등록한다.

  ```python
  INSTALLED_APPS = [
      ...
      'pages',
  ]
  ```

### 기본 흐름

#### 1. `urls.py`: 요청

```python
# django_intro/urls.py
from pages import views

urlpatterns = [
    path('lotto/', views.lotto),
]
```

* path에 url은 항상 `/` 로 닫아준다.(django의 특징)
* urls.py는 문지기
  - 어떤 요청 들어오면, 어디로 보내!

#### 2. `views.py`: 연결

```python
# pages/views.py
import random

def lotto(request):
    pick = random.sample(range(1, 46), 6)
    context = {
        'pick': pick
    }
    return render(request, 'lotto.html', context)
```

* 함수를 정의할 때, 항상 첫번째 인자는 `request`로 작성해둔다.

  * 내부적으로 요청을 처리할 때, 함수 호출 시 요청 정보가 담긴 객체를 넣어준다.

* `render` 함수를 통해서 반환한다.

  * 첫번째 인자 : `request`
  * 두번째 인자 : 템플릿 파일(`html`)
  * 세번째 인자 : dictionary, 템플릿에서 활용을 하려고 하는 값들을 전달

* `views.py` 에 `import` 는 사실 어느 위치에 넣어도 상관은 없음

  왜냐, 어차피 로드되는 순간 한 번씩 다 실행함

  함수 호출 권한은 django 서버에 있음

#### 3. `template` 파일 생성: 반환

* 반환할 `html` 파일은 항상 `templates`  폴더 안에 생성한다.

```html
<!-- pages/templates/lotto.html -->
<p>{{ pick }} </p>
```

* context 딕셔너리의 key 값을 적으면 출력된다.

## URL 설정

### Variable routing

> url의 특정 위치의 값을 변수로 활용

#### 1. urls.py

```python
# django_intro/urls.py
path('hi/<str:name>/', views.hi),
path('add/<int:a>/<int:b>/', views.add),
```

#### 2. views.py

```python
# pages/views.py
def hi(request, name):
    context = {
        'name': name
    }
    return render(request, 'hi.html', context)
```

#### 3. template

```html
<!-- pages/templates/hi.html-->
<h1>
    안녕, {{name}}
</h1>
```

## Template

### DTL

> 템플릿파일(html)은 django template language를 통해 구성된다.

#### 기본문법

1. 출력 `{{ }}`

   ```html
   {{ menu }}
   {{ menu.0 }}
   ```

2. 문법 `{% %}`

   ```html
   {% for menu in menupan %}
   
   {% endfor %}
   ```

3. 주석 `{# #}`

   ```html
   {# 주석입니다. #}
   ```

#### 반복문

```html
{% for reply in replies %}
	<li>{{ reply }}</li>
{% endfor %}
```

* `{{ forloop.counter }}`
* `{{ forloop.counter0 }}`
* `{% empty %}`

#### 조건문

```html
{% if user == 'admin' %}
	<p>관리자 입니다.</p>
{% else %}
	<p>권한이 없습니다.</p>
{% endif %}
```

#### built-in tag, filter

* [공식문서](https://docs.djangoproject.com/en/3.0/ref/templates/builtins/)

```html
{{ content|length }}
{{ content|truncatechars:10 }}
```

### Template 확장

```html
 <!-- pages/templates/base.html -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Django 기초 - pages</title>
    {% block css %}
    {% endblock %}
</head>
<body>
    <h1>Django 기초 문법 학습</h1>
    {% block body %}
    {% endblock %}
</body>
</html>
```

```html
{% extends 'base.html' %}

{% block css %}
<style>
    h1 {
        color: blue;
    }
</style>
{% endblock %}

{% block body %}
	<h1>페이지</h1>
{% endblock %}
```

### Template 설정

```python
# django_intro/settings.py Line#55
TEMPLATES = [
    {
        # DTL 엔진을 활용. jinja2 등으로 변경 가능함.
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        # APP 내에 있는 폴더가 아닌 추가적으로 템플릿으로 활용하고 싶은 경로.
        'DIRS': [
            os.path.join(BASE_DIR, 'django_intro', 'templates')
        ],
        # APP_DIRS: True 인경우, 등록된 app(INSTALLED_APPS)의 디렉토리에 있는 templates 폴더를 템플릿 폴더로 활용하겠다.
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

* `DIRS` 리스트에 경로 정의는 폴더 구조를 통해 확인하자.

  ```
  00_django_intro/ <- BASE_DIR
  	django_intro/
  		templates/
  ```

## Multiple app을 위한 설정

> 앞으로는 항상 app을 생성하면 다음과 같은 폴더 구조를 가진다.

```
app1/
	templates/
		app1/
			index.html
			a.thml
    urls.py
    views.py
    ...

app2/
	templates/
		app2/
			index.html
			b.thml
    urls.py
    views.py
    ...
```

### 1. url 설정 분리

> 각각의 app 별로 url을 관리한다.

* 프로젝트 폴더 urls.py 정의

  ```python
  # django_intro/urls.py
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('pages/', include('pages.urls')),
      path('boards/', include('boards.urls')),
  ]
  ```

* 각 프로젝트별 urls.py  정의

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns = [
      # /boards/
      path('', views.index),
      # /boards/new/
      path('new/', views.new),
      # /boards/complete/
      path('complete/', views.complete),
  ]
  ```

### 2.  templates 폴더 구조

* template 파일을 반환하기 위해서 django는 아래의 폴더들을 탐색한다.
  * `DIRS` 에 정의된 경로의 하위 디렉토리
  * `INSTALLED_APPS` 디렉토리의 `templates` 폴더의 하위 디렉토리 탐색
* 이 과정에서 중복된 파일이 있는 경우, 예상치 못한 결과가 나타날 수 있다.
* 따라서, 앞으로 다음과 같은 구조를 유지한다.

```
app1/
	templates/
		app1/
app2/
	templates/
		app2/
```

## Form을 통한 요청 처리

### 개요

1. 사용자들로부터 값을 받아서 (`boards/new/`)
2. 이를 단순 출력하는 페이지 구성 (`boards/complete/`)

### 1. 사용자에게 form 양식 제공

1. url 지정

   ```python
   # boards/urls.py
   path('new/', views.new),
   ```

2. view 함수 생성

   ```python
   # boards/views.py
   def new(request):
       return render(request, 'boards/new.html')
   ```

3. template

   ```html
   <!-- boards/templates/boards/new.html -->
   <form action="/boards/complete/">
       제목 : <input type="text" name="title">
   </form>
   ```

   * form 태그에는 `action` 속성을 정의한다.
     * 사용자로부터 내용을 받아서 처리하는 url
   * input 태그에는 `name` 속성을 통해 사용자가 입력한 내용을 담을 변수 이름을 지정한다.
   * url 예시 :  `/boards/complete/?title=제목제목`

### 2. 사용자 요청 처리

1. urls.py 정의

   ```python
   # boards/urls.py
   path('complete/', views.complete)
   ```

2. views.py

   ```python
   # boards/views.py
   def complete(request):
       title = request.GET.get('title')
       context = {
   		'title': title
       }
       return render(request, 'boards/complete.html', context)
   ```

   * `request` 에는 요청과 관련된 정보들이 담긴 객체가 저장되어 있다.

3. template

   ```html
   <!-- boards/templates/boards/complete.html -->
   {{ title }}
   ```

### 3. form 양식에 빈 내용을 입력하지 못하게 하는 방법

1. `input` 태그에 `required` 요소 먹이기

   ```html
   <input type="number" id="rank" name="rank" placeholder="1부터 5까지의 숫자를 입력하세요." required>
   ```

2. model 클래스 생성시 `blank=False` 설정하기

   ```python
   content = models.TextField(blank=False)
   ```

   - blank: 주어진 입력창이 비어있는 상태여도 되는 지 안되는 지를 정의(App 레벨)

     - True: 빈 내용 가능 / Fasle: 빈 내용 불가능(default)

   - null: 주어진 데이터베이스 컬럼이 null 값을 가질 것인지 아닌 지를 정의(DB 레벨)

     - True: null 가능 / False: null 불가능(default)

     - CharField, TextField와 같은 문자열 기반 필드에 `null=True` 정의하지 말 것.

       - "데이터 없음"에 대해 두 가지 값(None / "")을 중복해 갖게 됨. 

       - 빈 문자열("") 값을 사용하는 것이 컨벤션!

       - 만약 문자열 기반 모델 필드를 "nullable" 하게 만들고 싶다면 다음과 같이 설정할 수 있다.

         ```python
         class Person(models.Model):
           name = models.CharField(max_length=255)  # 필수
           bio = models.TextField(max_length=500, blank=True)  # 선택 (null=True를 넣지 말자)
           birth_date = models.DateField(null=True, blank=True)  # 선택 (여기서는 null=True를 넣을 수 있다.)
         ```

## ETC

### PORT

- 포트는 내마음대로
  - 약속된 포트 번호들만 쓰지 않으면 된다.
    - SMTP / FTP
  - echo $PORT
    - echo $IP
      - 127.0.0.1
      - localhost의 주소
  - 8080 PORT는 c-9의 규칙이다..?
- 도커 쓰면 좋은 점(linux 가상환경)
  - 개발환경과 배포 환경을 일치시킬 수 있다.
  - 개발자들 간의 개발환경을 일치시킬 수 있다.

### Fat Model, Thin Controller

- django에서 제안하는 비즈니스 로직 관리 방식은 가능한 Model 파트에 기능을 추가하는 것이다. 즉, 비즈니스 로직 코드를 모델에 넣어서 캡슐화 하는 것!
- MVC(MTV)의 기본 설계 패턴은 Fat Model, Thin Controller(View)이다. 가능한 Model에 기능을 모아두고, Controller(View)는 중개역할만 하게 하는 것!
- 이 경우, 코드의 중복이 줄어들고, 객체지향적 코드를 설계하기 용이하다는 장점이 있다. 이는 결국 프로젝트 전체에서 코드의 재사용을 개선할 수 있게 한다.
- 그러나 모델에 비즈니스 로직이 많아지고, 다양한 도메인이 섞이게 되면,  시스템 규모가 커질수록 관리가 어려워진다. 이는 [Django Proxy Model](https://www.benlopatin.com/using-django-proxy-models/)을 활용해 일정부분 해결할 수 있다.
- 한 App에서 Model이 너무 많아지면 각 모델을 서로 다른 App으로 분리하는 것이 방법이 될 수 있다.
- 참고 문서 - [Where to Put Business Logic in Django](https://sunscrapers.com/blog/where-to-put-business-logic-django/)