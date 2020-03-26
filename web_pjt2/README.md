# SSAFY_Web Project 2 [서울 / 3기/ 박선환]

### 새롭게 익히게 된 것들

- 네비게이션

  - `.navbar navbar-expand-md` 클래스 이용해 viewport 가로크기에 따라 서로 다른 스타일을 적용하는 방법
  - `text-[color]-[number]` 클래스 이용해 각 페이지마다 해당 페이지의 nav title을 강조하는 방법
  - nav 요소에 modal 연결하는 방법 / modal 구성하는 방법

- `container`, `row`, `col-[breakpoint]-` 이용해 viewport 가로크기에 따라 한 줄당 요소 개수 지정하는 방법

- `ul`, `li` 요소의 속성 변경(border, list-style)을 통해 하나의 표처럼 보이게 하는 방법

- media query 이용해 viewport 가로크기에 따라 특정 요소는 보이게(혹은 보이지 않게 하는 법)

  ```css
  <!-- viewport 가로크기가 992px 이상일 때 -->
  .board-normal {
      display: none !important;
  }
  .board-lg {
      display: block !important;
  }
  
  <!-- viewport 가로크기가 992px 미만일 때 -->
  @media screen and (max-width: 991px) {
      .board-normal {
          display: block !important;
      }
      .board-lg {
          display: none !important;
      };
  }
  ```

- `.pagination` 클래스 이용해 게시판 아래 pagination 추가하는 방법

  ```html
  <nav class="d-flex justify-content-center my-3" aria-label="Page navigation">
      <ul class="pagination">
          <li class="page-item"><a class="page-link" href="#">Previous</a></li>
          <li class="page-item"><a class="page-link" href="#">1</a></li>
          <li class="page-item"><a class="page-link" href="#">2</a></li>
          <li class="page-item"><a class="page-link" href="#">3</a></li>
          <li class="page-item"><a class="page-link" href="#">Next</a></li>
      </ul>
  </nav>
  ```

---

### 어려웠던 부분

- `.navbar navbar-expand-md` 클래스를 부트스트랩 document에서 찾아서 네비게이션 부분을 그나마 수월하게 작성할 수 있었다. 처음에 직접 media query를 걸고 viewport 가로크기에 따라 서로 다른 요소로 레이아웃을 바꾸려고 했었는데... 쉽지 않았다 @_@
- media query의 개념을 알고는 있었으나, 막상 사용하려고 할 때 낯설어서 애를 먹었다.
- (명세서 조건은 아니었지만..)Home 화면의 카드들의 위아래 간격을 자유롭게 하는 방법을 결국 찾지 못했다...ㅠ_ㅠ (후에 더 연구할 예정)