# 9장.쿠키와 세션 알아보기

## 9.1 웹 페이지 연결 기능

### 세션 트래킹

HTTP 프로토콜 방식으로 통신하는 웹 페이지들은 서로 어떠한 정보도 공유하지 않음

웹 페이지 사이의 상태나 정보 공유를 위해선 프로그래머가 세션 트래킹이라는 웹 페이지 연결 기능을 구현해줘야함

>####  :pushpin:stateless 와 stateful
>
>서로 다른 컴퓨터끼리의 통신 방식
>
>stateless 는 브라우저가 데이터를 전송할 때마다 연결하고 바로 끊어버림
>
>HTTP 프로토콜을 사용하는 웹은  stateless 방식이 적합하고 MMORPG 같은 게임에서는 stateful 방식이 적합함

웹 페이지를 연동하는 방법들..

1. **<hidden>태그**를 이용하여 웹 페이지들 사이의 정보를 공유하는 방식
2. URL Rewriting: GET 방식으로 URL 정보를 붙여서 다른 페이지로 전송하는 방식
3. 쿠키 - **클라이언트 PC의 Cookie 파일에 정보를 저장**한 후 다른 웹 페이지들이 공유하는 방식
4. 세션 - **서버 메모리에 정보를 저장**한 후 웹 페이지들이 공유하는 방식

## 9.2 <hidden> 태그와 URL Rewriting 이용해 웹 페이지 연동하기

<hidden>태그는 브라우저에 표시되진 않지만 저장된 정보를 서블릿으로 전송할 수 있음

URL Rewriting 을 이용하는 경우엔 GET방식으로 서블릿 뒤에 데이터를 붙여서 전송함

[URL Rewriting 실습](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec01/ex01/LoginServlet.java)

아무튼 위의 두 방법은 너무 불편함



## 9.3 쿠키를 이용한 웹 페이지 연동 기능

#### 📌쿠키란?

웹 페이지들 사이의 공유 정보를 클라이언트 PC에 저장해놓고 필요할때마다  여러 웹 페이지가 공유해서 사용할 수 있도록 하는 방법

#### 쿠키의 특징

1. 클라이언트에 저장됨

2. 저장 정보 용량에 제한이 있음(4kb를 넘지 못함)

3. 보안에 취약함

4. 클라이언트 브라우저에서 사용 유무 선택 가능

5. 웹 사이트 당 하나의 쿠키가 만들어짐

   ❓웹컨테이너에 추가된 컨택스트 기준을 말할는건가?

### 쿠키 API

`javax.servlet.http.cookie` 를 이용

`HttpServletResponse` 객체의 `addCookie()` 메서드를 이용하여 클라이언트에 쿠키를 전송한 후 저장함

`HttpServletRequest` 객체의 `getCookie()` 메서드를 이용하여 쿠키를 서버로 가져옴

setMaxAge() 메서드의 인자값에 따라 Persistence 쿠키를 만들거나 메모리에만 저장하는 session 쿠키를 만들 수 있음

#### Persistence  쿠키 

클라이언트에 파일로 생성되는 쿠키

#### session 쿠키

브라우저 메모리에 저장되는 쿠키

즉, 브라우저를 종료하면 사라짐	

[addCookie 예제](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec02/ex01/SetCookieValue.java)

[getCookie 예제](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec02/ex01/GetCookieValue.java)

## 9.4 세션을 이용한 웹 페이지 연동 기능

#### 세션

쿠키와 달리 세션은 서버의 메모리에 정보를 저장하고 웹 페이지들끼리 공유할 수 있도록 함

그러므로 쿠키보다 보안에 유리함

세션은 각 브라우저당 한개씩 생성됨

#### 세션의 특징

1. 정보가 서버의 메모리에 저장됨
2. 브라우저의 세션 연동은 세션 쿠키를 사용
3. 쿠키보다 보안에 유리
4. 서버에 부하를 줄 수 있음
5. 브라우저 당 한개의 세션이 생성됨
6. 세션은 유효시간을 가짐(기본 30분)

### 세션 API 

 `HttpSession` 클래스 객체를 사용해야함

`HttpServletRequest.getSession()` 메서드를 호출해서 생성

[getSession() 예제](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec03/ex01/SessionTest.java)

[유효시간 변경](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec03/ex02/SessionTest2.java)

[세션 강제삭제](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec03/ex03/SessionTest3.java)

[로그인정보 바인딩](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec03/ex04/SessionTest4.java)

## 9.5 encodeURL() 사용법

브라우저에서 쿠키 사용을 금지할 경우 encodeURL() 을 사용하여 jsessionid 를 서버로 보내서 세션 기능을 사용할 수 있음

> ❓실습코드를 그대로 따라해서 결과는 제대로 얻었지만 어떻게 그렇게 된건지는 이해 못함

[예제](https://github.com/jjy3385/javaWeb/blob/main/pro09/src/sec04/ex01/SessionTest5.java)

## 9.6 세션을 이용한 로그인 예제

[예제경로](https://github.com/jjy3385/javaWeb/tree/main/pro09/src/sec05/ex01)

