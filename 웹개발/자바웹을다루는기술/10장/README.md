

# 10장.서블릿 필터와 리스너

## 10.1 서블릿 속성과 스코프

### 서블릿 속성(attribute)

`ServletContext`,`HttpSession`,`HttpServletRequest` 이 세가지 서블릿 API 클래스에 저장되는 객체(정보)

### 서블릿 스코프(scope)

서블릿 API 에 바인딩된 속성에 대한 접근 범위

| 스코프 종류         | 해당 서블릿 API    | 속성의 스코프                                |
| ------------------- | ------------------ | -------------------------------------------- |
| 애플리케이션 스코프 | ServletContext     | 속성은 애플리케이션 전체에서 접근 가능       |
| 세션 스코프         | HttpSession        | 속성은 브라우저에서만 접근 가능              |
| 리퀘스트 스코프     | HttpServletRequest | 속성은 해당 요청/응답 사이클에서만 접근 가능 |

[예제코드](https://github.com/jjy3385/javaWeb/blob/main/pro10/src/sec01/ex01)

## 10.2 서블릿의 여러가지 URL 패턴

### URL 패턴이란?

서블릿 매핑 시 사용되는 가상의 이름으로 반드시 /(슬래시) 로 시작되어야함

세 가지 종류가 있음

1. 정확히 이름까지 일치
2. 디렉터리까지만 일치
3. 확장자만 일치

``` java
@WebServlet("/first/test") //1.정확히 이름까지 일치
@WebServlet("/first/*") //2.디렉터리까지만 일치
@WebServlet("/*.do") //3.확장자만 일치
```

[예제코드](https://github.com/jjy3385/javaWeb/tree/main/pro10/src/sec02/ex01)

> /first/base.do 로 요청하면 `2.디렉터리까지만 일치` 와 `3.확장자만 일치` 둘 다 만족하는데 이땐 2가 우선순위가 높음

## 10.3 Filter API

### 필터란?

클라이언트에서 서블릿으로 요청하거나 응답할 때 중간에서 미리 요청과 응답 관련 처리를 하는 기능

한글 인코딩 같은 작업을 서블릿마다 할 것 없이 필터에서 수행하면 좀 더 편함

`클라이언트 <-> 필터 <-> 서블릿 `

[예제코드](https://github.com/jjy3385/javaWeb/blob/main/pro10/src/sec03/ex01/EncoderFilter.java)

`Filter ` 를 구현하는 사용자정의 filter 클래스를 작성함

서블릿과 마찬가지로 `@WebFilter("/매핑주소")`로 매핑되며 `doFilter()` 메서드를 구현함

> @WebFilter("/*") 로 하면 모든 요청에 대해 필터가 기능을 수행하도록 할 수 있음

#### 응답 필터

요청과 응답에 대한 필터 기능은 동일한 필터에서 수행함

```java
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		System.out.println("doFilter 호출");
		request.setCharacterEncoding("utf-8");
		String context = ((HttpServletRequest) request).getContextPath();
		String pathinfo = ((HttpServletRequest) request).getRequestURI();
		String realPath = request.getRealPath(pathinfo);
		String mesg = " Context  정보:" + context + "\n URI 정보 : " + pathinfo + "\n 물리적 경로:  " + realPath;
		System.out.println(mesg);

		long begin = System.currentTimeMillis();
		chain.doFilter(request, response);
		long end = System.currentTimeMillis();
		System.out.println("작업 시간:" + (end - begin) + "ms");
```

`chain.doFilter()`기준 위쪽 코드는 요청에 대한 필터 기능

아래쪽 기능은 응답에 대한 필터 기능임

그러니까 `doFilter()` 메서드 호출 시 서블릿으로 요청과 응답을 넘기고 서블릿에서 요청을 처리하고 응답을 작성하여 이 메서드로 반환되는 것임

## 10.4 여러가지 서블릿 관련 Listener API

### Listener API

서블릿에서 발생하는 이벤트에 대한 적절한 처리를 해주는 여러 가지 기능

### HttpSessionBindingListener

1. 이벤트 핸들러를 생성한 후 세션에 저장
2. 세션에 바인딩 시 `HttpSessionBindingListener` 클래스 객체의 `valueBound()` 메서드 호출

[예제코드](https://github.com/jjy3385/javaWeb/tree/main/pro10/src/sec04/ex01)

### HttpSessionListener

`HttpSessionBindingListener` 와 다르게 `@WebListener` 애너테이션을 꼭 `HttpSessionListener` 인터페이스를 구현하는 클래스 위에 써줘야함

[예제코드](https://github.com/jjy3385/javaWeb/tree/main/pro10/src/sec04/ex02)

