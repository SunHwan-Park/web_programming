# 0428_homework

1. 다음 중 맞으면 T, 틀리면 F 를 작성하고 틀렸다면 이유를 함께 작성하시오

   - Django에서 1:N 관계는 ForeignKeyField 를 사용하고 M:N 관계는 ManyToManyField
     를 사용한다.

     > T

   - ManyToManyield를 설정하고 만들어지는 테이블 이름은 **앱이름\_클래스이름_지정한
     필드** 이름의 형태로 만들어진다.

     > T
     >
     > ```python
     > # accounts/models.py
     > 
     > class User(AbstractUser):
     >     followers = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name="followings")
     > ```
     >
     > - 이 경우 만들어지는 테이블 이름은 `accounts_user_followers`

   - ManyToManyField의 첫번째 인자는 모델 , 두번째 인자는 related_name 이 들어가는
     데 두 가지 모두 필수적으로 들어가야 한다.

     > F / related_name 은 필수 인자가 아니다.

2. 아래 빈 칸에 들어갈 코드를 각각 작성하시오.

   ```python
   class Article(models.Model):
       ...
       user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
       like_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles', blank=True)
   ```

   ```html
   <!-- articles/index.html -->
   
   {% for article in articles %}
   	...
   	<p>{{ article.title }}</p>
   	<a href="{% url 'articles:like' article.pk %}">
   		{% if __(a)__ in __(b)__ %}
           	<i class="fas fa-heart fa-lg" style="color:crimson;"></i>
   		{% else %}
           	<i class="fas fa-heart fa-lg" style="color:black;"></i>
           {% endif %}
   	</a>
   	{{ __(b)__|length }}명이 이 글을 좋아합니다.
   {% endfor %}
   ```

   > (a) : request.user
   >
   > (b) : article.like_users.all

3. 모델 정보가 다음과 같을 때 빈칸에 들어갈 코드를 각각 작성하시오.

   ```python
   # accounts/models.py
   from django.db import models
   from django.conf import settings
   from django.contrib.auth.models import AbstractUser
   
   class User(AbstractUser):
       followers = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='followings')
   ```

   ```python
   # accounts/views.py
   
   from django.contrib.auth import get_user_model
   
   User = get_user_model()
   
   @login_required
   def follow(request, __(a)__):
       person = get_object_or_404(User, username=__(a)__)
       user = request.user
       
       if person.__(b)__.__(c)__(username=__(a)__).exists():
           person.__(b)__.__(d)__(user)
       else:
           person.__(b)__.__(e)__(user)
       return redirect('articles:profile', person.username)
   ```

   > (a) : username
   >
   > (b) : followers
   >
   > (c) : filter
   >
   > (d) : remove
   >
   > (e) : add

4. 아래와 같은 에러 메시지가 발생하는 이유와 이를 해결하기 위한 방법을 작성하시오.

   ![image-20200428175957536](images\image-20200428175957536.png)

   > - `Custom User Model`을 사용하고 있음에도 불구하고, `UserCreationForm`을 사용해 회원가입을 구현하려고 했기 때문에 생긴 에러이다.
   > - `Custom UserCreationForm`을 만들어 회원가입 form으로 사용하면 해당 문제가 해결된다.

5. 아래의 경우  related_name을 필수적으로 설정해야 한다. 그 이유를 설명하시오.

   ```python
   class Article(models.Model):
       ...
       user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
       like_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles', blank=True)
   ```

   > M:N 관계의 related_name을 따로 설정하지 않으면, 기존 1:N 관계(글쓴이 - 글)에서 역참조를 위해 사용했던  `유저.article_set`(default 값)과 같은 값으로 역참조를 하게 되어 혼동이 온다. 따라서 별도의 이름으로 따로 지정해주어야 한다.

6. Person에는 view에서 넘어온 유저 정보가 담겨 있고 모델 정보가 아래와 같을 때, 빈칸에 들어갈 코드를 각각 작성하시오.

   ```python
   # accounts/models.py
   from django.db import models
   from django.conf import settings
   from django.contrib.auth.models import AbstractUser
   
   class User(AbstractUser):
       followers = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='followings')
   ```

   ```html
   <!-- articles/profile.html -->
   
   <h3>작성자: {{ person.username }}</h3>
   <h4>
       팔로잉: {{ __(a)__|length }}
       팔로워: {{ __(b)__|length }}
   </h4>
   <p>
       {% if __(c)__ != __(d)__ %}
       	{% if __(c)__ in __(b)__ %}
       		<a href="{% url 'accounts:follow' __(e)__ %}">Unfollow</a>
       	{% else %}
       		<a href="{% url 'accounts:follow' __(e)__ %}">Follow</a>
       	{% endif %}
       {% endif %}
   </p>
   ```

   > (a) : person.follwings.all
   >
   > (b) : person.followers.all
   >
   > (c) : request.user
   >
   > (d) : person
   >
   > (e) : person.username

