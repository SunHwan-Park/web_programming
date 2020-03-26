# 0326_homework

```bash
homework/
	articles/
		admin.py
		apps.py
		migrations/
		models.py/
		tests.py
		views.py
    manage.py
    myproject/
    	settings.py
    	urls.py
    	wsgi.py
```

##### 위와 같은 폴더와 파일구조가 있다고 할 때 다음 문제들에 해당하는 CLI 명령어를 작성하시오.(단, Ubuntu의 shell bash에서 진행한다고 가정한다.)

1. 현재 내가 작업중인 위치를 확인해야 하는데 이를 위한 명령어를 작성하시오.

   > ```bash
   > $ pwd
   > ```

2. 현재 내 위치가 homework 디렉토리에 있다는 것이 확인 되었다. myproject 디렉토리의 urls.py에 접근하기 위해 myproject로 이동하기 위한 명령어를 작성하시오.

   > ```bash
   > $ cd myproject/
   > ```

3. 현재 디렉토리에 있는 파일 및 폴더 목록을 확인하고 싶다. 이를 위한 명령어를 작성하시오.

   > ```bash
   > $ ls
   > ```

4. 이미지들을 모아두기 위한 images 라는 이름의 디렉토리를 만들어야 한다. 이를 만들기 위한 명령어를 작성하시오.

   > ```bash
   > $ mkdir images
   > ```

5. 현재 위치(myproject)에서 articles 폴더에 component.py 파일을 만들어야 한다. 이를 위한 명령어를 작성하시오.

   > ```bash
   > $ mkdir articles
   > $ cd articles/
   > $ touch component.py
   > ```

---

##### 다음은 django 에 관한 문제이다. 올바른 답을 작성하시오.

1. django 서버를 실행하고 첫 페이지에 접속했을 때 터미널에 출력된 서버 시간이 현재 우리 대한민국의 시간과 다른 시간으로 출력된다. 이를 한국 시간으로 바꾸려면 settings.py의 어떤 변수에 어떤 값을 할당해야 하는지 작성하시오.

   > `TIME_ZONE` 변수에 `UTC` 대신 `Asia/Seoul`를  할당한다.

2. 다음은 어떤 django 프로젝트의 urls.py의 모습이다. 주소 '/ssafy'로 요청이 들어왔을 때 실행되는 함수가 pages 앱의 views.py 파일 안 ssafy 함수라면, 요청에 응답하기 위해 빈칸 (a)에 추가되어야 할 코드를 작성하시오.

   ```python
   from django.contrib import admin
   from django.urls import path
   from pages import views
   
   urlpatterns = [
       path(    (a)    ),
       path('admin/', admin.site.urls),
   ]
   ```

   > `'ssafy/', views.ssafy`