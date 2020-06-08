# 0608_workshop

- `articles/models.py`

  ```python
  from django.db import models
  
  # Create your models here.
  class Article(models.Model):
      title = models.CharField(max_length=50)
      content = models.TextField()
  ```

- `articles/serializers.py`

  ```python
  from rest_framework import serializers
  from .models import Article
  
  class ArticleSerializer(serializers.ModelSerializer):
      class Meta:
          model = Article
          fields = '__all__'
  ```

- `articles/views.py`

  ```python
  from django.shortcuts import render, get_object_or_404
  
  from rest_framework.response import Response
  from rest_framework.decorators import api_view
  
  from .models import Article
  from .serializers import ArticleSerializer
  
  # Create your views here.
  @api_view(['GET', 'POST'])
  def article_list_create(request):
      if request.method == 'POST':
          serializer = ArticleSerializer(data=request.data)
          if serializer.is_valid(raise_exception=True):
              serializer.save()
      else:
          articles = Article.objects.all()
          serializer = ArticleSerializer(articles, many=True)
      return Response(serializer.data)
  
  @api_view(['GET', 'PUT', 'DELETE'])
  def article_detail_update_delete(request, article_pk):
      article = get_object_or_404(Article, pk=article_pk)
      if request.method == 'PUT':
          serializer = ArticleSerializer(data=request.data, instance=article)
          if serializer.is_valid(raise_exception=True):
              serializer.save()
              return Response({"message": "성공적으로 수정되었습니다.", "data": serializer.data})
      elif request.method == 'DELETE':
          article.delete()
          return Response({'message': "성공적으로 삭제되었습니다."})
      else:
          serializer = ArticleSerializer(article)
          return Response(serializer.data)
  ```