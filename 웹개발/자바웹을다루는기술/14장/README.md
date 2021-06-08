# 14장.표현 언어와 JSTL

## 14.1 표현 언어란?

JSP 2.0부터 자바 코드로 출력하는 표현식을 대체하기 위해 표현 언어라는 것이 등장함

페이지 디렉티브 태그에서 `isELIgnored=false`로 설정해야 사용 가능

(여기까지는 라이브러리 추가 없어도 됨)

```jsp
${표현식 or 값}
```

자료형,연산자 등을 갖춘 간단한 형식의 언어라고 생각하면 됨

empty 연산자만 조금 새롭고 대부분 직관적으로 알아볼 수 있음

#### empty 연산자

해당 객체가 비어있는지 판단하는 연산자

자바 빈 객체에 속성이 있거나 컬렉션 객체(List,Map)에 저장된 객체(값)가 있는지 판별함

## 14.2 표현 언어 내장 객체(내장 변수)

JSP 내장 객체는 표현식에서만 사용이 가능하다

따라서 표현언어에서는 따로 내장 객체를 제공한고 있다

표현 언어 내장 객체는 `${}` 안에서만 사용 가능한다

### 내장 객체의 종류와 기능

* #### 스코프

  * ##### pageScope

    page 영역에 바인딩된 객체 참조

  * ##### requestScope

    request에 바인딩된 객체 참조

  * ##### sessionScope 

    session 에 바인딩된 객체 차조

  * ##### applicationScope

    application에 바인딩된 객체 참조

* #### 요청 매개변수

  * ##### param

    request.getParameter() 메서드를 호출한 것과 같음

  * ##### paramValues

    request.getParameterValues() 메서드를 호출한 것과 같음(여러 개의 값을 전달하는 요청 매개변수 처리)

* #### 헤더 값

  * ##### header

    request.getHeader() 메서드를 호출한 것과 같음

  * ##### headerValues

    request.getHeader()  메서드를 호출한 것과 같음

    요청 헤더 이름의 정보를 배열로 반환

* #### 쿠키 값

  * ##### Cookies

    쿠키 이름의 값을 반환

* #### JSP 내용

  * ##### pageContext

    pageContext 객체를 참조할 때 사용

* #### 초기 매개변수

  * ##### initParam 

    컨텍스트의 초기화 매개변수 이름의 값 반환

[param실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member1.jsp)

[requestScope 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member2.jsp)

[pageContext 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/login.jsp)

> pageContext 객체는 `javax.servlet.jsp.PageContext` 클래스를 상속해 웹 컨테이너가 JSP 실행 시 자동으로 생성해서 제공하는 내장 객체다

[빈 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member3.jsp)

[Collection 객체 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member4.jsp)

> `${Collection객체 이름[index].속성명}` 형식으로 사용

[HashMap 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member5.jsp)

[has-a 관계 빈 실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test01/member6.jsp)

> 📌has-a관계 : 객체가 다른 객체를 속성으로 갖는 경우

## 14.3 표현 언어로 바인딩 속성 출력하기

request,session,application 내장 객체에 속성을 바인딩한 후 다른 서블릿이나 JSP로 전달할 수 있으며 표현 언어로르 사용하여 자바코드 없이 바인딩된 속성 이름으로 바로 값을 출력할 수 있다

[forward1](https://github.com/jjy3385/javaWeb/tree/main/pro14/WebContent/test02/forward1.jsp)

[member1](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test02/member1.jsp)

```jsp
<%
	request.setCharacterEncoding("UTF-8");
	String id = (String) request.getAttribute("id");
	String pwd = (String) request.getAttribute("pwd");
	String name = (String) session.getAttribute("name");
	String email =(String) application.getAttribute("email");
%>
```

member1.jsp의 스크립틀릿 부분이 없더라도 `forward1.jsp` 에서 바인딩되어 넘어온 속성들을 사용할 수 있음

 📌어떤 내장객체인지  상관없이 바인딩된 이름만으로도 접근할 수 있다는 뜻임

그러므로 같은 이름의 속성이 다른 내장 객체에 바인딩되는 경우도 있을 수 있으며 이때는 우선순위가 있음

### 스코프 우선순위

📌page>request>session>application

## 14.4 커스텀 태그

JSP페이지에서 자주 사용하는 자바 코드를 대체하기 위해 만든 태그

커스텀 태그에는 두 종류가 있음

* JSTL(JSP Standard Tag Libaray)
  *  JSP 페이지에서 가장 많이 사용하는 기능의 태그
  * JSTL 라이브러리를 따로 설치해야함
* 개발자가 만든 커스텀 태그
  * 스트러츠나 스프링 프레임워크에서 미리 만들어서 제공함

## 14.5 JSP 표준 태그 라이브러리(JSTL)

커스텀 태그 중 가장 많이 사용하는 태그를 표준화하여 라이브러리로 제공하는 것

톰캣에서 기본 제공되지 않기 때문에 라이브러리를 다운받아 lib 폴더에 넣어야함

### JSTL 태그 종류

| 라이브러리   | 세부 기능                               | 접두어 | 관련 URI                               |
| ------------ | --------------------------------------- | ------ | -------------------------------------- |
| 코어         | 변수 지원,흐름 제어,반복문 처리,URL처리 | c      | http://java.sun.com/jsp/jstl/core      |
| 국제화       | 지역,메시지 형식,숫자 및 날짜 형식      | fmt    | http://java.sun.com/jsp/jstl/fmt       |
| XML          | XML 코어,흐름 제어,XML변환              | x      | http://java.sun.com/jsp/jstl/xml       |
| 데이터베이스 | SQL                                     | sql    | http://java.sun.com/jsp/jstl/sql       |
| 함수         | 컬렉션 처리,문자열 처리                 | fn     | http://java.sun.com/jsp/jstl/functions |

## 14.6 Core 태그 라이브러리 사용

변수 선언,조건식,반복문 등의 자바 코드를 태그로 대체할 수 있도록 함

JSP 기본 라이브러리가 아니기 때문에 자바의 `import`문처럼 JSP 페이지 상단에 다음과 같은 `taglib` 디렉티브 태그를 추가하여 톰캣에게 알려줘야함

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

### < c:set > 태그

변수 선언용 태그

``` jsp
<c:set var="변수 이름" value="변수값" [scope="scope속성 중 하나"] />
```

[실습1](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member1.jsp)

[실습2](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/login.jsp)

```jsp
<c:set var="contextPath" value="${pageContext.request.contextPath }" />
```

위의 코드를 보면 < c:set > 태그를 사용하여 변수 선언만 하는 것이 아니라 너무 길어서 사용하기 불편한 변수나 속성을 간결한 명칭으로 치환해서 쓸 수 있음을 알 수 있다

### < c:remove > 태그

선언한 변수를 제거함

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member3.jsp)

