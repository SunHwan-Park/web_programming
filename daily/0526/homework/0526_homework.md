# 0526_homework

1. computed와 watch의 개념과 그 차이에 대해서 간략하게 설명하시오.

   > - 두 속성 모두 Vue 인스턴스의 데이터 변경을 관찰하고 이에 반응하는 속성이다.
   >
   > - watch는 감시할 데이터를 지정하고 해당 데이터가 바뀌면 특정 함수를 실행하라는 '명령형' 프로그래밍 방식
   > - computed는 계산해야 하는 목표 데이터를 정의하는 '선언형 프로그래밍' 방식
   > - 되도록 computed를 사용하는 것이 좋다.

2. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - 동일한 노드에 v-for와 v-if, 두 디렉티브가 함께 있다면 v-if가 더 높은 우선 순위를 가지며, v-if 는 루프가 반복 될 때마다 실행된다.

     > False. v-for가 v-if 보다 높은 우선순위를 갖는다.

   - Vue.js에서 HTML 속성에 Interpolation(보간법) 형태로 값을 넣을 수 있지만 코드 작성의 통일성을 위해 v-bind 디렉티브를 사용한다.

     > False. Mustaches(이중 중괄호를 활용한 보간법)는 HTML 속성에서 사용할 수 없다.

   - v-bind 디렉티브는 " @ ", v-on 디렉티브는 " : "shortcut(약어)을 제공한다.

     > False. v-bind => ":", v-on => "@"

   - v-model 디렉티브는 input, textarea, select 같은 HTML Element와 단방향 데이터 바인딩을 이루기 때문에 v-model 속성값의 제어를 통해 값을 바꿀 수 있다.

     > False. v-model 디렉티브는 HTML Element와 양방향 데이터 바인딩을 이룬다.

3. 다음의 빈칸 (a), (b), (c), (d)에 들어갈 코드를 작성하시오.

   ```html
   <div id="app">
       <ul>
           <li __(a)__="number in numbers" __(b)__="number % 2 === 0">
          		__(c)__
           </li>
       </ul>
   </div>
   
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
   	const app = new Vue({
           el: '#app',
           __(d)__: {
               numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
           },
       })
   </script>
   ```

   > (a): v-for
   >
   > (b): v-if
   >
   > (c):  {{ number }}
   >
   > (d): data