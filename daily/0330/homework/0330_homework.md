# 0330_homework

#### 아래 링크를 참고하여 각 문제들을 해결하기 위한 코드를 작성하시오.

> https://docs.djangoproject.com/en/2.1/ref/templates/builtins/

1. menus 리스트를 반복문으로 출력하시오.

   ```html
   {% for __(a)__ in menus %}
     <p>{{ menu }}</p>
   {% endfor %}
   ```

   > Answer: (a) = menu

2. posts 리스트를 반복문으로 활용하여 0번 글부터 출력하시오.

   ```html
   {% for post in posts %}
     <p>{{ __(a)__ }}번글 : {{ post }}</p>
   {% endfor %}
   ```

   > Answer: (a) = forloop.counter

3. users 리스트가 비어있다면 **현재 가입한 유저가 없습니다.** 텍스를 출력하시오.

   ```html
   {% for user in users %}
     <p>{{ user }}</p>
   {% __(a)__ %}
     <p>현재 가입한 유저가 없습니다.</p>
   {% endfor %}
   ```

   > Answer: (a) = empty

4. 첫 번째 반복문일 때와 아닐 때를 조건문으로 분기처리 하시오.

   ```html
   {% __(a)__ forloop.first %}
     <p>첫 번째 반복문 입니다.</p>
   {% __(b)__ %}
     <p>첫 번째 반복문이 아닙니다.</p>
   {% endfor %}
   ```

   > Answer: (a) = if, (b) = else 

5. 출력된 결과가 주석과 같아지도록 하시오.

   ```html
   <!-- 5 -->
   <p>{{ 'hello'__(a)__ }}</p>
   <!-- My Name Is Tom -->
   <p>{{ 'my name is tom'__(b)__ }}</p>
   ```

   > Answer: (a) = |length, (b) = |title

6. 변수 today에 datetime 객체가 들어있을 때 출력된 결과가 주석과 같아지도록 하시오.

   ```html
   <!-- 2020년 02월 02일 (sun) PM 02:02 -->
   {{ today|date:"__(a)__" }}
   ```

   > Answer: (a) = Y년 m월 d일 (D) A h:i

---

#### 다음은 form tag에 관한 문제이다. 올바른 답을 작성하시오.

```html
<form action="/create" method="">
    <input type="text" name="title">
    <input type="text" name="content">
    <input type="text" class="my-site">
    <input type="submit">
</form>
```

1. 지문의 코드 중 form 태그의 속성인 action의 역할에 대해 설명하시오.

   > Answer: 사용자로부터의 form 내용을 받아서 처리하는 url 지정(form 내용을 전송할 서버 쪽 스크립트 파일 지정)

2. 지문의 코드 중 method가 가질 수 있는 속성 값을 작성하시오.

   > Answer: method => 브라우저에서 form data를 가져와 서버로 보내는 기능 수행
   >
   > - GET: form data를 URL 끝에 붙여서 보낸다(눈으로 확인가능)
   > - POST: form data를 보이지 않게 보낸다

3. input 태그에 각각 '안녕하세요', '반갑습니다', '파이팅' 문자열을 넣고 submit 버튼을 눌렀을 때 이동하는 url 경로를 작성하시오.

   > Answer: /create?title=안녕하세요&content=반갑습니다