### < c:if > 태그

조건문 태그

```jsp
<C:if test="${조건식}" />
...
</c:if>
```

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member4.jsp)

### < c:choose > 태그

swith문 태그

```jsp
<c:choose>
	<c:when test="${조건식1}">
        ...
    </c:when>
	<c:when test="${조건식1}">
        ...
    </c:when>
    <c:otherwise>
        ...
    </c:otherwise>
</c:choose>
```

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member5.jsp)

### <c: forEach > 태그

반복문 태그

```jsp
<c:forEach var="변수 이름" items="반복할객체이름" begin="시작값" end="마지막값" step="증가값" varStatus="반복상태변수이름">
    ...
</c:forEach>
```

varStatus 속성은 `index`,`count`,`first`,`last` 가 있음

[실습1](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member6.jsp)

> `<c:forTokens>` 태그로 items 문자열을 ',' 마다 잘라서 쓰고 있음

[실습2](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member8.jsp)

> List 에 MemberBean 객체를 담고 차례대로 보여줌(향상된 for문 기능과 같음)

### < c:url > 태그

URL정보를 저장

```jsp
<c:url var="변수이름" value="URL경로" [scope="scope속성 중 하나"] >
    ...
</c:url>
```

### < c:redirect > 태그

지정된 URL 로 리다이렉트

response.sendRedirect() 기능과 동일

```jsp
<c:redirect url="redirect할 URL">
    ...
</c:redirect>
```

### < c:out > 태그

화면에 값을 출력해주는 태그

기본값 설정 기능 등을 제공하므로 표현 언어보다 편리함

```jsp
<c:out value="출력값" default="기본값" [escapeXml="boolean값"] />
```

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test03/member9.jsp)

> 회원가입 페이지에서 보낸 parameter 를 출력해주고 있음

## 14.7 Core 태그 라이브러리 실습

이 실습에서 중요한건 JSP 스크립트 요소를 이용했을 때와 비교해보는 것임

JSP 스크립트 요소들을 사용할 땐 JSP 의 HTML태그 중간중간에 `<% %>` 를 사용하여 자바 코드를 작성하여 가독성이 떨어졌지만 이 예제들의 경우엔 태그 형태로 기능을 구현하고 있기 때문에 가독성이 높고 웹 디자이너들에게 친화적이다.

[실습예제폴더](https://github.com/jjy3385/javaWeb/tree/main/pro14/WebContent/test04)

## 14.8 다국어 태그 라이브러리 사용하기

> 솔직히 그대로 따라하긴 했는데 좀 .. 노다가 같기도 하고 이해도 잘 안간듯

## 14.9 한글을 아스키 코드로 변환하기

다국어 기능을 사용하려면 미리 한글을 아스키 코드로 변환한 형태로 저장하고 있다가 요청 시 이 아스키 코드를 다시 한글로 변환해서 표시해야함

14.8과 14.9 정리는 생략

필요할 일이 있으면 다시 정리...

## 14.10 포매팅 태그 라이브러리 사용

원하는 형태로 숫자,날짜,문자열을 표시할 수 있게함

core 태그 라이브러리와 마찬가지로 `taglib` 디렉티브 태그를 추가해야함

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/fmt" %>
```

```jsp
사용예시
<fmt:formatDate value="${now}" pattern="YYYY-MM-dd" />
```

[실습1](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test05/formatTest.jsp)

## 14.11 문자열 처리 함수 사용

자바의 String 클래스의 메서드 기능과 비슷한 함수들을 JSTL에서 제공함

core 태그 라이브러리와 마찬가지로 `taglib` 디렉티브 태그를 추가해야함

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/functions" %>
```

[실습1](https://github.com/jjy3385/javaWeb/blob/main/pro14/WebContent/test05/fnTest.jsp)

## 14.12 표현 언어와 JSTL을 이용한 회원 관리

여기서도 중요한건 자바코드로 작성된 JSP와의 차이를 느껴보는 것임

[실습폴더](https://github.com/jjy3385/javaWeb/tree/main/pro14/WebContent/test06)



