# SSAFY_Web Project [서울 / 3기/ 박선환]

### 새롭게 익히게 된 것들

- `position: fixed` 이용해 특정 요소의 화면 내 위치를 고정시킬 수 있다.
  
  - `top`, `bottom`, `right`, `left` 활용해 요소의 위치를 조정할 수 있다.
  - `header(navigation)`와  `footer` 부분을 각각 위/아래에 고정시킬 때, 중간 `body` 부분의 위/아래 `padding` 을 `header`와 `footer`의 높이 만큼 줘야 콘텐츠가 겹치지 않을 수 있다.
- `<br>` 태크 이용해 간편하게 텍스트 줄바꿈을 할 수 있다.
- `<button>` 태크 이용해 버튼을 생성할 수 있다.
  
  - `width`, `height` : 버튼 크기 설정
  - `background-color` : 버튼 배경 색 설정
  - `border`: 버튼 경계 설정(굵기, 색 등)
  - `border-radius`: 버튼 모서리 설정
- `:hover`를 활용해 마우스를 올렸을 경우의 요소 상태를 변화시킬 수 있다.
- `<figure>`, `<figurecaption>` 태그를 이용해 이미지와 캡션을 묶어 표현할 수 있다.
  
- `caption-side`: 캡션 위치 설정
  
- 하나의 `<div class="main">` 전체의 너비를 고정하고, 화면 내에서 가운데 정렬 하는 방법

  - ```css
    .main {
        margin: auto;
        width: 720px;
    }
    ```

- 요소 `<article class="comm_article">`의 아래 테두리만 보이게 하는 방법

  - ```css
    .comm_article {
        border-bottom: solid rgb(150, 150, 150) 1.5px;
    ```

---

### 어려웠던 부분

- 프로젝트를 시작할 때, 어떤 단위의 요소들까지 같은 클래스를 부여하고, 해당 클래스를 활용해 디자인을 적용해야할 지 감이 잘 잡히지 않았다. 프로젝트를 진행하면서 구조를 구성하는 데 조금은 익숙해진 것 같다.
- 마찬가지로, 요소들을 정렬할 때, 어느 단계에서 정렬을 먹여야 할 지도 처음에는 헤맸지만 프로젝트를 진행하며 적응이 됐다.