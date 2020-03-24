## 0316 solution

```javascript
const form = document.querySelector('form');
const users = ['admin', 'ssafy', 'test'];

form.addEventListener('submit', function(event) {
  // 각 변수에 담기 위한 코드 입니다. 수정을 금합니다.
  event.preventDefault();
  const formData = new FormData(event.currentTarget);
  const userName = formData.get('username');
  const password = formData.get('password');
  const passwordConfirmation = formData.get('password_confirmation');
  // 개발자 도구를 통해 해당 값들을 모두 확인하세요.
  console.log(userName, password, passwordConfirmation);
    
  // 위의 값들을 활용하여, 회원가입 로직을 작성하시오.
  if (users.includes(userName)) {
    alert('존재하는 회원입니다.');
  } else if (password != passwordConfirmation) {
    alert('비밀번호가 일치하지 않습니다.');
  } else {
    alert(`${userName}님, 회원가입을 축하합니다.`);
  }
})

```

> `includes()` 메서드는 자바스크립트 배열이 특정 요소를 포함하는 지 판별합니다.
>
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes

* 추가 안내 I - `formData`

  * `formData`에 저장된 값은 `console.log` 를 통해 디버깅할 수가 없습니다.

    * 브라우저 정책

  * 따라서, 여러분들이 디버깅할 수 있도록 편의상 각각의 변수를 `.get(key)` 로 꺼내서 코드를 작성하였습니다.

  * 추후에 서버로 값을 보내는 경우에는 추가 변형 없이 `formData` 값 자체를 보내는 형식으로 구성합니다.

  * 디버깅은 할 수 없지만 아래와 같이 구성되어 있다고 생각하셔도 됩니다 :)

  * 다만 form에 작성된 내용은 일반적으로 서버로 전송되는 값이므로 직접 `formData.username` 이 아니라 메서드롤 통해서 접근할 수 밖에 없다 정도로만 기억 해주시면 감사하겠습니다.

    ```js
    const formData = {
        username: 'ssafy',
        password: 'ssafy_pw
        password_confirmation: 'ssafy_pw'
    }
    ```

    

* 추가 안내 II - `formData` 에서 key는 어떤 설정 때문인가요?

  * formData에서 key가 `username`, `password`, `password_confirmation`으로 작성된 이유는 마크업 되어 있는 HTML에서 `input` 태그에 정의된 `name` 속성에 정의된 값이기 때문입니다.
  * 추후에 Django 수업에서 `form`, `input` 태그 들에 대해서 자세히 학습 하게 될 예정입니다.



* 추가 안내 III - `preventDefault()` 
  * 왜 `preventDefault()`를 해 두었는지에 대한 궁금증이 있을 수 있어 설명 드립니다.
  * `preventDefault()` 는 원래 해당 이벤트가 발생했을 때 하는 일을 하지 않도록 합니다. (기본 내용을 방지)
  * `form` 태그의 제출을 하게 되면 일반적으로 해당 값을 전송하게 되어 페이지 전환이 발생합니다.
    * 예를 들면, 입력하고 회원가입을 하면 서버에 제출되고 회원가입 축하 메시지들을 볼 수 있겠죠.
  * 따라서, 전송되는 것을 방지하고 여러분이 해당 로직을 작성하고 디버깅 할 수 있도록 작성 해둔 겁니다.
    * 나중에는 비동기 처리를 통해서 아래의 코드를 더 작성하여 데이터를 보내는 작업도 하게 됩니다! 



## 결론

아래의 내용으로만 중심으로 익히시면 됩니다. 나머지는 django를 학습하면서 추가적으로 배워 나갈 내용들입니다 :) 

* 조건문 실습

* 이벤트 리스너 코드 구조 확인

  ```js
  form.addEventListener('submit', function(event) {
  	// 함수 내용
  })
  ```

* `event` 객체의 `preventDefault()`의 의미