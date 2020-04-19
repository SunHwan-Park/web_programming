# Web Programming_flex

## HTML / CSS 배치 핵심

- 왼쪽 위에 쌓인다
- 블록: 전체 너비
- 인라인: 컨텐츠 너비
- 일반적인 배치 흐름을 깨는 것
  - float
  - position(relative, absolute)
  - flex

## flex

- `flex` 이전에는 자유로운 배치를 위해서 `float`, `position` 지정을 해야 했다.

### flex 주요 개념

![flex_container_item](images\flex_container_item.png)

- container / item

  ```html
  <stlye>
      .container {
  	    display: flex;
      }
  </stlye>
  
  <div class="container">
      <div class="item"></div>
      <div class="item"></div>
  </div>
  ```

- main axis / cross axis

- `flex` 정의시 기본 사항

  - `main axis` 을 기준으로 배치가 시작된다.(기본은 `row`)
    - 만약, `row-reverse`로 지정하게 된다면, 오른쪽 끝부터 배치가 시작됨.
  - 모든 `item`은 행으로 배치된다.(`flex-direction`:`row` 값으로 기본 설정 됨.)
  - 모든 `item`은 `cross axis`을 모두 채운다.(`align-items`의 기본값이 `stretch`)
  - 모든 `item`은 본인의 너비 혹은 컨텐츠 영역만큼 너비를 가지게 된다.
    - 경우에 따라서, 본인이 지정받은 너비보다 작을 수 있다.
      - `flex-wrap`의 기본값이 `nowrap`이기 때문
      - 전체 아이템의 너비의 합이 컨테이너의 너비보다 작을 때!

![flex_row_column](images\flex_row_column.png)


### flex 속성

1. `flex-grow`

   > **남은 너비**(`container` 의 너비 - `item` 너비의 합)를 **각각의 비율로** 나눠서 가져간다. 

   - 기본값: `0`

2. `justify-content`

   > `main-axis`의 정렬을 할 수 있다.

   - `flex-start`: 앞쪽 정렬(기본값)
   - `center`: 가운데 정렬
   - `flex-end`: 끝쪽 정렬
   - `space-around`: 앞 뒤 여백을 포함한 아이템들이 총 영역을 동등하게 나눠가진다. 
   - `space-between`: 아이템 간 간격을 같게 배치(첫/끝 여백 없음)
   - `space-evenly`: 아이템 간 간격을 같게 배치(첫/끝 여백 있음)

   ![flex_justify_content](images\flex_justify_content.png)

3. `align-items`

   > `cross-axis`의 정렬을 할 수 있다.

   - `stretch`: `container`의 영역을 `item`의 영역을 늘려 다 채운다.(기본값) 단, `min-width`와 `max-width` 속성은 지켜진다.
   - `flex-start`: 앞쪽 정렬
   - `center`: 가운데 정렬
   - `flex-end`: 끝쪽 정렬
   - `baseline`: 각 `item` content의 `baseline`을 맞춰서 배치한다.
     - 각 item들의 `font-size`가 다를 때 활용할 수 있다.

   ![flex_align_items](images\flex_align_items.png)

4. `align-content`

   > 여러 줄들 사이의 간격을 지정할 수 있다.

   - `align-items`는 컨테이너 안에서 **어떻게 모든 요소들이 정렬**하는 지를 지정한다.
   - 한 줄만 있는 경우, `align-content`는 효과를 보이지 않는다.
   - 기본값이 `stretch`

   ![flex_align_content](images\flex_align_content.png)

5. `flex-wrap`

   > `item`들을 한 줄에 담을 지 여러 줄에 담을 지 지정할 수 있다.

   - `nowrap`이 기본값 => 한 줄안에 무조건 담는다.
   - `wrap` => 각각의 너비만큼 영역을 가지고, 한 줄에 자리가 없으면 다음 줄에 넘긴다.
   - `wrap-reverse` => 방향이 반대로

6. `flex-flow`

   > `flex-direction`과 `flex-wrap`의 속성값을 한 번에 지정할 수 있다.

   - `flex-flow`: `flex-direction` `flex-wrap` 형태로 사용
   - ex) `column wrap`: `column` 방향, `wrap` 적용

7. `order`(각 `item`에 적용)

   > 아이템의 순서를 정의할 수 있다.

   - 기본값: `0`
   - 음수값도 가질 수 있음

8. `align-self`(각 `item`에 적용)

   > 각 아이템에 직접 `align-items`의 규칙을 지정할 수 있음(cross axis 기준의 배치)
   
   - `align-items`보다 우선순위가 높다.

