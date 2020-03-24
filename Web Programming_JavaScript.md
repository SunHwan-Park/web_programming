# Web Programming_JavaScript

## JavaScript

- WHY? - 브라우저 화면을 동적으로 만들기 위해서!

### JavaScript 역사

- 두 아버님: 팀 버너스리(Web 창시자)와 브랜던 아이크(JavaScript 창시자)
- 1990년대 네스케이프사의 Nescape Navigator(NN) 브라우저가 표준
- 정적인 HTML을 동적으로 표현하기 위한 언어 도입을 결정
- 1996년 브랜던 아이크 주도로 개발된 'Mocha'를 자체 브라우저에 도입
- 이후 LiveScript라는 이름을 거쳐 지금의 JavaScript의 이름으로 변경

### 브라우저 전쟁

- MS의 폭발적 성장, IE3에서 자체적인 JScript를 지원, 호환성 문제로 크로스 브라우징 등의 이슈 발생
- Netscape 후계자들은 이후 모질라 재단 기반의 firefox를 개발

### 표준화의 시작

- 계속되는 파편화를 방지하고 모든 브라우저에서 동일하게 동작하기 위한 표준의 필요성 제기
- Netscape는 ECMA 인터네셔널에 기술 규격을 제출한 이후 발전
- 자바스크립트의 고질적 문제들을 많이 해결한 ES2015(ES6)를 지나 현재 ES2019까지 발표
- ES6라고 불리우는 이 버전은 기존 코드를 간결하게 작성할 수 있는 새로운 문법들이 추가 되면서 더욱 발전할 수 있는 계기가 되었음
- Vanilla JS - 순수 자바스크립트(최고의 튜닝은 순정이다...)
  - 크로스브라우징, 간편한 활용 등을 위해 많은 라이브러리 등장(대표적 jQuery)
  - 최근 표준화된 브라우저, ES6 이후의 다양한 도구의 등장으로 순수 자바스크립트 활용의 증대

### 브라우저에서 할 수 있는 일

- 일반적인 프로그래밍 언어가 하는 일
- 전역 객체 window
  - DOM(Document Object Model) 조작
    - 문서에 대한 모든 내용을 담고있는 객체
    - 문서 즉 열려진 페이지에 대한 정보를 따로 객체화 시켜서 관리함
    - JavaScript로 객체화된 모델을 이용하여 동적 HTML을 제어할 수 있다
    - elements(요소)에 대한 접근을 통해 HTML의 내용을 변경할 수 있다
      - getElementsByTagName
      - getElementsById
      - getElementsByClassName
    - CSS(스타일)의 내용 또한 변경 가능하다
  - BOM(Brouser Object Model) 조작
    - 브라우저에 대한 모든 내용을 담고있는 객체
    - 브라우저가 가지고 있는 정보를 따로 객체화 시켜서 관리함
    - navigator, screen, location, frames, history, XHR, 즐겨찾기, 북마크 등등
  - JavaScript
    - Object, Array, Function

### Nodejs

- 원래 자바스크립트는 브라우저 환경에서만 작동
- V8 
  - **브라우저(chrome)**에서 자바스크립트 작동시키는 엔진. 속도가 매우 빨랐음.
- Nodejs 
  - V8 기반으로 만들어진 **컴퓨터에서** 자바스크립트 작동시키는 엔진.
  - 이것이 출시되면서, JavaScript 진영이 확대됨.
  - 자바스크립트는 프론트엔드에서 백엔드 영역까지 두로 활용되게 된다. 

## JavaScript 기초

### 변수 선언

- 변수 선언은 `var` 키워드 활용
- ES6 기준으로 아래와 같은 키워드가 등장한다
  - const
  - let

### 데이터 타입 분류 (typeof)

- 원시 타입(primitive) - 변경 불가능한 값(immutable)
  - boolean - true, false
  - null
  - undefined
  - number
  - string
  - symbol (ES6)
- 객체 타입(object)
  - object: 일반 객체, function, array, date, RegExp

### Number

- 모든 숫자는 number 타입
- 8진수(0), 16진수(0x)로 표현 가능
- 추가적으로 Infinity, -infinity, NaN(Not a Number)도 Number 타입
- 상수의 경우 아래의 내용을 참고하면 좋다.
  - MDN 자바스크립트 number (https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number)
