# Web Programming_django_login

User.objects.all()

회원가입 / 로그인 -> auth

authenticate: 검증하다(진짜임을 증명하다)

authorize: 권한을 주다

django.contrib.auth이 관장



- User.objects.create_user => 비밀번호 암호화



### 해시함수

- 어떤 값을 정해진 길이의 16진수 숫자로 만들어주는 함수
- 실제 비밀번호를 DB에 그대로 저장하지 않기 위해 사용
- SHA256: 단방향 알고리즘, 즉 역함수가 존재 X
- 특정 값과 해시함수 적용된 값은 1:1로 대응
- 그래서 서로 다른 값으로 보이게 하기 위해서 비밀번호 각각 salting(추가적인 변환 과정) 작업을 거침



### lazy load

변수 정의하는 시점이 아니라, 

해당 변수가 활용되는 시점에 정의되는 경우

왜? 메모리 최적화를 위해서



### 회원가입(신규 User -> DB에 저장)

- UserCreationForm(C)
  - User.objects.create_user
- UserChangeForm(U)

### 로그인(기존 User -> DB에 있는 지 확인)

- 비밀번호 SHA256 + salting + iteration(시간끌기용)
- git commit sha 1..? => sha2로 바꾼다고..





- create_user : 유저 생성시

- set_password : 비번 재설정(update 할 때)
- get_user_model : 유저 정보 가져올 때
  - get_user_model은 현재 장고 내부에서 활성화된 유저 모델을 가져와주는 메소드입니다. 디폴트로는 장고 내부에 정의된 User모델을 가져와주는데, 추후에 우리가 직접 유저 모델을 정의하게 될 경우 장고 내부의 기본 User모델이 아닌 우리가 커스터마이징한 유저 모델을 가져오기 위해 사용합니다.

### Stateless & Connectless



### 쿠키

- 서버가 클라이언트의 특정 요청에 대한 응답을 줄 때 쿠키를 함께 보내준다.
- 이후 클라이언트의 요청에는 해당 쿠키가 묻어 온다.
- 이로써 쿠키를 통해 특정 상태를 유지할 수 있게 된다.

### 세션

- 어떤 사람이 어떤 쿠키로 접속하고 있는 지 서버 내에 저장해둬야겠다.(pk, remote ip, browser, 구글의 경우 기기정보까지..)
- 이로써 쿠키만 가져와서는 다른 사용자가 같은 상태를 흉내낼 수 없다.
- 서버리소스 사용
- 보안상으로 중요한 정보의 경우는 쿠키로 하면 위험하니 서버에 따로 저장
- 영구 데이터는 아니다... DB가 아닌 인메모리에 임시 저장

로그인과 관련된 form

- AuthenticationForm
  - ModelForm 이 아니다!
  - 태생이 그냥 form(특정 model과 관련이 없음) forms.form을 상속받음
  - request, request.POST
  - 쿠키와 세션 정보 조작
- login 함수
  - request, form.get_user()
  - 로그인 하면 DB 에 django-session 파트에 관련 정보가 임시 저장이 된다.

- 광고 ID





리졸버 매치

- setting - 탬플릿 - context_processors => 컨텍스트에 안넘겨줘도 html에서 쓸 수 있음!
- 장고.탬플릿.context_processors.request





### 캐시 데이터

- 속도를 위해 임시저장되는 반복적으로 쓰이는 데이터
- 자주 주고 받는 데이터를 브라우저, 즉 기기에 저장
- 유효기간이 있다.





### ?next

https://35d6f03d82e44777b8afde250574ccf6.vfs.cloud9.us-west-2.amazonaws.com/accounts/login/?next=/accounts/1/update/

- 성공을 했을 때 내가 바로 어디로 가는가를 적어둔 경로

### login_required

### LOGIN_URL

- 기본은 /accounts/login/
- 만약 다른 url 설정하려면 기본값 변경 해줘야함 (settings.py)
- login_required 와 관련됨



AuthenticationForm => DB에 저장할 것이 아니라서, ModelForm X

DB에 있고, 비번도 맞으면 session에 해당 유저에 정보 저장

=> auth_login() 하면 한방에 ㅎㅎ

