# 8장.서블릿 확장 API 사용하기

## 8.1 서블릿 포워드 기능 사용하기

### 포워드 기능

서블릿에서 다른 서블릿이나 JSP로 요청을 전달하는 기능

이 요청(request)을 전달할 때 추가 데이터를 포함시켜서 전달하는 것도 가능함

## 8.2 서블릿의 여러 가지 포워드

| redirect 방법                                                | Refresh 방법                                                 | location 방법                                                | dispatch 방법                                                |
| ------------------------------------------------------------ | :----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `HttpServletResponse` 객체의 sendRedirect() 메서드 사용      | `HttpServletResponse` 객체의 <br />addHeader() 메서드 사용   | 자바스크립 location 객체의 href 속성을 이용                  | `RequestDispatcher` 객체의 <br />forword() 메서드 사용       |
| 웹 브라우저에 재요청하는 방식                                | 웹 브라우저에 재요청하는 방식                                | 자바스크립트에서 재요청하는 방식(어쨋든 웹 브라우저에서 재요청하는건 똑같음) | 서블릿이 직접 요청하는 방식<br />(웹 브라우저로 가지 않고 서블릿에서 서블릿으로 직접 요청 ) |
| `HttpServletResponse<br />.sendRedirect("포워드할 서블릿 또는 JSP") ;` | `HttpServletResponse<br />.addHeader("Refresh",경과시간(초);url=요청할 서블릿 또는 JSP);` | `location.href='요청할 서블릿 또는 JSP';`                    | `RequestDispatcher dis = <br />request.getRequestDispatcher("포워드할 서블릿 또는 JSP");` |

[redirect 실습](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec01/ex01/FirstServlet.java)

[Refresh 실습](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec01/ex02/FirstServlet.java)

[location 실습](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec01/ex03/FirstServlet.java)

:pushpin: 세 방식 모두 웹 브라우저를 거쳐서 요청을 수행함

1. 클라이언트의 웹 브라우저에서 첫번째 서블릿에 요청을 보냄
2. 첫 번째 서블릿은 두번째 서블릿을 요청하라는 내용을 붙여서 웹 브라우저로 응답함
3. 응답을 받은 웹 브라우저가 두번째 서블릿을 다시 요청함

### redirect 방식으로 다른 서블릿에 데이터 전달

GET방식을 이용해 이름/값 쌍으로 데이터를 전달할 수 있음

`response.sendRedirect("second?name=jin")`

[redirect 데이터 전달 실습](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec02/ex01/FirstServlet.java)

## 8.3 dispatch를 이용한 포워드

:pushpin:클라이언트의 웹 브라우저를 거치지 않고 바로 서버에서 포워딩이 진행됨

1. 클라이언트의 웹 브라우저에서 첫 번쨰 서블릿에 요청을 보냄
2. 첫 번째 서블릿이 두번째 서블릿으로 포워드함

> 포워딩을 하는 경우 웹 브라우저의 주소창이 바뀌지 않음
>
> 클라이언트 사이드에서는 서버에서 포워딩이 이뤄졌는지 알 수 없음

[dispatch 실습](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec03/ex01/FirstServlet.java)

## 8.4 바인딩

포워딩 시 데이터의 양이 적을 땐 GET방식을 이용하여 데이터를 전달하는게 편함

하지만 대량의 데이터를 주고 받기엔 GET방식은 불편하므로 **바인딩(binding)**기능을 사용함

주로 `HttpServletRequest`,`HttpSession`,`ServletContext` 객체에 객체를 저장함

### 바인딩 관련 메서드

| 메서드                               | 기능                                     |
| ------------------------------------ | ---------------------------------------- |
| setAttribute(String name,Object obj) | 데이터를 각 객체에 바인딩함              |
| getAttribute(String name)            | 객체에 바인딩된 데이터를 name으로 가져옴 |
| removeAttribute(String name)         | 객체에 바인딩된 데이터를 name으로 제거   |

### HttpServletRequest를 이용한 redirect 포워딩 시 바인딩

요청(request)에 데이터를 바인딩하여도 두 번째 서블릿에서는 해당 데이터를 확인할 수 없음

왜냐하면 redirect포워딩 시  첫번째 요청에 바인딩한 데이터는 클라이언트로 보내지고 새로 생성된 두번째 요청이 두번째 서블릿으로 들어오기 때문임

[redirect 포워딩 시 바인딩 실습 - FirstServlet](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec04/ex01/FirstServlet.java)

[redirect 포워딩 시 바인딩 실습 - SecondServlet](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec04/ex01/SecondServlet.java)

그러므로 두번째 서블릿에서 바인딩된 데이터를 사용하기 위해선 웹브라우저가 재요청하는 방식이 아닌 직접 서블릿에서 서블릿으로 요청하는 방식을 사용해야함

:pushpin:dispatch 포워딩을 사용해야함

### HttpServletRequest를 이용한 dispatch 포워딩 시 바인딩

[dispatch 포워딩 시 바인딩 실습 - FirstServlet](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec04/ex02/FirstServlet.java)

[dispatch 포워딩 시 바인딩 실습 - SecondServlet](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec04/ex02/SecondServlet.java)

### 실습 - 두 서블릿 간 회원 정보 조회

