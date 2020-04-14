# 0414_homework

### 아래 코드들을 참고하여 각 문항에 답하시오.

1. django 에서 기본적으로 사용하는 User 모델은 AbstractUser 모델을 상속받아 정의된다.

   ```python
   class User(AbstractUser):
       class Meta(AbstractUser.Meta):
           swappable = 'AUTH_USER_MODEL'
   ```

   아래의 models.py 를 참고하여 User 모델에서 사용할 수 있는 칼럼 중 BooleanField 로
   정의 된 칼럼을 모두 작성하시오.
   https://github.com/django/django/blob/master/django/contrib/auth/models.py

   >**강조 표시** 된 것이 **BooleanField**
   >
   >주요 모델 필드
   >
   >- username - CharField
   >- first_name - CharField
   >- last_name - CharField
   >- email - EmailField
   >- **is_staff** - BooleanField
   >- **is_active** - BooleanField
   >- date_joined - DateTimeField
   >- password - CharField
   >- last_login - DateTimeField
   >- **is_superuser** - BooleanField

2. django 에서 기본적으로 사용하는 User 모델의 사용할 수 있는 칼럼 중 username 에
   저장할 수 있는 최대 길이를 작성하시오.

   >max_length=150

3. 다음은 로그인 기능을 구현한 코드이다 . 빈 칸에 들어갈 코드를 작성하시오.

   ```python
   from django.contrib.auth.forms import __(a)__
   from django.contrib.auth import __(b)__ as auth_login
   
   def login(request):
       if request.method == "POST":
           form = __(a)__(request, request.POST)
           if form.is_valid():
               auth_login(request, __(c)__)
               return redirect('accounts:index')
       else:
           form = __(a)__()
       context = {
           'form':form,
       }
       return render(request, 'accounts/login.html', context)
   ```

   > (a) : AuthenticationForm
   >
   > (b) : login
   >
   > (c) : form.get_user()

4. 로그인 했는지 확인하기 위하여 User 모델 내부에 정의된 속성의 이름을 작성하시오.

   > .is_authenticated

5. 로그인을 하지 않았을 경우 template에서 user 변수를 출력했을 때 나오는 클래스의
   이름을 작성하시오.

   >AnonymousUser

6. django에서 기본적으로 사용하는 User 모델에서 암호화를 하기 위해 사용되는
   알고리즘의 이름을 작성하시오.

   >PBKDF2 algorithm(with a SHA256 hash)

7. 로그아웃 기능을 구현하기 위하여 다음과 같이 코드를 작성하였다. 로그아웃 기능을
   실행 시 문제가 발생한다고 할 때 그 이유와 해결 방법을 작성하시오.

   ```python
   from django.contrib.auth import logout
   
   def logout(request):
       logout(request)
       return redirect('accounts:login')
   ```

   >정의된 함수 `logout`가 무한히 재귀 호출 되면서 RecursionError가 발생한다.
   >
   >django의 `logout` 함수를 import 할 때 alias를 사용해 이름을 바꿔 import 하거나,
   >
   >정의할 함수 `logout`의 이름을 다른 것으로 바꿔주면 문제가 해결된다.

