# Web Programming_bootstrap

## Bootstrap

- Bootstrap은 HTML, CSS, JS로 구성된 웹 개발을 위한 오픈소스 라이브러리(프레임워크)

- **반응형, 모바일 대응**을 위한 프론트엔드 컴포넌트

## Start Bootstrap

- 부트스트랩은 설치해서 사용하는 개념 X
- 라이브러리의 HTML, CSS, JS 소스를 **끌어와서** 사용한다.

1. 소스코드 다운

   - [Bootstrap Download](https://getbootstrap.com/docs/4.4/getting-started/download/)
   - 소스를 다운받아 작성하려는 HTML에 링크로 연결

2. **CDN**

   - [BootstrapCDN](https://getbootstrap.com/)

   - 작성하려는 HTML에 Bootstrap 웹서버에 올라가있는 소스코드를 연결

   - CSS Only

     - `<head>` 안에 작성

     ``` html
     <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
     ```

   - JS, Popper.js, and jQuery

     - `<body>` 닫는 태그 전에 작성
       - 사실 어디에 넣어도 코드를 돌리는 데는 문제가 없지만, **성능상으로 뒤에 오는 것이 유리**하다.
       - 처음에 페이지 로드할 때 끌고 올게 너무 많으면 과부하가 걸릴 수 있기 때문
       - 요즘에는 브라우저가 좋아져서 웬만한 경우 큰 상관이 없다.

     ```html
     <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js" integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n" crossorigin="anonymous"></script>
     <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
     <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js" integrity="sha384-wfSDF2E50Y2D1uUdj0O3uMBJnjuUD4Ih7YwaYd1iqfktj0Uod8GCExl3Og8ifwB6" crossorigin="anonymous"></script>
     ```

## Reboot(규격 초기화)

- 부트스트랩의 CSS는 웹페이지의 스타일을 초기화 시킨다.
- 브라우저마다 제각기 다른 기본 스타일 세팅을 초기화 해, 크로스브라우징 문제를 해결한다. 
- Reset CSS vs Normalize CSS
  - Reset CSS: 브라우저 간의 스타일 차이를 최대한 없애서, **스타일이 0인 상태**로 만드는 것
  - Normalize CSS: 스타일 초기화 시키지만 어느정도의 **고유한 스타일이 가미**되어 있는 것
    - Boostrap Reboot의 경우는 Normalize CSS!

## 상속

- bootstrap의 경우 상속이 잘 이뤄지지 않는 경우가 많다.
- 되도록 각 요소별로 스타일을 먹이는 것이 좋다.
  - 스타일 가독성 측면에서도 좋음!

## Utilities

> 대표적인 utilities

* position
* display
* spacing - `margin`, `padding` 
* border
* color
* flex

## Component

* alerts
* badge
* breadcrumb
* button
* card
* carousel
  * JS
* Form / input
* modal
  * JS
* Navbar
  * JS
* Pagination

## grid

> grid system은 균형감 있는 레이아웃을 구성하기 위한, 즉 균일한 콘텐츠 디자인을 위한 레이아웃 시스템이며, bootstrap에서는 반응형으로 레이아웃 자유롭게 구성할 수 있다.
>

* [break point](https://getbootstrap.com/docs/4.4/layout/grid/#grid-options)
  * `.col` , `.col-sm`, `.col-md`, `.col-lg`, `.col-xl`
* 왜 이렇게 크기가 정해졌지?
    - 모바일세로, 모바일가로, 태블릿, 데스크탑에 맞춰서
    - 유통되고 있는 디바이스 중 가장 작은 너비를 기준으로 break point를 잡음
* `.container`
  * 항상 bootstrap의 grid system을 사용하려면, 상위에 `.container`가 존재해야 합니다.
  * `.container`
  * `.container-fluid`
* `.row`
  * 12개의 컬럼으로 구성
    - 숫자 12 - 약수가 많아서, 즉 나누기가 편해서
  * `.col-{breakpoint}-{number}`
* `Gutter`: 항목간 간격, 각 항목의 패딩으로 이루어짐
  - default: 좌우간격 30
  - `.no-gutters`를 **row**에 주면 gutter를 없앨 수 있다.
* flex로 구현되어 있다는 점!
  - flex의 요소들을 사용가능하다!
* offset
  - 레이아웃 배치 시 공백을 활용하고 싶을 때!
  - 항목 class에 `.offset-?-?` 형식으로 달아줌 : offset 먼저 먹이고 저 들어가겠습니다
  - flex가 없던 시절, 아이템 앞에 한 칸씩 밀어서 정렬하기 위해서 사용했었다.
  - 이제는 활용도가 좀 떨어짐

* nesting
  - 하나의 항목 안에 또 다시 grid

* img-fluid: 이미지의 크기를 반응형 조절

## 미디어쿼리 살펴보기

```css
// Extra small devices (portrait phones, less than 576px)
@media (max-width: 575.98px) { ... }

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) and (max-width: 767.98px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) and (max-width: 991.98px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) and (max-width: 1199.98px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```

```css
// Extra small devices (portrait phones, less than 576px)
// No media query for `xs` since this is the default in Bootstrap

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```

