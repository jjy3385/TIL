# 16장.HTML5와 제이쿼리

## 16.1 HTML5 주요 개념

HTML5는 기존 HTML4에서 지원하지 않는 동영상이나 오디오 기능 그리고 지리 위치 정보 등을 지원한다. 플러그인을 따로 설치하지 않아도 화려한 그래픽 효과를 구현할 수 있으며 운영체제에 상관없이 스마트폰,태브릿 같은 모바일 환경에서도 기능을 구현할 수 있다.

문서 구조도 훨씬 심플해졌다

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>HTML5 구조</title>
    </head>
    <body>
        hello web!!
    </body>
</html>
```

## 16.2 HTML5 시맨틱 웹을 위한 구성 요소

HTML4에서는 웹 페이지 구조에 해당하는 머리말,메뉴,본문,하단부를 만들 때 < div > 태그에 CSS 적용하는 방식으로 작업했었지만 HTML5 에서는 의미 있는 구조를 나타낼  수 있는 태그들을 추가하여 가독성을 높였다.

![HTML5레이아웃](https://github.com/jjy3385/TIL/blob/main/%EC%9B%B9%EA%B0%9C%EB%B0%9C/%EC%9E%90%EB%B0%94%EC%9B%B9%EC%9D%84%EB%8B%A4%EB%A3%A8%EB%8A%94%EA%B8%B0%EC%88%A0/16%EC%9E%A5/image/html_layout.png)

## 16.3 제이쿼리 주요 개념

### 제이쿼리란?

화면의 동적 기능을 자바스크립트보다 좀 더 쉽고 편리하게 개발할 수 있게 해주는 자바스크립트 기반 라이브러리

* CSS 선택자를 사용해 각 HTML 태그에  접근해서 작업하므로 명료하고 읽기 쉽다
* 메서드 체인 방식으로 여러 동작이 한줄에 나열되어 코드가 반복되는 것을 피할 수 있다
* 풍부한 플러그인을 제공한다
* 브라우저 종류에 상관없이 동일하게 기능을 수행할 수 있다

사용방법은 라이브러리를 다운받아서 사용하거나 CDN 호스트를 설정해서 사용하는 방법이다

> #### CND 호스트?
>
> Content Delivery Network
>
> 전세계에 분산된 서버를 만들어갔고 사용자가 리소스를 다운받아서 사용할 수 있게   해주는 것이라고 한다
>
> 어쨋든 우리는 html5 문서에 아래 태그만 추가하면 제이쿼리를 사용할 수 있다.

```html
<script src="http://code.jquery.com/jquery-latest.min.js"></script>
```

## 16.4 제이쿼리의 여러 가지 기능

제이쿼리는 HTML 객체(DOM)를 탐색하는 방법으로 CSS 선택자를 이용한다

`$(" ")`

`" "` 사이에 #id, elementName, .className 등을 사용하면 됨

[실습1 - ID셀렉터](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test02/jQuery.html)

[실습2-CLASS셀렉터](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test02/jQuery3.html)

[실습3-엘리먼트 셀렉터](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test02/jQuery4.html)

> 엘리먼트 셀렉터는 해당 엘리먼트 여러 개를 선택하고 있음
>
> 마찬가지로 class셀렉터도 똑같이 어려 개를 선택할 수 있으며  ','를 사용하여 한꺼번에 여러 객체(DOM)를 선택할 수도 있음

## 16.5 제이쿼리 Ajax 기능

### Ajax?

Asynchronous Javascript + XML 를 의미한다

자바스크립트를 이용한 비동기 통신으로 클라이언트와 서버 간의 XML 이나 JSON 데이터를 주고받는 기술을 의미한다

> #### 비동기 통신?
>
> 예를 들어 메소드1,메소드2,메소드3이 연속적으로 수행된다고 하면 동기적으로 수행될 땐 
>
> * 메소드1 실행 => 메소드1 종료 => 메소드2 실행 => 메소드2 종료 => 메소드3 실행 => 메소드3 종료
>
> 이렇게 실행된 메소드가 종료된 후 다음 메소드가 실행되는 방식이 동기적이란 뜻임
>
> 반대로 비동기 통신은 앞에서 실행된 메소드의 종료 여부에 관계없이 다음 메소드가 실행되며 메소드 종료 응답이 들어오면 순서 상관없이 그때 그때 처리하는 방식이다.
>
> 비동기 통신을 활용하면 성능을 끌어올릴 수 있는데 프로그램이 느려지는 것은 대부분 IO 발생이라던가 외부의 네트워크에서 데이터를 끌어올 때 느려지는것인데 이 요청에 대한 응답을 기다리지 않고 다음 요청을 바로 수행하고 각 요청에 대한 응답이 올 때마다 처리를 하는 방식이다.



📌기존의 웹 페이지 동작 방식과의 가장 큰 차이점은 **페이지 이동이 발생하지 않는다**는 것이다

기존 웹 페이지 동작방식에서는 웹 서버가 요청을 받아서 HTML을 생성하여 결과페이지를 반환했다

반면에 Ajax 웹 페이지 동작 방식의 경우엔 클라이언트와 웹 서버 중간에 `XMLHttpRequest` 가 있으며 요청을 받은 웹서버는 XML 또는 JSON을 데이터를 생성하여 기존 요청한 페이지로 보내주면 요청한 페이지에서 바로 입력 결과를 보여줄 수 있다

> #### ❓XMLHttpRequest?
>
> 브라우저에서 제공하는 객체인데 지금은 Ajax 통신을 이 객체로 제어하고 있다는 정도만 알고 넘어간다

### Ajax사용하기

[ajax1.html](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test03/ajax1.html)

[AjaxText1.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec01/ex01/AjaxTest1.java)

### XML 주고받기

[ajax2.html](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test03/ajax2.html)

[AjaxTest2.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec01/ex01/AjaxTest2.java)

### ID 중복여부 확인 실습

[ajax4.html](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test04/ajax4.html)

[MemberServlet.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec02/ex01/MemberServlet.java)

[MemberDAO.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec02/ex01/MemberDAO.java)

html 에서 MemberServlet의 url매핑명으로 요청을 보내면 MemberServlet의 요청처리메서드(doXXX)가 수행되면서 MemberDAO를 호출하고 DAO에서 DB에 query를 보낸다

응답은 이 순서의 역순으로 html로 전달된다

 클라이언트 - 웹 서버 - DB 가 연결되는 과정이고 이게 핵심이라고 본다

## 16.6 제이쿼리에서 JSON 사용

XML보다는 JSON 이 좋다

1. name/value 쌍으로 이뤄져 있어 사람이 읽기 편하다
2. xml은 태그형식이라 태그 여닫기를 하면서 문자열이 많아져서 같은 양의 데이터를 주고 받는다고 할 때 json보다 용량이 클 수 밖에 없다

기본형 : `"name":"value"` 

객체 : `{}`객체는 중괄호에 둘러싸서 표현하며 `,`를 사용하여 여러 프로퍼티를 포함시킬 수 있음

배열 : `[]` 배열은 대괄호로 나타내며, 배열의 각 요소는 기본자료형/배열/객체 가능, 마찬가지로 `,`로 요소를 구별

### JSON 예시

```html
"members": [
	{"name":"마이클조던","age":"31","nickname":"그분"},
	{"name":"크리스폴","age":"36","nickname":"파궁사"}
]
```

> members란 이름을 가진 배열에 2개의 객체를 담음
>
> 객체는 name,age,nickname 이란 3개의 프로퍼티를 갖고 있음

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test05/json1.jsp)

[실습](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test05/json4.jsp)

### Ajax를 사용하여 서버와 JSON 데이터 주고받기

참고로 서버의 서블릿에서 JSON을 사용하려면 JSON 라이브러리를 깔아야됨

[https://code.google.com/archive/p/json-simple/downloads](https://code.google.com/archive/p/json-simple/downloads)

#### 클라이언트에서 보낸 Json 형식의 정보를 서버에서 처리해보기

[json5.jsp](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test05/json5.jsp)

[JsonServlet.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec03/ex01/jsonServlet.java)

#### 서버에서 보낸 json형식의 정보를 클라이언트에서 처리하기

[json6.jsp](https://github.com/jjy3385/javaWeb/blob/main/pro16/WebContent/test05/json6.jsp)

[JsonServlet2.java](https://github.com/jjy3385/javaWeb/blob/main/pro16/src/sec03/ex01/JsonServlet2.java)

> json 객체를 보낼 때 최종적으로는 하나의 Json객체를 보내기 때문에 JsonArray 객체를 JsonObject 객체에 담는것이다
>
> 

