# .net framework 와 .net core

## Web Form

- winform 처럼 개발이 가능한 형태
- 웹페이지 내에 소스코드가 존재할 수 있음
- 유지보수가 굉장히 어려움
- 이벤트마다 페이지가 다시 로드됨, 즉 서버를 갖다옴, 그래서 느림
- 히든태크인 viewState 를 사용하여 컨트롤의 상태를 저장하고 있음, 따라서 html이 더러워짐
- MVC나 Web API 보다 성능이 부족하여 ERP같은 업무용 웹에 적합함

## ASP.NET MVC

- model ,view controller 형태임
- 요청,응답 기반의 웹 개발자에게 익숙한 형태

## SignalR

- 실시간 채팅 서비스 등 실시간 처리가 필요한 경우 사용함

## Web API

- 데이터베이스에서 받아온 정보를 XML,JSON 형식으로 송출해주는 서비스
- RESTful API
- Stateless
- 최고의 장점은 모든 플랫폼과 통신이 가능하다는 것임

    즉, XML,JSON 형식으로 안드로이드,ISO앱에 데이터를 보내줄 수 있음