[소스경로](https://github.com/jjy3385/javaWeb/tree/main/pro08/src/sec04/ex03)

#### 🚩트러블 슈팅

회원가입 시 405 에러가 발생함

GET/POST 메서드 방식 제대로 못했을 때 나오는 오류

원인 : 저장은 POST방식으로 진행되는데 그 직후 조회기능을 수행하는  `ViewMembers` 서블릿에는 doGet()메서드만 작성해놨음

해결 : `ViewMembers` 서블릿에 doGet() , doPost() 를 모두 만들고 doHandle() 을 호출하도록 수정하여 해결

## 8.5 ServletContext 와 ServletConfig

### ServletContext 클래스

톰캣 컨테이너가  실행될 때 각 컨텍스트(애플리케이션)마다 한 개의 `ServletContext` 객체가 생성됨

마찬가지로 톰캣 컨테이너가 종료되면 `ServletContext` 객체도 소멸됨

애플리케이션 전체의 공통 자원이나 정보를 미리 `ServletContext` 객체에 바인딩하여 서블릿들이 공유할 수 있음

`ServletContext` 가 제공하는 기능

- 서블릿에서 파일 접근 기능
- 자원 바인딩 기능
- 로그 파일 기능
- 컨텍스트에서 제공하는 설정 정보 제공 기능

> 참고로 `ServletConfig` 는 각 서블릿마다 하나씩 생성됨

### ServletContext 바인딩 기능

각 서블릿에서 `ServletContext` 객체를 받아올 때 `init()` 메서드의 유무에 따라 용법이 조금 달라질 수 있음

- `init()` 이 있을 때 : `init()` 의 매개변수 `ServletConfig` 객체에서 `getServletContext()` 를 호출하여 객체를 받음
- `init()` 이 없을 때 :  다른 메서드(`doXXX()`)에서 그냥`getServletContext()` 호출(this인듯)

[실습 소스확인](https://github.com/jjy3385/javaWeb/tree/main/pro08/src/sec05/ex01)

### ServletContext 매개변수 설정 기능

`web.xml` 파일에 `<context-param>` 태그 안에 `<param-name>` 태그와 `<param-value>` 태그를 이용해 매개변수를 설정할 수 있음

`ServletContext객체.getInitParameter("매개변수 이름");` 으로 접근할 수 있음

[실습 소스확인](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec05/ex02/ContextParamServlet.java)

### ServletContext 의 파일 입출력 기능

파일에서 데이터를 읽어올 수 있음

`ServletContext객체.getResourceAsStream("경로")`

[실습 소스 확인](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec05/ex03/ContextFileServlet.java)

### ServletConfig

각 `Servlet` 객체에 대해 생성되며 각 서블릿에서만 접근할 수 있고 `ServletContext`처럼 공유할 수 없음

`ServletConfig`제공기능

- `ServletContext` 객체를 얻는 기능
- 서블릿에 대한 초기화 작업 기능

초기화 방법은 `@WebServlet` 애너테이션을 이용하는 방법과 `web.xml`에서 설정하는 방법 두가지가 있음

### @WebServlet 애너테이션을 이용한 서블릿 설정

@WebServlet 구성요소

- urlPatterns : 웹 브라우저에서 서블릿 요청 시 사용하는 매핑 이름
- name : 서블릿 이름
- loadOnStartup : 컨테이너 실행 시 서블릿이 로드되는 순서 지정
- initParams : @WebInitParam 애너테이션을 이용해 매개변수를 추가하는 기능
- desription : 설명

이클립스에서 서블릿 생성 시 간단하게 설정할 수도 있음

[실습 소스확인](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec06/ex01/InitParamServlet.java)

> web.xml에 설정하는 방법은 따로 실습하지 않음
>
> 지금은 잘 사용하지 않는다고 함
>
> 책 300p 참고

## 8.6 load-on-startup 기능 사용하기

서블릿은 웹 브라우저에서 최초로 요청했을 때 `init()` 을 수행하여 메모리에 로드됨

 load-on-startup 을 사용하면 톰캣 컨테이너가 실행되면서 미리 서블릿을 실행되면서 메모리에 로드되게 할 수 있음

사용자의 최초 요청이 있을 때 메모리에 로드해놓는 것 보다 미리 로드해 놓는게 당연히 좋음

`@WebServlet` 애너테이션을 이용하는 방법과 `web.xml`에서 설정하는 방법 두가지가 있음

[실습 소스확인](https://github.com/jjy3385/javaWeb/blob/main/pro08/src/sec06/ex02/LoadAppConfig.java)

:pushpin:애플리케이션에서 항상 가장 느린건 IO가 발생할 때임

즉, 파일을 읽어들이는 작업을 최소화해야함

위의 예제에서는 load-on-startup 우선순위가 1로 지정된 서블릿의  `init()` 메서드에서 `ServletContext객체.getInitParameter("매개변수명")` 를 수행한다

이렇게 하면 최초 톰캣 컨테이너 실행 시 서블릿이 메모리에 로드되고 그 때 web.xml 파일의 매개변수를 읽어들여놓고 `ServletContext` 에 데이터를 바인딩 해놓기 때문에 추후에 해당 데이터를 접근할 땐 따로 파일을 읽어들일 필요가 없게됨

간단한 내용이지만 이런것들을 고려하여 메모리 효율과 성능에 좋은 웹 애플리케이션을 구성할 수 있음



