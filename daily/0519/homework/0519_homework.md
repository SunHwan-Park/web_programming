# 0519_homework

1. Non Blocking 과 Blocking 의 차이를 간단하게 작성하시오.

   > - Non Blocking
   >   - 한 작업이 완료되지 않은 상태에서 다른 처리 작업을 계속 진행할 수 있도록 한다.
   > - Blocking
   >   - 한 작업을 진행하는 동안 프로그램의 진행(다음 작업의 진행)을 멈추고 결과를 도출할 때까지 기다린다.

2. "\_\_(a)\_\_ 는 XHR(XMLHttpRequest)을 보내고 응답받는 결과를 \__(b)__ 객체로 반환해주는 라이브러리이다.” 빈칸 (a)와 (b)에 들어갈 단어를 작성하시오.

   > (a) : axios
   >
   > (b) : Json

3. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - 페이지 전환 없이 화면의 일부분을 변경하기 위해서 JavaScript를 이용해야만 한다.

     > True

   - setTimeout(myCallbackFunction, 1000)에서 1000이 의미하는 것은 콜백 함수가 1초 뒤에 실행될 것이라는 의미다.

     > True

   - 페이지의 일부만 갱신하는 것은 브라우저가 해당 페이지의 특정한 부분의 DOM만 다시 그리는 것이다.

     > True

4. 다음은 JavaScript 코드를 활용해 작성한 좋아요 코드의 일부분이다 . (a), (b), (c)에 들어갈 코드를 작성하시오.

   ```html
   <!-- index.html -->
   <script>
     const likeButtons = document.querySelectorAll('.like-button')
     likeButtons.forEach(button => {
       button.addEventListener(__(a)__, function (__(b)__) {
         const articleID = event.target.dataset.id
         axios.get(`/articles/${article.id}/like/`)
         .__(c)__(response => {
           ...
         })
       }
     })
   </script>
   ```

   > (a) : 'click'
   >
   > (b) : event
   >
   > (c) : then