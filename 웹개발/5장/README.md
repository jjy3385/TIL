# 5.서블릿 이해하기

## 5-1.서블릿이란?

클라이언트의 요청에 따라 동적 서비스를 제공하는 자바 클래스

### 특징

서버쪽에서 실행되며 그렇기 때문에 보안 기능을 적용하기에 유리함

쓰레드 방식으로 실행됨

정적 웹 프로그래밍의 문제점을 보완하는 동적 기능을 제공함

## 5-2.서블릿 API 계층 구조와 기능

### 서블릿 클래스 계층 구조

- Servlet 인터페이스,ServletConfig 인터페이스
  - GenericServlet 추상클래스
    - HttpServlet 클래스

GenericServlet : 

Servlet인터페이스와 ServletConfig 인터페이스를 구현하여 일반적인 서블릿 기능을 구현한 클래스

HttpServlet : 

GernericServlet을 상속받아 Http프로토콜을 사용하는 웹 브라우저에서 서블릿 기능을 수행하는 클래스

클라이언트 요청 => public service() 호출 => protected service() 호출 => doXXX() 호출

## 5-3.서블릿의 생명 주기 메서드

### 서블릿 생명주기 메서드

서블릿 실행단계마다 호출되어 기능을 수행하는 콜백 메서드

(브라우저가 요청하면 자동으로 호출되는 메서드)

| 생명 주기 단계 | 호출 메서드      | 기능                                                         |
| -------------- | ---------------- | ------------------------------------------------------------ |
| 초기화         | init()           | 서블릿 요청 시 맨 처음 한번만 수행<br />서블릿 초기화 작업을 수행 |
| 작업수행       | doGet(),doPost() | 서블릿 요청 시 매번 수행<br />실제 클라이언트가 요청한 작업을 수행 |
| 종료           | destroy()        | 메모리에서 소멸될 때 호출                                    |

init(), destroy()는 생략가능 doGet(),doPost()는 생략불가

## 5-4.FirstServlet 실습

### 서블릿 매핑

작성한 서블릿 호출 시 `http://주소:포트번호/프로젝트명/패키지명이 포함된 클래스명` 로 접속해야함

> 클래스명을 직접 쓰면 불편하고 보안상 좋지 않음
>
> 따라서 서블릿 클래스에 대응하는 서블릿 매핑 이름을 설정하는게 더 좋음

서블릿 매핑 설정 시 `http://주소:포트번호/프로젝트명/서블릿매핑이름` 으로 접속 가능

#### 서블릿 매핑 방법

- 각 프로젝트의 web.xml 에서 설정
- <servlet> 태그와 <servlet-mapping> 태그를 이용

[web.xml 작성 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro5/WebContent/WEB-INF/web.xml)

[FirstServlet 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro5/src/main/java/sec01/ex01/FirstServlet.java)



## 5-5.서블릿 동작 과정

쓰레드로 기능을 수행함

브라우저에서 최초 요청 시 한번 만 init() 메서드가 수행되며 재 요청 시 doXXX() 메서드만 수행됨

즉, 서블릿을 한번만 메모리에 로드하고 그 다음 요청부터는 재사용함

[SecondServlet 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro5/src/main/java/sec01/ex01/SecondServlet.java)

## 5-6.애너테이션을 이용한 서블릿 매핑

web.xml 에 여러 서블릿 매핑 설정을 하게 되면 유지관리하기 힘들어짐

그렇기 때문에 애너테이션을 이용하여 가독성을 올리는 방법을 선택하는게 더 좋음

@WebServlet(서블릿매핑이름) 을 이용

[ThirdServlet 예제](https://github.com/jjy3385/gilbutJavaWeb/blob/main/pro5/src/main/java/sec01/ex01/ThirdServlet.java)



