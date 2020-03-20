# Web Programming_JS Function

## 함수의 고급 기능

### 함수의 기본

- 함수 선언문
- 함수 표현식
- 즉시 실행 함수

### 함수 호이스팅

- 자바스크립트에서는 모든 선언이 호이스팅 된다.
  - let, const
- 앞서 설명한 함수 선언 방식의 가장 큰 차이점은 아래와 같다.
  - 함수 선언문의 경우 **선언, 초기화, 할당이 모두 이뤄져** 실행 가능
  - 함수 표현식은 **변수 호이스팅이 발생**하여, undefined, 즉 실행 불가.

### Array helper methods

- forEach: 주어진 함수를 **배열의 요소 각각에 대해 실행**
- filter: 주어진 함수를 배열의 요소 각각에 대해 실행하여 **반환 값이 true인 요소를 모아 배열을 반환**
- map: 주어진 함수를 배열의 요소 각각에 대해 실행한 결과를 모아 배열을 반환
- every: 주어진 함수에 모든 요소가 true인 경우 true (boolean 값을 반환)
- some: 주어진 함수에 하나라도 true인 경우 true (boolean 값을 반환)
- 이외에도 reduce, find 함수 등이 존재한다.

## JavaScript Closure

### First class function

- 자바스크립트 함수는 아래와 같은 특징을 가진다.
  - 함수를 **인자로 전달 가능**함
  - 함수를 **반환**할 수 있음
  - **변수에 함수를 할당** 가능함
- 위의 조건은 프로그래밍 언어에서의 **일급 객체**(first class object / first class citizen)의 조건이다.

### Closure

- 클로저는 함수와 함수가 선언된 **어휘적 환경(Lexical scoping, environment)의 조합**이다.

- 함수 안의 함수를 호출할 때, 그 함수의 내용 뿐만 아니라 **그것을 감싸고 있는 외부함수의 환경 역시 함께 가져온다.**

  ```python
  # python
  def count():
      cnt = 0
      
      def plus():
          nonlocal cnt # unboundlocalError 방지
          cnt += 1
          return cnt
      
      return plus
  
  a = count()
  print(a()) # 1 -> a로 호출된 함수 환경을 공유!
  print(a()) # 2 -> a로 호출된 함수 환경을 공유!
  b = count() # a로 호출된 함수(+환경)와는 다른 것!
  print(b()) # 1
  print(b()) # 2
  ```

  ```javascript
  /**javascript**/
  funtion count() {
      var cnt = 0
      
      return function() {
          cnt += 1
          return cnt
      }
  }
  
  var a = count()
  console.log(a()) // 1 -> a로 호출된 함수 환경을 공유!
  console.log(a()) // 2 -> a로 호출된 함수 환경을 공유!
  var b = count() // a로 호출된 함수(+환경)와는 다른 것!
  console.log(b()) // 1
  console.log(b()) // 2
  ```
