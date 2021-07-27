# 4장.ASP.NET 주요 내장 개체(Global.asax)

## Response 개체

aspx.cs 파일에서 Page_Load() 코드블록안에 Response.Write() 를 작성하면 aspx보다 먼저 수행됨

즉, 클라이언트에서 요청을 하면 응답으로 aspx파일을 동적으로 그리고 있음을 확인할 수 있음

이게 ASP.NET임

💯그니까 동적 웹 애플리케이션이란게 별 게 아니고 웹서버(ISS)가 요청시마다 html 등 정적 요소들을 작성해주는 웹 환경을 말하는것임

## Request 개체

QueryString[] 은 Get방식으로 넘어온 값인 Key 와 Value 를 받고자 할 때 사용함

현재 폼의 정보를 서버의  aspx.cs로 전송할 때 FOST 방식이므로 QueryString[] 은 사용이 용이하지 않음

ASP.NET 에서는 Request개체보다는 컨트롤 속성을 사용해서 값을 받는게 일반적임

```C#
string name = Name.Text;
//여기서 Name 은 aspx의 태그 ID
```

## Server 개체

`MapPath()` 로 현재 파일과 같은 경로값을 반환함

❓자바의 컨테이너에 대응되는 개체인가? 

## Application 개체

애플리케이션 단위로 생성되는 공통적 성격의 개체

## Session 개체

사용자(브라우저)별로 생성되는 전용적 성격의 개체

Application 개체나 Session 개체 모두 서버측 메모리(❓)에 저장함

> 메모리가 RAM을 말하는 것임? 아니면 디스크를 말하는 것임?

session 개체는 사용자가 많아지만 기하급수적으로 저장용량이 불어날 수 있으므로 주의

### 📌Global.asax

웹사이트에 접근하는 모든 사용자에 대한 판단을 관리하는 관문 역할을 하는 게이트웨이 파일

application 시작과 종료, session 시작과 종료에 대한 메서드를 작성할 수 있음

## 💼Page 클래스

📌IsPostBack : 다시 게시

IsPostBack = true 라면 다시 게시되었다는 뜻

즉, 페이지가 처음 로드되는 것이 아니라 서버 컨트롤의 이벤트 등에 의해서 다시 로드되었다는 것임

서버 컨트롤에서 버튼을 클릭하면 페이지 깜빡임이 발생함

이 때, aspx는 서버로 요청을 보내면서 Page_Load()를 다시 수행함

그러므로 처음 로드될 때만 처리해줘야할 코드는 `if(!Page.IsPostBack)` 코드 블록 안에 정의해줘야함

그렇지 않으면 버튼 클릭등의 이벤트 처리를 할 때도 Page_Load() 메서드 블록의 모든 코드가 재수행됨

반대로 버튼 클릭 시 Page_load 이벤트 처리기를 실행하지 않고 해당 버튼의 기능만 구현할 수 있게 해주는 Button속성이 있는데 CauseValidation 속성임

한번 써봐야 감이 올 듯

