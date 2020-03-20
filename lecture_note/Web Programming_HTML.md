# Web Programming_HTML

## Web_basic

- 기본 구조
  - 클라이언트가 서버에 '**요청(request)**'하고, 서버가 클라이언트에 '**응답(response)**'
  - 무엇을? => **웹 문서**를!

- IP(Internet Protocol)
  - 172.217.27.78 => 구글의 IP
  - 8비트(0~255)까지의 숫자로 구성된 숫자의 집합으로, **각자가 가지고 있는 주소**와 동일하다.

- Domain
  - google.com
  - **네트워크 상의 컴퓨터를 식별**하는 **호스트명**
- URL(Uniform Resource Locator)
  - https://www.google.co.kr/serach?q=구글
  - 도메인 + 경로, 실제로 해당 **서버에 저장된 자료의 위치**
- 웹표준과 브라우저 전쟁
  - 1차 전쟁의 승자 IE(Window OS에 끼워팔기 성공)
  - 하지만 이후 브라우저에 소홀했던 IE, chrome 및 다른 브라우저에 밀려남

---

## HTML

- Hyper Text Markup Language: **웹 페이지를 작성하기 위한(구조를 잡기 위한) 역할 표시 언어**
- Hyper Text : **문서들이 서로 링크로 연결**이 되는 비선형적인 텍스트
  - HTTP : hyper text transfer protocol
- Markup : 가독성과 편리성을 높여주는 문서 구조 방식(Markdown과 유사)

- 현재 표준 - HTML5
  - 결국 2019년 5월 W3C(연구자 협회) 와 WHATWG(기업들의 연합)의 대통합...! (사실상 WHATWG의 승리)

- Visual Studio Code(IDE)
  - HTML/CSS 코드 작성을 위한 VS code 추천 패키지
    - HTML Snippets (3.9M), HTML CSS Support(4.2M)
    - Open in browser (1.7M)
    - Auto rename tag (4.1M), Auto close tag (3.8M)

---

## HTML 문서의 기본 구조

- DOM(Document Object Model) 트리 구조(부자, 형제 관계)
  - document
    - html
      - head
        - title
          - My title
        - body(head의 자손이자 title의 형제이자 h1의 부모)
          - h1
            - A heading

```html
/*DOCTYPE 선언부: 사용하는 문서의 종류를 선언하는 부분. 보통 html를 사용한다.*/
<!DOCTYPE html>

/*html 요소: HTML문서의 최상위 요소로 문서의 root를 뜻한다. head와 body 부분으로 구분된다.*/
<html lang="ko">
    
/*head 요소: 문서 제목, 문자코드(인코딩)와 같이 해당 문서 정보를 담고 있으며, 브라우저에 나타나지 않는다. og와 같은 메타데이터를 통해 웹 문서의 대한 추가 정보를 선언한다. CSS 파일 혹은 자바스크립트 파일 등 외부 파일을 연결할 수 있다.*/
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
    
/*body 요소: 브라우저 화면에 나타나는 정보로 실제 내용에 해당한다.*/
<body>
</body>
    <header>
        <h1>title</h1>
        <nav></nav>
    </header>
    <div>
        <section>
	        <h1></h1>
            <article></article>
        </section>
    </div>
    <footer>
    </footer>
</html>
```

- Open Graph Protocol

  - 페이스북에서 만든 메타 데이터 표현하는 새로운 규약
  - 메타정보에 해당하는 제목, 설명 등을 쓸 수 있도록 정의(**링크 미리보기**에 등장)
  - 카톡 공유할 때 뜨는 제목과 이미지

- 시맨틱태그

  - HTML5에서 **의미론적 요소**를 담은 태그의 등장(div를 사용하지 않고!)
  - 개발자 및 사용자 뿐만 아니라 검색엔진 등에 의미 있는 정보의 그룹을 태그로 표현
  - 단순히 구역을 나누는 것 뿐만 아니라 의미를 가지는 태그들을 활용하기 위한 노력
  - Non semantic 요소에는 div, span 등이 있으며, h1, table 태그도 시맨틱 태그로 볼 수 있다.
  - 검색엔진최적화(SEO)를 위하여 메타태그, 시맨틱태그 등을 통한 마크업을 효과적으로 할 필요가 있다.
    - header : 문서 전체나 섹션의 헤더
    - nav : 내비게이션
    - aside : **사이드에 위치한 공간**, 메인 콘텐츠와 관련성이 적은 콘텐츠
    - section : 문서의 일반적인 구분, **컨텐츠의 그룹**을 표현, 일반적으로 h1~h6 요소를 가짐
    - article : 문서, 페이지, 사이트 안에서 **독립적으로 구분되는 영역**(포럼/신문 등의 글)
    - footer : 문서 전체나 섹션의 푸터(**마지막 부분**)

