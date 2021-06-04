# 6.서블릿 기초

## 6-1.서블릿 세 가지 기본 기능

### 서블릿의 세가지 기본 기능

1. 클라이언트로부터 요청을 받음
2. 데이터베이스 연동과 같은 비즈니스 로직 처리
3. 처리된 결과를 클라이언트에 응답

### 서블릿 요청과 응답 수행 API

- 요청 : javax.servlet.http.HttpServletRequest 클래스
- 응답 : javax.servlet.http.HttpServletResponse 클래스

## 6-2. 폼태그 이용해 서블릿 요청하기

```html
<form name="frmLogin" method="get" action="login" encType="UTF-8">
    ...
</form>
```

| 속성    | 기능                                                         |
| ------- | ------------------------------------------------------------ |
| name    | form태그의 이름<br />자바스크립트에서 form태그가 여럿일 때 특정 form태그로 접근할 때 사용 |
| method  | 데이터 전송 방법을 지정할 때 사용<br />GET과 POST로 지정할 수 있으며 기본값은 GET |
| action  | form태그에서 데이터를 전송할 서블릿이나 JSP를 지정<br />서블릿으로 전송할 땐 서블릿 매핑 이름을 사용하면 됨 |
| encType | 전송할 데이터의 인코딩 타입을 지정<br />파일 업로드할 경우엔 `multipart/form-data` 로 지정 |

## 6-3.서블릿에서 클라이언트의 요청을 얻는 방법

HttpServletRequest  객체의 여러가지 메서드를 이용하여 전송된 데이터를 얻음

`String getParameter(String name)` 

[getParameter 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec01/ex01/LoginServlet.java)

`String[] getParameterValues(String name)` 

[getParameterValues 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec01/ex01/InputServlet.java)

`Enumeration getParameterNames()`

[getParameterNames 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec01/ex01/InputServlet2.java)

## 6-4.서블릿의 응답 처리 방법

1. doGet() , doPost() 메서드 안에서 처리
2. javax.servlet.http.HttpServletResponse 객체 사용
3. setContentType() 메서드를 이용하여 전송할 데이터 종류(MIME-TYPE)을 지정
4. 클라이언트와 서블릿의 통신은 자바 I/O의 스트림(PrintWriter) 객체를 이용

> #### MIME-TYPE
>
> 톰캣 컨테이너에 미리 지정해 놓은 데이터 종류
>
> HTML로 전송 : html/text
>
> 일반 텍스트로 전송 : text/plain
>
> XML 데이터로 전송 : application/xml

### 서블릿 응답과정 실습

1. setContentType() 로 MIME-TYPE 지정
2. 데이터를 출력할 PrintWriter 객체 생성
3. 출력 데이터를 HTML 형식으로 만듬
4. PrintWriter 객체의 print() , println() 을 이용하여 데이터 출력

[응답실습](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec02/ex01/LoginServlet2.java)



## 6-5.웹 브라우저에서 서블릿으로 데이터 전송하기

### GET방식과 POST 방식

| get방식                                                      | post방식                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 데이터가 url 뒤에 name=value 형태로 보여지게 전송되므로 **보안에 취약** | TCP/IP 프로토콜 데이터의 body 영역에 숨겨진 채로 전송되므로 **보안에 유리** |
| 전송할 수 있는 데이터는 최대 **255개**                       | 전송할 수 있는 데이터 **무제한**                             |
| 기본방식이며 쉽고 빠름                                       | 전송 시 서블릿에서 또 다시 가져오는 작업을 해야 하므로 처리 속도가 get방식보다 느림 |

**클라이언트에서 보낸 요청이 get인지 post인지 맞춰서 서블릿에서 처리해야함**

[환율계산기 실습](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec02/ex01/CalcServlet.java)

## 6-6.GET 방식과 POST 방식 요청 동시에 처리하기

doGet() doPost() 어떤 메서드든 doHandle() 이란 다른 메서드를 호출하도록 처리

[실습](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec03/ex02/LoginServlet4.java)

## 6-7.자바스크립트로 서블릿 요청하기

```javascript
frmLogin.method = "post";
frmLogin.action = "login5";
frmLogin.submit();
```

자바스크립트에서 form태그에 접근할 때 form태그의 name 속성을 사용함

그리고 폼태그name.submit(); 을 호출하여 클라이언트에서 서블릿으로 요청을 보낼 수 있음

여기 예제에서는 유효성 검사를 위해 자바스크립트를 사용함

[실습 - 자바스크립트코드](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/webapp/login2.html)

[실습 - 자바코드](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec03/ex03/LoginServlet5.java)

## 6-8.여러가지 실습

[구구단1](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec04/ex01/GuguTest.java)

[구구단2](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec04/ex01/GuguTest2.java)

[구구단3](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec04/ex01/GuguTest3.java)

[로그인1](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec04/ex01/LoginTest.java)

[로그인2 ](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro6/src/main/java/sec04/ex01/LoginTest2.java)