- 정수의 타입이 별도로 없는 것이지, 정수라는 수 체계가 존재하지 않는 것은 아니다
- IEEE 754 표준에 따라서 부동 소숫점으로 표현되며, -2^53 ~ 2^53의 정수만 안전하게 표현 가능하다

### String - 템플릿 문자열 (ES6)

- 템플릿 문자열
  - 편하게 문자열 내에 변수를 사용(string interpolation) 가능 - `${var}`
  - 여러 라인으로 이뤄진 문자열 사용 가능

### null vs undefined

- null
  - **의도적으로** 변수에 **값이 없다**는 것을 명시
  - typeof 출력시 object로 출력되는 것은 설계상의 실수
- undefined
  - 선언 이후 할당하지 않은 변수에 지정된 값
  - 자바스크립트 엔진이 할당 이전에 초기화된 값
  - 직접 값으로 할당해서 사용하는 것 금지

### 객체

- 자바스크립트는 원시 타입(primitive type)을 제외하고는 모두 객체이다.
- 자바스크립트의 객체는 **키(문자열 또는 심볼)와 값(모두)으로 구성된 속성(property)의 집합**이며, 프로퍼티 값이 함수일 경우 구분을 위해 메소드라고 부른다.

> JSON(JavaScript Object Notation)
>
> - 자바스크립트 객체 표기법을 따른다는 의미

### Object 생성 방법

- 객체 리터널로 생성을 하는 경우 키가 문자열로 표기될 수 있다면, 암묵적 형변환이 발생한다.

- 그게 아닌 경우는 반드시 따옴표를 통해서 문자열로 만들어주어야 한다.

  ```javascript
  var myObj = {
      name: "hong",
      'e-mail': "test@test.com"
  }
  undefined
  ```

- 만약, 생성자 함수를 만들어 사용하면 마치 클래스처럼 속성이 동일한 객체를 생성할 수 있다.

  ```javascript
  function Person(name, age) {
      this.name = name;
      this.age = age;
  }
  undefined
  ```

- 다양한 객체 생성법

~~~javascript
var person = {
	name: "hong",
	greeting: function() {
        console.log(`Hi, I'm ${this.name}`)
    }
}
person.greeting()
  /* Hi, I'm hong */
~~~

```javascript
var dog = {}
dog.name = "baduki"
console.log(dog)
  /* {name: "baduki"} */
```

```javascript
/* Array */
/* 자바스크립트 배열은 다음과 같이 생성 가능하다 */
var a = [1, 2, 3, "hi"]
console.log(a)
  /* (4) [1, 2, 3, "hi"] */
var b = new Array()
b[0] = 1
console.log(b)
  /* [1] */
typeof b
  /* "object" */
```

```javascript
/* 함수 */
/* 자바스크립트 함수는 다음과 같이 생성 가능하다 */
/* ES6에서는 화살표 함수(arrow function)이 새롭게 등장 */
function add(num1, num2) {
    return num1 + num2;
}

const sub = function(num1, num2) {
    return num1 - num2;
}
```

### 객체 속성 접근

- 속성 접근은 . 혹은 [] 로 접근 가능하다.

  - 단, 반드시 [] 로 접근을 해야하는 경우가 있다.(따옴표로 속성 선언된 경우)

- ```javascript
  myObj.email
  // Uncaught ReferenceError: ~~~
  myObj['e-mail']
  // "test@test.com"
  ```

### 변수 유효 범위(scope)

- 자바스크립트는 함수 레벨 스코프를 가진다.
- 따라서, 함수 내에서 선언된 변수는 지역 변수이며, 나머지는 전역 변수로 활용된다.
- 변수 선언시 키워드를 쓰지 않으면, 암묵적 전역으로 설정된다.
  - 주의 : 변수가 아닌 **전역객체(window)의 프로퍼티**로 생성.
  - 따라서, delete(객체의 속성을 지우는 연산자)로 지워지는 값.

```javascript
function test() {
    var local = "local" /* 해당 함수에서만 사용되는 지역변수 */
    global = "global" /* 암묵적 전역변수 */
}
console.log(local)
  /* Uncaught ReferenceError: ~~~ */
console.log(global)
  /* global */

delete global
true
console.log(global) /* 암묵적 전역변수는 delete로 지울 수 있다 */
  /* Uncaught ReferenceError: ~~~ */

var real_global = "real_global"
delete real_global /* 전역변수는 delete로 지울 수 없다 */
false
console.log(real_global)
  /* global */
```

### 변수 호이스팅과 let, const(ES6)

