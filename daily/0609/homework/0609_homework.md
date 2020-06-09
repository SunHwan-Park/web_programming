# 0609_homework

1. MVVM은 무엇의 약자인지 작성하시오.

   > M - Model : 앱에서 사용되는 데이터 및 데이터 처리 파트
   >
   > V - View : 사용자에게 보여지는 UI 파트
   >
   > VM - View Model : View를 나타내주기 위한 Model이자 View를 나타내기 위한 데이터 처리를 하는 파트

2. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   1. Vue.js에서 반응형은 data가 변경되면 이에 반응하여 연결된 DOM이 다시 렌더링 되는 것을 의미한다.

      > True

   2. 동일한 노드에 v-for, v-if 두 디렉티브가 함께 있다면 v-if가 더 높은 우선 순위를 가진다.

      > False

   3. npm은 Node Package Manager의 약자로 자바스크립트 런타임 환경 Node.js의 기본 패키지 관리자이다.

      > True

   4. Vue 인스턴스는 Vue 컴포넌트이며 .vue 확장자를 통해 SFC를 용이하게 구현할 수 있다.

      > True

   5. 컴포넌트에서 data는 반드시 object를 리턴해야한다.

      > False

   6. 상태 관리 패턴은 어떤 경우에도 최적화 되어 있기 때문에 SPA 개발을 한다면 항상 숙지하여 사용해야한다.

      > False

3. 아래는 Vue Router와 관련된 코드이다. 빈칸에 들어갈 코드를 작성하시오.

   ```js
   // router/index.js
   const routes = [
       {
           path: '/lunch',
           name: 'Lunch',
           component: Lunch
       }
   ]
   ```

   ```vue
   <!-- App.vue -->
   <template>
   	<div id="app">
           <div id="nav">
       		<__(b)__ to="__(a)__">Lunch</__(b)__>        
   	    </div>
           <__(c)__/>
       </div>
   </template>
   ```

   > (a) : /lunch
   >
   > (b) : router-link
   >
   > (c) : router-view

4. 아래의 코드에서 increment 메서드가 실행될 때 단방향 데이터 흐름에 대해서 설명하시오.

   (Action, State, View의 관점에서 설명하시오.)

   ```js
   new Vue({
   	// 상태
       data() {
           return {
               count: 0
           }
       },
       // 뷰
       template: `
   		<div>{{ count }}</div>
   	`,
       // 액션
       methods: {
           increment() {
               this.count++
           }
       }
   })
   ```

   > - 메서드가 실행되기 전 상태의 `count` 값 0이 뷰에서 보여진다. (상태 => 뷰)
   > - increment 메서드가 실행되면 상태의 `count`의 값이 1 증가한다.(액션 => 상태)
   >
   > - 상태의 `count` 값이 변화함에 따라 뷰에서 1이 보여지게 된다.(상태 => 뷰)