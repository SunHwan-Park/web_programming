# 0527_homework

1. 아래의 설명을 읽고 T/F 여부를 작성하시오.

   - 컴포넌트를 생성할 때 data 속성은 함수를 정의하여 return 해야만 한다.

     > True

   - vue-cli를 사용하지 않으면 vue 프로젝트를 시작할 수 없다.

     > False. 할 수 있지만 일일히 필요한 요소를 짜야한다.

   - javascript에서 모듈을 불러오기 위해서는 불러오는 파일에서 내보내는 작업을 해줘야만 한다.

     > True

2. vue router를 추가하면서 설정하는 history mode의 의미를 작성하시오.

   > history.pushState API를 활용하여 페이지를 다시 로드하지 않고 URL 탐색(뒤로가기, 앞으로 가기 등)을 할 수 있다.

3. 다음과 같은 경로로 이동하는 route-link 를 작성하시오.

   ```js
   const routes = [
       {
           path: '/about',
           name: 'About',
           component: About
       }
   ]
   ```

   > `<router-link to="/about">About</router-link>`