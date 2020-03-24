# 0324_homework

```html
<div class="{a}">
  <div class="{b}">
    <div class="col-{c}-{d}">...</div>    
  </div>
</div>
```

### 1. 상단 코드에 Bootstrap Grid System을 적용시키고자 할 때, {a}, {b} 각각에 입력해야 할 클래스 이름을 작성하시오.

> Answer:
>
> - {a} : container
> - {b} : row



### 2. Bootstrap Grid System에서 요소의 크기를 지정하기 위해서는 상단 코드와 같은 형태로 클래스 이름을 지정해야 한다.

- {c}에 들어갈 수 있는 값과 그 값들이 가지는 의미를 작성하시오.

  > Answer:
  >
  > - (None): device의 너비와 관계없이(특정 조건 없을 경우) columns의 레이아웃을 지정
  > - sm: device의 **너비가 576px 이상**일 때, columns의 레이아웃을 지정
  > - md: device의 **너비가 768px 이상**일 때, columns의 레이아웃을 지정
  > - lg: device의 **너비가 992px 이상**일 때, columns의 레이아웃을 지정
  > - xl: device의 **너비가 1200px 이상**일 때, columns의 레이아웃을 지정

- {d}에 들어갈 수 있는 값과 그 값들이 가지는 의미를 작성하시오.

  > Answer:
  >
  > - 들어갈 수 있는 값: **정수 0 ~ 12**
  > - 한 row의 12개의 columns 중 해당 item에 **몇 column을 할당**할 것인지 지정 



### 3. Align-items-center를 사용하려면 d-flex 클래스와 함께 사용하여야 했었다. 그러나, Grid System 에서는 d-flex 클래스를 생략하여도 올바르게 동작한다. 그 이유를 작성하시오.

```html
<div class="container">
  <div class="row align-items-center">
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns  
    </div>
    <div class="col">
      One of three columns  
    </div>
  </div>    
</div>
```

> Answer: 부트스트랩에서 `row` 클래스의 `display`가 `flex`이기 때문



### 4. Nav를 그림과 같이 오른쪽 정렬 하고자 할 때 {a}에 들어가야 할 클래스 이름을 작성하시오.

​									  																										Active		Link

```html
<ul class="nav {a}">
  <li class="nav-item">
  	<a class="nav-link active" href="#">Active</a>
  </li>
  <li class="nav-item">
  	<a class="nav-link" href="#">Link</a>
  </li>
</ul>
```

> Answer:
>
> - {a} :  **justify-content-end**(부트스트랩에서 `nav` 클래스의 `display`는 `flex`이다)