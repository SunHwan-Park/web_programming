# 0331_exercise

### 결과 사진

- ping

  <img src="images/ping.png">

- pong

  <img src="images/pong.png">

### Code

- views.py

  ```python
  from django.shortcuts import render
  
  # Create your views here.
  def ping(request):
      return render(request, 'ping.html')
  
  def pong(request):
      ping = request.GET.get('ping')
      context = {'ping':ping}
      return render(request, 'pong.html', context)
  ```

- crud/urls.py

  ```python
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('articles/', include('articles.urls')),
  ]
  ```

- articles/urls.py

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns = [
      path('ping/', views.ping),
      path('pong/', views.pong),
  ]
  ```

- base.html

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>crud</title>
  </head>
  <body>
      {% block content %}
      {% endblock %}
  </body>
  </html>
  ```

- ping.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
  <h1>여기는 ping</h1>
  <h2>pong으로 데이터를 보내보자!</h2>
  <form action="/articles/pong/">
      <input type="text" name="ping">
      <input type="submit">
  </form>
  {% endblock %}
  ```

- pong.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
  <h1>여기는 pong</h1>
  <h2>ping에서 {{ ping }}를 받았어!</h2>
  {% endblock %}
  ```