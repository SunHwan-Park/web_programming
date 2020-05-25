# 0525_homework

1. SPA는 무엇의 약자인지 작성하고, 의미하는 바를 간략하게 작성하시오.

   > Single Page Application: 사용자의 특정한 요청에 대해 새로운 페이지를 불러오지 않고, 현재 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹서비스를 의미한다.

2. MVVM은 무엇의 약자인지 작성하고, 해당 패턴에서 Vue.js 가 담당하는 부분을 작성하시오.

   > - Model: 어플리케이션에서 사용되는 데이터와 그 데이터를 처리하는 부분 / object
   > - View: 사용자에게 보여지는 UI 부분 / HTML
   > - View Model: View를 나타내주기 위한 Model이자, View를 나타내기 위한 데이터 처리를 하는 부분 / Vue(object)

3. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - SPA는 웹 어플리케이션에 필요한 모든 정적 리소스를 한번에 받고 이후부터는 페이지 갱신에 필요한 데이터만 전달 받는다.

     > True

   - 모든 Vue 앱은 Class로부터 새로운 Vue 인스턴스를 생성하는 것부터 시작한다.

     > True

   - Vue.js에서 말하는 '반응형'이라는 것은 데이터가 변경되면 이에 반응하여 연결된 DOM이 업데이트 되는 것을 의미한다.

     > True

4. 다음의 빈칸 (a), (b), (c)에 들어갈 코드를 작성하시오.

   ```html
   <div id="app">
       {{ __(c)__ }}
   </div>
   
   <script>
   	const app = new __(a)__({
           el: __(b)__,
           data: {
           	message: '안녕하세요 Vue!'
   	    }
       })
   </script>
   ```

   > (a): Vue
   >
   > (b): '#app'
   >
   > (c):  message