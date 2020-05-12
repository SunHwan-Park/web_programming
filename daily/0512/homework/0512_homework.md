# 0512_homework

1. "Javascript는 \_\_(a)\_\_ 를 조작할 수 있는 유일한 언어이며 전세계에서 가장 인기 있는 프로그래밍 언어 중 하나이다.” \__(a)__에 들어갈 말을 작성하시오.

   > (a): Browser(브라우저)

2. Javascript에서 변수를 다룰 때 사용하는 키워드는 크게 var, let, const 3가지가 있다. 각각의 핵심 특징을 나열하고 block scope와 function scope의 차이를 나타내는 예시를 작성하시오.

   > - var
   >   - 변수 할당 및 선언을 몇 번이고 자유롭게 할 수 있다.
   >   - Function Scope
   > - let
   >   - 변수 할당을 자유롭게 할 수 있지만, 선언은 최초 한 번만 할 수 있다.
   >   - 변수 선언을 먼저하고 나중에 값을 할당할 수 있다.
   >   - Block Scope
   > - const
   >   - 변수 할당과 선언을 한 번씩만 할 수 있다.
   >   - 변수 선언과 할당을 동시에 해야한다.
   >   - Block Scope
   >
   > ```js
   > // Function Scope & Block Scope
   > 
   > if (true) {
   >     var name1 = 'park' // function scope => console.log(name1)과 같은 선상 
   >     let name2 = 'sum' // block scope => console.log(name2)와 다른 선상
   >     
   >     function scopeTest() {
   >         var name3 = 'hwan' // function scope => console.log(name1)과 다른 선상
   >     }
   > }
   > 
   > console.log(name1) // 출력 O
   > console.log(name2) // 출력 X
   > console.log(name3) // 출력 X
   > ```

3. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - JavaScript에서는 python의 type()과 비슷하게 typeof 연산자를 통해서 자료형을 파악할 수 있다.

     > True

   - JSON은 Javascript Object Notation의 약자로 Javascript의 Object 표기법을 따른 문자다.

     > True

   - 화살표 함수는 함수의 선언식 & 표현식과 문법적으로 차이가 있지만 내부 동작은 완전히 동일하기 때문에 무엇을 사용하든 관계없다.

     > False, 화살표 함수는 익명 함수로만 사용할 수 있다. 따라서 화살표 함수를 호출하기 위해서는 함수 표현식을 사용해야한다.

   - null과 undefined는 javascript의 설계상의 실수이며 typeof 연산자를 통해 확인해보면 모두 undefined로 나온다.

     > False, null의 자료형은 object이다. 

4. 동등 연산자(==)와 일치 연산자(===)의 차이를 간략히 설명하시오.

   > - 동등 연산자(==)
   >   - 왼쪽 피연산자와 오른쪽 피연산자의 값이 값으면 참을 반환함
   > - 일치 연산자(===)
   >   - 왼쪽 피연산자와 오른쪽 피연산자의 값이 같고, **같은 타입이면** 참을 반환함
   >   - 일반적으로 사용