- 자바스크립트에서는 **모든 선언을 호이스팅**한다.

- 호이스팅

  - 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 **유효 범위의 최상단**에 선언한다.
    - 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는다.
    - 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.
    - 유효 범위: **함수 블록 {} 안에서 유효**
  - 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
    - 실제로 코드가 끌어올려지는 건 아니며, 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이다.
    - 실제 메모리에서는 변화가 없다.

- 호이스팅의 대상

  - **var 변수 선언**과 **함수선언문**에서만 호이스팅이 일어난다.

    - var 변수/함수의 선언만 위로 끌어 올려지며, **할당은 끌어 올려지지 않는다.**
    - **let/const** 변수 선언과 **함수표현식**에서는 **호이스팅이 발생하지 않는다.**

  - var 변수 vs let/const 변수

    ```javascript
    
    console.log("hello");
    var myname = "park"; // var 변수
    let myname2 = "park2"; // let 변수
    
    /* --- JS Parser 내부의 호이스팅 결과 --- */
    var myname; // [Hoisting] "선언"
    console.log("hello");
    myname = "park"; // "할당"
    let myname2 = "park2"; // [Hoisting] 발생 X
    ```

  - 함수선언문 vs 함수표현식

    ```javascript
    foo();
    foo2();
    
    function foo() { // 함수선언문
        console.log("hello")
    }
    var foo2 = function() { // 함수표현식
        console.log("hello2")
    }
    
    /* --- JS Parser 내부의 호이스팅 결과 --- */
    var foo2; // [Hoisting] 함수표현식의 변수값 "선언"
    function foo() { // [Hoisting] 함수선언문
        console.log("hello")
    }
    
    foo(); // hello
    foo2(); // ERROR!!
    
    foo2 = function() {
        console.log("hello2");
    }
    ```

- ES6에서 새롭게 등장한 let과 const 키워드는 이러한 내용을 방지할 수 있다.

  - 호이스팅 자체가 이뤄지지 않는 것은 아니고, var는 선언과 동시에 초기화(undefined)를 하고, let / const는 선언과 초기화 단계가 분리되어 진행된다.

## JavaScript 문법

- 연산자
- 조건문
- 반복문

### == vs ===

- 동등 연산자(==)
  - 느슨한 같음. 값 비교 및 예상치 않은 변환
- 일치 연산자(===)
  - 엄격한 같음. 형 비교
  - 그냥 이걸 위주로 쓰면 됨.

```javascript
0 == ''
true
0 == '0'
true
'' == '0'
false
```

### 조건문

- if / else if / else

```javascript
const userName = prompt("Hello! Who are you?");
let message = ""

if (userName === "1q2w3e4r") {
    message = "<h1>This is secret Admin page</h1>";
} else if (userName === "happy") {
    message = "<h1>Hacking!</h1>";
} else {
    message = `<h1>hello ${userName}</h1>`;
}
document.write(message);
```

### 반복문

```javascript
for (let j=0; j < 10; j++) {
    console.log(j);
}

let i = 0;
while (i < 10) {
    console.log(i)
    i++;
}
```

## JavaScript 배열 / 함수

### 배열(Array)

- JS에서 배열은 값만 존재한다.

  - 배열 리터럴

    ```javascript
    var a = [1, 2, 3]
    undefined
    a
    // (3) [1, 2, 3]
    //	0: 1
    //	1: 2
    //	2: 3
    //	length: 3
    //  __protp__: Array(0)
    ```

  - Array 생성자 함수

    ```javascript
    var b = new Array(1, 2, 3)
    undefined
    b
    // (3) [1, 2, 3]
    //	0: 1
    //	1: 2
    //	2: 3
    //	length: 3
    //  __protp__: Array(0)
    ```

### 배열 순회

- for

  ```javascript
  var a = [1, 2, 3]
  undefined
  for (var i = 0; i < a.length; i++) {
      console.log(i, a[i]);
  }
  // 0 1
  // 1 2
  // 2 3
  ```

- for ... of

  ```javascript
  var a = [1, 2, 3]
  undefined
  for (var elem of a) {
      console.log(elem);
  }
  // 1
  // 2
  // 3
  ```

- forEach

  ```javascript
  var a = [1, 2, 3]
  undefined
  forEach(function(elem, idx) {
      console.log(idx, elem);
  })
  // 0 1
  // 1 2
  // 2 3
  ```

