# 12장. JSP 스크립트 요소 기능

## 12.1 JSP스크립트 요소

JSP페이지에서 여러가지 동적 처리를 하는 기능으로  <% %> 안에 자바코드로 구현

<% %> 기호는 스크립트릿이라고 부름

세가지 스크립트 요소가 있음

* 선언문 : 변수나 메서드 선언 시 사용
* 스크립트릿 : 자바코드 작성 시 사용
* 표현식 : 변수의 값 출력 시 사용

## 12.2 선언문 사용

변수나 메서드 선언 시 사용

`<%! 멤버 변수 OR 멤버 메서드 %>`

[선언문 실습](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/hello.jsp)

> 📌.java 파일을 열어보면 jsp 클래스의 멤버 변수로 선언되어 있음

## 12.3 스크립트릿 사용

자바코드 작성 시 사용

`<% 자바코드 %>`

[스크립트릿 실습](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/hello2.jsp)

> 📌.java 파일을 열어보면 jsp 클래스의 `_jspService()` 메서드 내에 선언되어 있음
>
> 서블릿으로 치면 `doXXX()` 메서드 내에 선언되어 있는것과 같음

## 12.4 표현식 사용

변수나 값 출력 시 사용

`<%= 값 or 자바 변수 or 자바 식 %>`

> 세미콜론(;) 안붙임

[표현식 실습](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/hello3.jsp)

> 📌.java 파일을 열어보면 `out.Write(값)` 형태로 변환되어 있음 

## 12.5 JSP 주석문 사용

JSP에 사용할 수 있는 주석문

1. HTML 주석 `<!-- 주석내용 -->` 

   브라우저에서 코드보기로 보면 주석 확인 가능

2. 자바 주석 `/* 주석내용 */` 

   .java 파일에서 주석 확인 가능

3. JSP 주석 `<%-- 주석내용 --%>`

   JSP파일에서만 주석 확인되며 .java 파일이나 브라우저에서는 안보임

   왜냐하면 JSP주석이라 .java로 변환될 때 변환되지 않았기 때문임

[주석실습](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/hello4.jsp)

## 12.7 내장 객체 기능

내장 객체란 JSP가 서블릿으로 변환될 때 컨테이너가 자동으로 생성시키는 멤버 변수를 말함

`_jspService()` 메서드 내에 선언된 객체임

(❓왜 메서드 내부를 스코프로 정한걸까? 요청이 없다면 쓰지 않기 때문에??)

> 📌JSP가 .java로 변환된다고 해왔지만 그냥 서블릿으로 변환된다고 표현해도 될듯

| 내장 객체   | 클래스                                 | 설명                              |
| ----------- | -------------------------------------- | --------------------------------- |
| request     | javax.servlet.http.HttpServletRequest  | 클라이언트의 요청정보 저장        |
| response    | javax.servlet.http.HttpServletResponse | 응답 정보 저장                    |
| out         | javax.servlet.jsp.JspWriter            | JSP 페이지에 결과 출력            |
| session     | javax.servlet.http.HttpSession         | 세션 정보 저장                    |
| application | javax.servlet.ServletContext           | 컨텍스트 정보 저장                |
| pageContext | javax.servlet.jsp.PageContext          | JSP 페이지에 대한 정보 저장       |
| page        | java.lang.object                       | JSP 페이지의 서블릿 인스턴스 저장 |
| config      | javax.servlet.ServletConfig            | JSP 페이지에 대한 설정 정보 저장  |
| exception   | java.lang.Exception                    | 예외 발생 시 예외 처리            |

### 스코프

| 내장 객체   | 서블릿             | 스코프                                                   |
| ----------- | ------------------ | -------------------------------------------------------- |
| page        | this               | 한번의 요청에 대해 하나의 JSP페이지를 공유               |
| request     | HttpServletRequest | 한번의 요청에 대해 같은 요청을 공유하는 JSP페이지를 공유 |
| session     | HttpSession        | 같은 브라우저에서 공유                                   |
| application | ServletContext     | 같은 애플리케이션에서 공유                               |

## 12.8 JSP 페이지 예외처리

### JSP페이지 예외처리 과정

1. 예외처리 담당 JSP 를 만든다

   `<%@ isErrorPage = 'true' %>`

2. 예외 발생 시 예외 처리 담당 JSP 파일을 지정한다

   `<%@ page errorPage = '예외처리.jsp' %>`

> 예외가 발생하면 URL은 기존페이지 URL을 그대로 유지하고 있음
>
> ❓내부적으로 기존페이지에서 예외페이지로 포워딩을 하고 있는 것으로 생각됨

[예외처리 담당 JSP](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/test02/addException.jsp)

[예외처리 담당 JSP를 지정한 JSP](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/test02/add.jsp)

### 에러코드 종류에 따른 예외처리 페이지 지정

모든 페이지에 예외처리 JSP를 지정하는 것은 불편하므로 자주 발생하는 예외코드에 대한 예외처리 페이지를 지정하는 것이 좋을 수 있음

`web.xml` 파일에 `<error-page>` 태그를 사용하면 예외처리 페이지를 에러코드에 따라 지정할 수 있음

또한 `web.xml`에 WELCOME파일도 지정할 수 있음

[web.xml](https://github.com/jjy3385/javaWeb/blob/main/pro12/WebContent/WEB-INF/web.xml)