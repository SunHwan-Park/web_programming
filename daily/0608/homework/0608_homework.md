# 0608_homework

1. Vuex에 대한 개념과 Vuex를 사용하는 상황에 대해서 공식문서를 참고해 작성해주세요.

   > - Vuex는 Vue.js 앱에서 모든 컴포넌트에 대해 중앙 집중식 저장소 역할을 하는 라이브러리이다. 
   > - Vue.js 앱의 컴포넌트 구조가 단순할 때는, props와 events를 통한 부모 자식 간 state 공유만으로도 데이터 흐름을 만들어내는 데 충분하지만, 구조가 복잡해질수록 컴포넌트간 state를 공유하고, 이를 유지 보수하는 데 어려움이 생길 수 있다.
   > - 이러한 상황에서 모든 컴포넌트에서 공유된 상태를 추출하고 이를 전역 싱글톤으로 관리하는 Vuex는 하나의 효율적인 도구가 될 수 있다.

2. Vuex의 핵심적인 네가지 속성을 작성하시오.

   > - state(상태)
   >   - 중앙 저장소에서 관리할 모든 데이터의 집합
   > - getters
   >   - state의 데이터를 가공/활용해서 특정한 값을 반환할 함수의 집합
   >   - computed와 비슷한 개념
   > - mutations(변이)
   >   -  state의 데이터를 변경하는 함수의 집합
   >   - mutations에 작성되지 않은 state 변경 코드는 모두 동작하지 않는다.
   >   - 모든 mutation 함수들은 동기적으로 동작하는 코드이다.
   >   - `store.commit`을 통해 호출한다.
   >   - 첫 번째 전달 인자로 state를 받는다.
   > - actions(액션)
   >   - 범용적으로 사용되는 함수의 집합
   >   - mutations에 정의한 함수 역시 actions에서 실행 가능하다.
   >   - 비동기 로직은 actions에서 정의한다.(정의 할 수 있다.)
   >   - `store.dispatch`를 통해 실행한다.
   >   - 첫 번째 전달 인자로 context를 받는다.
   >   - `context.commit`을 호출하여 mutation을 commit 하거나, `context.state`와 `context.getters`를 통해 state와 getters에 접근할 수 있다.

3. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - Vuex는 데이터의 상태를 관리하는 최적화된 형태의 라이브러리이기 때문에 항상 사용하는 것이 좋다.

     > False
     > Vuex는 공유된 상태 관리를 처리하는 데 유용한 도구이지만, 사용법을 이해하고 초기에 필요한 것을 구성하는 데 비용이 든다. 단순한 형태의 Vue.js 앱을 만든다면 Vuex 없이도 충분하다.  

   - Vuex store는 반응형이다.

     > True

   - Vuex store는 저장소의 상태를 직접 변경할 수 있다.

     > False
     >
     > Vuex 저장소에서 실제로 상태를 변경하는 유일한 방법은 mutation 뿐이다. 즉, component에서의 mutation 호출을 통해서만 상태 변경이 가능하다.