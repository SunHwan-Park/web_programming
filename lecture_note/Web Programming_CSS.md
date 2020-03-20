# Web Programming_CSS

## CSS

- Cascading Style Sheets
- 웹 문서(어플리케이션)의 **스타일을 정의**하는 역할(HTML은 문서의 구조를 정의)

- 기본 사용법 => **Selector {Property: Value}**

## CSS 정의 방법

- 인라인(inline): HTML 문서 내부 특정 태그에, 직접 style 프로퍼티를 활용해 스타일 적용.
- 내부참조(embedding): HTML 파일 내에 `<style>` 태그를 생성해 스타일 지정.
- 외부참조(link file): 외부 CSS 파일을 HTML 파일의 `<head>` > `<link>` 통해 불러오기.

## 선택자(Selector)

- HTML 문서에서 특정한 요소를 선택하여 스타일링 하기 위해서는 반드시 선택자라는 개념이 필요하다.
- 기초 선택자
- 고급 선택자
  - 자손 선택자, 직계 자손 선택자
  - 형제, 인접형제 선택자, 전체 선택자
- 의사 클래스(pseudo class)
  - 링크, 동적 의사 클래스
  - 구조적 의사 클래스
  - 기타 의사클래스, 의사 엘리먼트, 속성 선택자

## CSS 상속

- CSS는 상속을 통해 부모 요소의 일부 속성을 자식에게 상속한다.
- 속성 중에는 상속이 되는 것과 되지 않는 것이 있다.
  - 상속 되는 것
    - Text 관련 요소(font, color, text-align), opacity, visibility
  - 상속 되지 않는 것
    - Box model 관련 요소(width, height, margin, padding, border, box-sizing, display)
    - Position 관련 요소(position, top/right/bottom/left, z-index)

## CSS 적용 우선순위(cascading order)

- CSS 우선순위를 아래와 같이 그룹을 지어볼 수 있다.
  - 중요도(Importance) - 최우선 적용(사용시 주의)
    - !important
  - 우선순위(Specificity) - 그 다음 적용
    - 인라인/id 선택자/class 선택자/요소 선택자
  - 소스 순서 - 그 다음 적용

```css
CSS
h3 { color: violet !important }
p { color: green; }
.blue { color: blue; }
.skyblue { color: skyblue; }
#red { color: red; }
```

```html
HTML
<p>1</p> => green(요소 선택자)
<p class="blue">2</p> => blue(class 선택자가 요소 선택자에 우선)
<p class="blue skyblue">3</p> => skyblue(class 선택자 중 뒤에 적힌 소스)
<p class="skyblue blue">4</p> => skyblue(class 선택자 중 뒤에 적힌 소스)
<p id="red" class="blue">5</p> => red(id 선택자가 class 선택자에 우선)
<h3 id="red" class="blue">6</h3> => violet(!important)
<p id="red" class="blue" style="color: yellow">7</p> => yellow(인라인 CSS)
<h3 id="red" class="blue" style="color: yellow">7</h3> => violet(!important)
```

## CSS 단위

### 크기 단위

- px(픽셀)
- %(퍼센트)
- em: **배수** 단위, 요소에 지정된 사이즈에 **상대적인 사이즈**를 가짐
- rem: **최상위 요소(html)의 사이즈를 기준**으로 배수 단위를 가짐.
- Viewport 기준 단위
  - vw, vh, vmin, vmax

### 색상 단위

- HEX(00~ff): 16진수의 2자리 숫자 세 개(빨/초/파)를 활용
  - #ffffff
- RGB(0, 255): 빨/초/파의 정도
  - rgb(0, 0, 0)
- RGBA: RGB + Opacity
  - rgba(0, 0, 0, 0.3)

## CSS Box model

### Box model 구성

- Content: 실제 내용이 위치
- Padding: 테두리 안쪽의 내부 여백. **요소에 적용된 배경의 컬러, 이미지는 패딩까지 적용.**
- Border: 테두리 영역
- Margin: 테두리 바깥의 외부 여백. 배경색을 지정할 수 없다.

### box-sizing

- 기본적으로 모든 요소의 box-sizing은 content-box
  - Padding을 제외한 순수 contents 영역만을 box로 지정.
  - 즉, 해당 요소에 width를 100px를 주었을 때,
    우리 눈에 보이는 해당 요소(content+background+border)의 너비는,
    100px + padding * 2 + border-width * 2 가 된다.
- 다만, 우리가 일반적으로 영역을 볼 때는 border 까지의 너비를 100px 보는 것을 원함.
  - 이 경우 box-sizing을 border-box로 설정!

### 마진 상쇄(Margin collapsing)

- 인접 형제 요소 간의 margin은 겹쳐서 보인다.
- 따라서, 인접 형제 요소의 마진 중 더 큰 것이 둘 사이의 간격이 된다. 

## CSS Block / Inline

### 블록 레벨 요소와 인라인 레벨 요소

- 대표적인 블록 레벨 요소
  - div / ul, ol, li / p / hr / form 등
- 대표적인 인라인 레벨 요소
  - span / a / img / input, label / b, em, i, strong 등