- for ... in

  - 배열의 요소만 접근 하는 것이 아니라 속성까지 출력될 수 있다.
  - 자바스크립트에서 배열도 object라서 속성 설정이 가능하지만, 리스트의 요소가 아니라 객체의 속성이 된다.

  ```javascript
  var a = [1, 2, 3]
  undefined
  a.name = "myarr"
  a
  // (3) [1, 2, 3, name: "myarr"]
  
  for (var i in a) {
      console.log(i, a[i]);
  }
  // 0 1
  // 1 2
  // 2 3
  // name myarr
  ```

### 배열 메소드

- sort 메소드
  - sort 메소드에 비교 함수가(인자) 없으면 ****문자열 기준으로 정렬**한다.

    ```javascript
    var numbers = [4, 2, 5, 1, 3, 100];
    numbers.sort();
    console.log(numbers);
    // (6) [1, 100, 2, 3, 4, 5]
    ```

  - 비교함수가 있다면, 해당 함수의 리턴값이 0보다 크거나 작음으로 정렬한다.

    ```javascript
    var numbers = [4, 2, 5, 1, 3, 100];
    numbers.sort(function(a, b) { // 비교함수
        return a - b;
    });
    console.log(numbers);
    // (6) [1, 2, 3, 4, 5, 100]
    ```

- join, toString

  ```javascript
  var a = [1, 2, 3]
  a.join('-')
  // "1-2-3"
  a.tosting()
  "1,2,3"
  ```

- concat

  ```javascript
  var a = [1, 2, 3]
  a.concat([4, 5])
  // (5) [1, 2, 3, 4, 5]
  a + [4, 5]
  // "1,2,34,5"
  a.concat(4, 5)
  // (5) [1, 2, 3, 4, 5]
  ```

- 원소 삽입/삭제 push, pop, unshift, shift

  ```javascript
  var a = [1, 2, 3]
  a.push(4) // a = [1, 2, 3, 4]
  a.pop() // a = [1, 2, 3]
  a.unshift(0) // a = [0, 1, 2, 3]
  a.shift(0) // a = [1, 2, 3]
  ```

- 인덱스 탐색 indexOf

  ```javascript
  var a = [1, 2, 3]
  a.indexOf(3)
  // 2
  a.indexOf(5)
  // -1
  ```

- 배열 조작 splice - 원본을 수정

  ```javascript
  /*
  array.splice(start_index, deletecount, replace_item1, replace_item2...)
  */
  
  var a = [1, 2, 3]
  a.splice(1) // index 1부터 잘라내기
  > (2) [2, 3] // 잘라낸 부분
  a
  > [1] // 남은 부분
  
  var a = [1, 2, 3]
  a.splice(1, 2, "처음") // index 1부터 2개 잘라내고 하나 넣기
  > (2) [2, 3] // 잘라낸 부분
  a
  > [1, "처음"] // 남은 부분
  ```

- 배열 자르기 slice - 원본에서 일부분을 리턴

  ```javascript
  /*
  array.slice(start_index, end_index)
  */
  
  var a = [1, 2, 3]
  a.slice(-2) // index -2부터 잘라내기
  > (2) [2, 3]
  a.slice(1, 2) // index 1부터 index 2 전까지 슬라이스
  > [2]
  a.slice(1)
  > (2) [2, 3]
  a.slice()
  > (3) [1, 2, 3]
  ```

## 함수

### 함수 선언

- 함수 선언문

  ```javascript
  function sum(a, b) {
      return a + b;
  }
  sum(1, 2)
  3
  ```

- 함수 표현식

  ```javascript
  var sub = function(a, b) {
      return a - b;
  }
  sub(1, 2)
  -1
  ```

- 즉시 실행 함수

  ```javascript
  (function(a, b){return a + b})(1, 2)
  2
  ```

- 화살표 함수(ES6)

  ```javascript
  var sum = (a, b) => a + b
  sum(3, 4)
  7
  ```

### 함수 인자

- 자바스크립트에서 함수는 매개변수 전달에 대한 제한이 없음

- arguments 객체는 매개변수로 넘겨진 모든 정보를 가지고 있음

  ```javascript
  function foo(a) {
      console.log(arguments);
      return a;
  }
  
  foo()
  > Arguments [collee: f, Symbol (Symbol.iterator): f]
  foo(1, 2, 3)
  > Arguments(3) [1, 2, 3, collee: f, Symbol (Symbol.iterator): f]
  ```