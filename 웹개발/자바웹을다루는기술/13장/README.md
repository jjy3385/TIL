# 13장.자바 코드를 없애는 액션 태그

앞장까지 JSP의 스크립트 요소를 통해 자바코드를 작성하는 것을 배웠다

하지만 화면이 복잡해지면 자바코드와 HTML 태그가 뒤섞여 작업이 힘들어진다

액션 태그는 JSP에서 스크립트 요소를 없앨 수 있게 해준다

## 13.1 인클루드 액션 태그 사용하기

### 인클루드 액션 태그 형식

```jsp
<jsp:include page="jsp페이지" flush="true/false">
    ...
</jsp:include>
```

> ❓flush 는 지정한 JSP를 실행하기 전 출력 버퍼 비움 여부를 지정하는 것이다
>
> 일반적으로 false로 지정한다고 하는데 정확하게 어떤 건지는 아직 잘 모르겠음

### 특징

인클루드 디렉티브 태그처럼 화면을 분할해서 관리할 때 사용한다

📌인클루드 디렉티브 태그와의 가장 큰 차이점은 **동적 처리가 가능하다는 것**이다

>  인클루드 디렉티브 태그는 컨테이너가 jsp파일을 .java로 변환할 때 하나의 .java 파일로 변환하지만 **인클루드 액션 태그는 jsp파일마다 .java파일이 생성**됨

![screen shot 2021-06-08 212927](D:\GitRepository\TIL\웹개발\자바웹을다루는기술\13장\image\screen shot 2021-06-08 212927.png)

.java 파일의 소스에서 include() 메서드로 포함시킨 jsp로 request와 response를 넘기는 것을 확인할 수 있다.즉 jsp request에 매개변수를 바인딩하여 자식jsp로 전달하고 있다

```java
org.apache.jasper.runtime.JspRuntimeLibrary.include(request, response, "duke_image.jsp")
```

실행시마다 JSP를 재변환하고 있기 때문에 부모jsp에서 자식 jsp로 매개변수를 다르게 전달하는 방식으로 동적 처리가 가능하다.

[예제1](https://github.com/jjy3385/javaWeb/blob/main/pro13/WebContent/include1.jsp)

[예제2](https://github.com/jjy3385/javaWeb/blob/main/pro13/WebContent/include2.jsp)

[포함된JSP](https://github.com/jjy3385/javaWeb/blob/main/pro13/WebContent/duke_image.jsp)

위의 예제를 보면 예제1에서는 인클루드 액션 태그 매개변수를 아래와 같이 보내준다

```jsp
	<jsp:include page="duke_image.jsp" flush="true">
		<jsp:param name="name" value="주영" />
		<jsp:param name="imgName" value="duke.png" />
	</jsp:include>
```

예제2는 다음과 같다

```jsp
	<jsp:include page="duke_image.jsp" flush="true">
		<jsp:param name="name" value="주영2" />
		<jsp:param name="imgName" value="duke2.png" />
	</jsp:include>
```

둘다 똑같은 duke_image.jsp를 인클루드 했지만 서로 다른 매개변수를 보냈기 때문에 둘은 서로 다른 이미지를 보여준다.

## 13.2 포워드 액션 태그 사용하기

서블릿에서 다른 서블릿으로 포워딩할 때 사용했던 클래스는 `RequestDispatcher` 다

포워드 액션 태그 형식

```jsp
<jsp:forward page="포워딩할 JSP 페이지">
    ...
</jsp:forward>
```

[예제](https://github.com/jjy3385/javaWeb/blob/main/pro13/WebContent/result.jsp)

## 13.3 useBean,setProperty,getProperty 액션 태그 사용하기

### 자바 빈 

DTO(Data Transfer Object ,데이터 전송 객체) 클래스, VO(Value Object,값 객체) 클래스와 같은 개념

자바 빈을 만드는 방법

* 속성의 접근 제어자는 private
* 각 속성은 각각의 setter/getter를 가짐
* setter/getter 이름의 첫글자는 반드시 소문자
* 인자 없는 생성자를 반드시 가지며 다른 생성자 추가 가능

### 유즈빈 액션 태그

JSP페이지에서 자바 빈을 대체하기 위한 태그

```jsp
<jsp:useBean id="빈 이름" class="패키지 이름 포함 자바 빈 클래스" [scope]="접근범위"]/>
```

 id에는 객체명,class는 클래스명

접근 범위는 `page`,`request`,`session`,`application` 이렇게 네가지가 있으며 `page` 가 기본값임

### setProperty/getProperty 액션 태그

setter/getter 를 대체하는 액션 태그

```jsp
<jsp:setProperty name="빈 이름" property="속성 이름" value="값" />
<jsp:getProperty name="빈 이름" property="속성 이름" />
```

[예제](https://github.com/jjy3385/javaWeb/blob/main/pro13/WebContent/member.jsp)

