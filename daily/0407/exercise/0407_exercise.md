# 0407_exercise

## 결과 사진

- Read

  <img src="images/read.png">

- Create

  <img src="images/create.png">

- Detail

  <img src="images/detail.png">

## Code

- views.py

  ```python
  from django.shortcuts import render, redirect, get_object_or_404
  from .models import Article
  from .forms import ArticleForm
  
  # Create your views here.
  def index(request):
      articles = Article.objects.order_by('pk')
      context = {
          'articles':articles,
      }
      return render(request, 'articles/index.html', context)
  
  def create(request):
      if request.method == 'POST':
          form = ArticleForm(request.POST)
  
          if form.is_valid():
              article = form.save()
              return redirect('articles:index')
      else:
          form = ArticleForm()
  
      context = {
          'form':form,
      }
      return render(request, 'articles/create.html', context)
  
  def detail(request, pk):
      article = get_object_or_404(Article, pk=pk)
      context = {
          'article':article,
      }
      return render(request, 'articles/detail.html', context)
  ```

- forms.py

  ```python
  from django import forms
  from .models import Article
  
  class ArticleForm(forms.ModelForm):
      class Meta:
          model = Article
          fields = ['title', 'content']
  ```