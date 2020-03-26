# 0326_workshop

<img src="images/lotto numbers.png" alt="lotto numbers"/>

1. intro/urls.py

   ```python
   from django.contrib import admin
   from django.urls import path
   from pages import views
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       path('lotto/', views.lotto),
   ]
   ```

2. pages/views.py

   ```python
   from django.shortcuts import render
   def lotto(request):
       import random
       pick = sorted(random.sample(range(1, 46), 6))
       context = {'pick': pick}
       return render(request, 'lotto.html', context)
   ```

3. templates/lotto.html

   ```html
   <!DOCTYPE html>
   <html lang="ko">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <meta http-equiv="X-UA-Compatible" content="ie=edge">
       <title>Lotto numbers</title>
   </head>
   <body>
       <h1>
           제 1회 로또 번호 추천
       </h1>
       <p>
           SSAFY님께서 선택하신 로또 번호는 {{ pick }}입니다.
       </p>
   </body>
   </html>
   ```

