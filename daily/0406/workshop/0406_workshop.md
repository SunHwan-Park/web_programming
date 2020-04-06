# 0406_workshop

## 변동 Code

- articles/urls.py

  ```python
  from django.urls import path
  from . import views
  
  app_name = 'articles'
  urlpatterns = [
      path('', views.index, name='index'),
      path('new/', views.new, name='new'),
      path('create/', views.create, name='create'),
      path('<int:pk>/', views.detail, name='detail'),
      path('<int:pk>/edit/', views.edit, name='edit'),
      path('<int:pk>/update/', views.update, name='update'),
      path('<int:pk>/delete/', views.delete, name='delete'),
  ]
  ```

- articles/views.py

  ```python
  from django.shortcuts import render, redirect
  from .models import Article
  
  # Create your views here.
  def index(request):
      articles = Article.objects.all()
      context = {
          'articles': articles
      }
      return render(request, 'articles/index.html', context)
  
  def new(request):
      return render(request, 'articles/new.html')
  
  def create(request):
      article = Article()
      article.title = request.POST.get('title')
      article.content = request.POST.get('content')
      article.save()
      return redirect('articles:detail', article.pk)
  
  def detail(request, pk):
      article = Article.objects.get(id=pk)
      context = {
          'article':article,
      }
      return render(request, 'articles/detail.html', context)
  
  def edit(request, pk):
      article = Article.objects.get(id=pk)
      context = {
          'article':article,
      }
      return render(request, 'articles/edit.html', context)
  
  def update(request, pk):
      article = Article.objects.get(id=pk)
      article.title = request.POST.get('title')
      article.content = request.POST.get('content')
      article.save()
      return redirect('articles:detail', article.pk)
  
  def delete(request, pk):
      article = Article.objects.get(id=pk)
      article.delete()
      return redirect('articles:index')
  ```

- articles/templates/articles/index.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
  <h1>INDEX</h1>
  <a href="{% url 'articles:new' %}">NEW</a>
  {% for article in articles %}
      <h3>제목: {{ article.title }}</h3>
      <p>내용: {{ article.content }}</p>
      <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
      <hr>
  {% empty %}
      <p>게시물이 없습니다.</p>
  {% endfor %}
  {% endblock %}
  ```

- articles/templates/articles/new.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
  <h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="POST">
      {% csrf_token %}
      TITLE: <input type="text" name="title">
      <br>
      CONTENT: <textarea cols='40' rows='10' name="content"></textarea>
      <br>
      <input type="submit" value="작성">
  </form>
  <a href="{% url 'articles:index' %}/">BACK</a>
  {% endblock %}
  ```

- articles/templates/articles/detail.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
      <h1>DETAIL</h1>
      <hr>
      <h3>{{ article.title }}</h3>
      <p>{{ article.content }}</p>
      <p>작성일: {{ article.created_at }}</p>
      <p>수정일: {{ article.updated_at }}</p>
      <a href="{% url 'articles:edit' article.pk %}">EDIT</a>
      <a href="{% url 'articles:delete' article.pk %}">DELETE</a>
      <br>
      <a href="/articles/">BACK</a>
  {% endblock %}
  ```

- articles/templates/articles/edit.html

  ```html
  {% extends 'base.html' %}
  
  {% block content %}
  <h1>EDIT</h1>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
      {% csrf_token %}
      TITLE: <input type="text" name="title" value="{{ article.title }}">
      <br>
      CONTENT: <textarea cols='40' rows='10' name="content">{{ article.content }}</textarea>
      <br>
      <input type="submit" value="수정">
  </form>
  <a href="{% url 'articles:detail' article.pk %}">BACK</a>
  {% endblock %}
  ```