# Web Programming_HTTP

url에는 길이제한이 있다..일정 길이 넘어가면 오류뜸

### 요청 처리 방식

- GET
  - 정보를 가져오는 것

- POST
  - DB에 어떤 값을 저장하는 것
  - token
  - CSRF 사이트 간 요청 위조를 막기 위해 쓰는 방법 중 하나가 
    - CSRF Token 사용
    - form tag 안에 token 값을 넣어두고, 이를 검증하는 방식



- get => 특정한 리소스를 리턴한다
- post => 특정 리소스에 엔티티를 제출한다. 서버의 상태 변화나 부작용을 일으킨다



url의 변수화



- curl: 요청 보내주는 친구(command line)
- telnet: 탑골 curl
  - 접속: telnet 도메인 포트번호
  - method http 버전
  - Host: 도메인
- traceroute(tracert)



- app_name
- {% url %}
- POST 보내는 법



- get : 데이터를 가져오다
- post: 데이터를 게시하다(서버에 입력값을 보내서 조작한 값을 가져옴)



message framework를 다른 방식으로 띄울 수 있을까?

HTTP(요청과 응답의 규약)의 특징 - 단절성(가벼운 연결을 위해서)

- stateless(무상태성)
  - 상태가 없다. 과거가 없다. 바로 직전에 뭘했는 지 모른다.
  - 새로운 request는 이전의 기반이 없고 완전히 새로운 요청으로 다가간다.
  - 그래서 연결이 가볍다.
- connectionless(무연결성)
  - 요청과 응답이 끊나고 나면, 연결이 끝난다.



즉 message framework는

이전의 상태를 다음 req&res 사이클에 넘겨준다.

session storage