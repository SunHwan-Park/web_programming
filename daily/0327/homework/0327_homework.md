# 0327_homework

### 1. Django는 MTV 디자인 패턴으로 이루어진 Web Framework이다. 여기서 MTV는 무엇의 약자이며 각각 MVC 디자인 패턴과 어떻게 매칭이 되는지 작성하시오.

> - M: Model(Model과 매칭)
> - T: Template(View와 매칭)
> - V: View(Controller과 매칭)

### 2. ____(a)____는 Django에서 URL 자체를 변수처럼 사용해서 동적으로 주소를 만드는 것을 의미한다. (a)는 무엇인지 작성하시오.

> Variable Routing

### 3. Django 프로젝트는 render할 template 파일들을 찾을 때, 기본적으로 settings.py에 등록된 각 앱 폴더 안의 (a) 폴더 내부를 탐색한다. (a)에 들어갈 폴더 이름을 작성하
시오.

> templates

### 4. Static web page와 Dynamic web page의 특징을 간단하게 서술하시오.

> - Static Web Page
>   - 사용자가 해당 Web Page에서 기본적으로 제공해주는 콘텐츠 이외에 다른 것을 요청하고 제공받지 못한다.(별도의 action이 없는 single page)
>   - 모든 사용자들은 해당 Web Page에서 똑같은 화면을 볼 수 밖에 없다.  
> - Dynamic Web Page
>   - 사용자가 해당 Web Page에서 기본적으로 제공해주는 콘텐츠 이외에도 다른 것을 요청하고 제공받을 수 있다.(사용자가 동적으로 action을 하면 그에 따른 웹페이지의 반응이 존재함)
>   - 각 사용자들은 해당 Web Page에서 모두 다른 화면을 볼 수 있다.