### display: block

- **줄 바꿈이 일어나는 요소**
- 화면 크기 **전체의 가로폭을 차지**한다.
- 블록 레벨 요소 안에 인라인 레벨 요소가 들 어갈 수 있음.
- 요소의 크기가 한 줄을 다 점유할 수 없다면 **나머지를 다 margin으로** 둔다.
- 속성에 따른 수평 정렬
  - `margin-right: auto;` => 왼쪽 정렬
  - `margin-left: auto;` => 오른쪽 정렬
  - `margin-right: auto; margin-left: auto;` => 가운데 정렬

### display: inline

- **줄 바꿈이 일어나지 않는 행의 일부 요소**
- **content 너비만큼** 가로폭을 차지한다
- width, height, margin-top, margin-bottom을 지정할 수 없다.
- **상하여백은 line-height로 지정**한다.
- 속성에 따른 수평 정렬
  - `text-align: left` => 왼쪽 정렬
  - `text-align: right` => 오른쪽 정렬
  - `text-align: center` => 가운데 정렬

### display: inline-block

- block과 inline 레벨 요소의 특징을 모두 갖는다.
- inline 처럼 한 줄에 표시 가능하며,
- block 처럼 width, height, margin 속성을 모두 지정할 수 있다.

## CSS Position

- static : 디폴트 값(기준 위치)
  - 기본적인 요소의 배치 순서에 따름**(좌측상단)**
  - 부모 요소 내에서 배치될 때는 **부모 요소의 위치를 기준**으로 배치 된다.
  - 요소가 점유하고 공간은 **해당하는 줄 전체**
    - 실제 요소 이전/이후로는 전부 margin으로 가진다
- 아래는 좌표 프로퍼티(top, bottom, left, right)를 사용하여 이동이 가능하다.(음수값도 가능)
  - relative(상대위치) : **static 위치를 기준**으로 이동
    - 원래 있어야 할 곳(구조상)에 위치
    - but 우리에게 보이기에, 원래 위치에서 상대적으로 이동한 모습으로 보인다.
    - 따라서 원래 **점유한 위치는 그대로 점유**!
    - **실제 보이는 곳은 미점유**!
  - absolute(절대위치) : **static이 아닌** 가장 가까이 있는 부모/조상 요소를 기준으로 이동
    - 이동 시 원래 본인의 위치는 잃는다(집을 나간다). 하지만 **실제 보이는 위치 역시 점유하지 않는다.(붕 떠 있음)**
    - 그렇게 되면 다른 형제 요소들의 위치가 변동 될 수도 있다.(빈 공간을 자동으로 채워서 점유하기 때문)
    - 사용 시 항상 조심해야한다.
  - fixed(절대위치): 부모 요소와 관계없이 **브라우저를 기준**으로 이동
    - **스크롤 시에도 항상 같은 곳에 위치**(ex) nav 부분이 상단에 고정된 경우)

## CSS float 속성

- float는 요소를 일반적인 흐름(normal flow)에서 벗어나도록 하는 속성 중 하나
  - **반드시 clear 속성을 통해 초기화가 필요**하며, 예상치 못한 상황이 발생할 수 있음.
- 아래와 같은 배치에서 일반적으로 많이 쓰임
- float를 사용하는 경우 block 사용을 뜻하며, display 값이 inline인 경우 block으로 계산된다.
- 둥둥 떠다니는 녀석들...
- float left / float right
- **공간을 점유**한다. 다만, 다음 요소가 들어올 때 **해당 줄에 공간이 남아있으면 해당 공간으로 치고 들어온다.**

## float가 발생 시키는 문제

- 자식 요소의 float 속성으로 인해 부모 영역의 높이가 사라지는 문제

- clear 한 요소의 margin이 제대로 표현이 되지 않는 문제

- 해당 문제를 해결하기 위한 방법 중 하나

  - 의사 요소 선택자 활용

  - ```css
    .clearfix::after {
        content: "";
        display: block;
        clear: both;
    }
    ```

  - clearfix를 **부모 요소에 적용**

## CSS Layout

### HTML/CSS의 기본 특징

- 일반적으로 HTML 요소들은 문서의 위에서부터 아래로 순차적으로 나열된다.
- 아래의 방법들을 통해 변경될 수 있다.
  - display 속성을 통해 요소가 보여지는(표현되는) 방식 변경
    - block, inline, inline-block
    - table, fllexible box, grid 등의 레이아웃을 활용
  - position 속성을 통해 **위치 자체를 변경**
  - float 속성을 통해 **떠 있도록 만듦**

### CSS를 어렵게 만드는 요소

- 일반적인 흐름(Normal flow)을 바꿔버리는 경우!
- Normal flow
  - inline, block, relative position
- Floats
- Absolute positioning

### inline-block 주의사항

- display 속성이 inline 혹은 inline-block인 경우 4px의 공간이 있음.
- 이유는 소스코드 상의 **공백** 때문에!

### `display: none` vs `visibility: hidden`

- `display: none` => 공간 점유 X
- `visibility: hidden` => 공간 점유 O