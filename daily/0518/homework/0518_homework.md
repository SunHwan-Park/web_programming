# 0518_homework

1. DOM에서 특정 요소를 선택할 때, document.querySelector() 뿐만 아니라 document.querySelectorAll() 역시 사용 할 수 있다. 이 둘의 차이를 간단하게 작성하시오.

  > - querySelector()
  >   - 한 개의 반환객체를 찾을 수 있다.
  >   - 동일한 클래스명을 가진 객체가 여럿 있을 경우, html 문서내 첫 번째 나타나는 요소를 반환한다.
  >   - #sample => sample 아이디를 가진 요소를 찾는다.
  >   - .sample => sample 클래스명을 가진 요소를 찾는다.
  > - querySelectorAll()
  >   - 조건에 해당하는 모든 객체를 nodeList에 담아 반환한다.
  >   - 반환객체 안에 있는 개별 객체에 접근하기 위해선, for문 혹은 forEach문을 사용해야 한다.

2. DOM에 요소를 추가할 때, innerHTML 속성을 사용하는 방법과 appendChild() 메서드를 사용하는 방법이 있다. 이 둘의 차이를 간단하게 작성하시오.

  > - innerHTML
  >   - 요소를 추가할 객체의 내부 HTML **전체**를 추가/교체한다.
  > - appendChild()
  >   - 요소를 추가할 객체의 **자식리스트 맨 마지막에** 인자(이 또한 하나의 DOM 객체)를 더해준다.

3. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - 콜백 함수는 매개 변수를 통해 전달되고 전달 받은 함수의 내부에서 어느 특정 시점에 실행된다.

     > True

   - EventTarget.addEventListener(type, listener)에서 type은 이벤트의 종류를 의미하고 listener는 이벤트가 발생했을 때, 알림을 받는 객체다.

     > True

   - js에서 함수는 변수에 담을 수 있고, 인자로 전달 할 수 있다. 하지만 반환값으로 전달할 수는 없다.

     > False, JS에서 함수는 1급 객체이므로 변수에 담을 수 있고, 인자로 전달할 수 있으며, 반환값으로 전달할 수 있다.
4. DOM Event에는 다양한 카테고리의 Event들이 존재한다. 아래 제시된 Event들이 각각 어떤 시점에 발생하는지 간단하게 작성하시오.

  - click

    > 포인팅 장치 버튼이 엘리먼트에서 **눌렸다가 놓아졌을 때**

  - mouseover

    > 포인팅 장치가 리스너가 등록된 엘리먼트나 그 자식 엘리먼트의 **위로 이동 했을 때**

  - mouseout

    > 포인팅 장치가 리스너가 등록된 엘리먼트 또는 그 자식 엘리먼트의 **밖으로 이동했을 때**

  - keypress

    > shift, Fn, CapsLock 을 제외한 키가 눌린 상태일 때(연속적으로 실행됨)

  - keydown

    >키가 눌렸을 때

  - keyup

    >키 누름이 해제될 때

  - load

    > 리소스와 그 의존 리소스의 로딩이 끝났을 때

  - scroll

    > 다큐먼트 뷰나 엘리먼트가 스크롤되었을 때

  - change

    > 엘리먼트의 값이 변경될 때