- 그룹 컨텐츠

  - `<p>`: 한 문단의 텍스트
  - `<hr>`: 가로선
  - `<ol>`: 순서가 있는 목록(목록은 `<li>`를 통해 생성)
  - `<ul>`: 순서가 없는 목록(목록은 `<li>`를 통해 생성)
  - `<pre>`: 입력한 형태 그대로 출력할 때 사용, 하지만 각 영역별로 서식을 꾸밀 수가 없다.
  - `<blockquote>`: 인용문. 자동으로 들여쓰기가 된다. `<cite>` 태그와 함께 사용되기도 한다.
  - `<figure>`:  이미지, 오디오, 비디오 등을 담는 컨테이너 태그. `<figureCaption>` 태그와 함께 사용되기도 한다.
  - `<div>`: division의 약자. 특별한 기능이 없고 웹사이트 레이아웃을 만들때 주로 사용한다. **block 속성 요소.**

- 텍스트 관련 요소

  - `<a>`: 하이퍼링크 걸어주는 태그.  `href`로 이동할 링크를 설정
  - `<b>`: 글자를 굵게 표시하는 태그. CSS `font-weight: bold`와 같은 효과.
  - `<strong>`: 글자를 굵게 표시하는 태그. 최신 표준은 이것을 사용할 것을 권고.
  - `<i>`: 글자를 기울여서 표시하는 태그. CSS `font-style: italic`과 같은 효과.
  - `<em>`: emphasize의 약자. 글자를 기울여서 표시하는 태그. 역시 `<i>`보다 이를 권장한다.
  - `<span>`:  특별한 기능이 없는 태그. **inline 속성 요소.**
  - `<br>`: 텍스트 줄바꿈
  - `<img>`: 이미지를 삽입하는 태그. `src`속성을 통해 이미지 경로를 지정. `alt` 속성을 통해 이미지가 로드되지 않을 경우 나타날 텍스트 지정.

- 테이블 관련 요소

  - `<table>`: 표를 만드는 태그

  - `<tr>`: 표의 행

  - `<td>`: 표의 열. `<tr>` 태그 하위에 위치.

  - `<th>`: 표의 제목 셀. `<td>` 태그 대신 사용.

  - `<thead>`: 표의 제목 영역

  - `<tbody>`: 표의 본문 영역

  - `<tfoot>`: 표의 마지막 영역

  - `<caption>`:  표의 캡션을 설정. `caption-side` 속성으로 캡션의 위치를 정한다.

  - `colspan`: `<td>` 태그에서 사용. 열을 좌우로 확장한다.

  - `rowspan`: `<td>` 태그에서 사용. 행을 상하로 확장한다.

  - `scope`: 테이블의 `<th>` 또는 `<td>` 등의 해당 셀에게 사용. 열인지 행인지 알려주는 역할.

  - `<col>`: 테이블 하나 이상의 열 `<td>`에 대해 속성값을 정의한다. 각 셀에 스타일을 반복하는 대신에 열에 대하여 스타일을 동일하게 적용하는 데 유용하다. `<table>`, `<colgroup>` 요소 안에서만 사용가능. 종료 태그가 없다.

  - `<colgroup>`: `<col>`  태그를 그룹으로 관리. 행이 아닌 열단위로 스타일 제어 가능
    다음과 같이 사용

    ```html
    <colgroup>
      <col span="2" style="background: red"/>
      <col style="background: blue"/> /* 기본은 span="1" */
    </colgroup>
    ```

- `<form>` 태그

  - 서버에서 처리될 데이터를 제공하는 역할. **웹페이지에서의 입력 양식**을 의미. 
  - 전체 양식을 의미하며, 화면에 보이지 않는 추상적인 태그이다. 실제로 사용자가 양식을 입력하기 위한 태그는 `<input>` 태그 등이 사용된다.
  - `<form>` 의 기본 속성
    - action
    - method

- `<input>`

  - `type` 속성을 통해 종류를 나타내며,
  - `name` 속성을 통해 데이터의 이름을,
  - `value` 속성을 통해 기본 값을 지정한다.
  - `type` 종류
    - `text`: 일반 문자
    - `password`: 비밀번호
    - `button`: 버튼
    - `submit`: 양식 제출용 버튼
    - `reset`: 양식 초기화용 버튼
    - `radio`: 한개만 선택할 수 있는 컴포넌트
    - `checkbox`: 다수를 선택할 수 있는 컴포넌트
    - `file`: 파일 업로드
    - `hidden`: 사용자에게 보이지 않는 숨은 요소