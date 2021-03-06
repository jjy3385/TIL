# 7장.서블릿 비즈니스 로직 처리



## 7.1 서블릿의 비즈니스 로직 처리 방법

서블릿의 비즈니스 처리 작업이란 서블릿이 클라이언트로부터 요청을 받으면 그 요청에 대해 작업을 수행하는 것을 의미함

웹 프로그램에서 대부분의 비즈니스 처리 작업은 데이터베이스 연동관련 작업이지만 그 외 다른 서버와 연동해서 데이터를 얻는 작업도 수행함

## 7.2 서블릿의 데이터베이스 연동

JDBC , DAO ,VO 등을 알아야함

### JDBC(Java Database Connectivity)

자바 애플리케이션에서 DBMS 의 종류에 상관없이 표준화된 방법으로 모든 DBMS에 쉽게 접근할 수 있도록 구성한 API

모든 DBMS는 그 특징과 구조가 모두 다르기 때문에 자바 애플리케이션에서 DBMS로 접근하는 방식이 각각 다름

JDBC가 있으면 자바 애플리케이션 개발자는 모든 DBMS에 표준화된 방법으로 접근할 수 있음

>  DMBS드라이버를 자바에서 인터페이스와 클래스를 미리 정의하고 실제 구현은 각 DBMS 개발사에서 진행함

여하튼 오라클은 ojdbc6.jar 라이브러리를 웹 애플리케이션 /WEB-INF/lib에 추가해야됨

### DAO 와 VO 클래스

#### DAO(Data Access Object)

자바 애플리케이션에서 데이터베이스 작업만 수행하는 클래스

#### VO(value Object)

데이터를 다른 클래스로 전달할 때 사용

TO(Transfer Object)라고도 부름

테이블의 필드를 멤버변수로 사용하며 멤버변수,생성자, getter/setter 로 구성됨

### 회원정보 조회 과정

1. 웹 브라우저가 서블릿에 회원 정보를 요청
2. 서블릿은 요청을 받은 후 DAO 객체를 생성하여 회원정보를 조회하는 메서드 호출
3. 회원정보를 조회하는 메서드에서 데이터베이스와 연결한 후 SQL문을 실행하여 회원 정보를 조회
4. 조회된 회원 정보를 List<VO> 에 담아서 서블릿으로 전달
5. 서블릿에서 전달받은 VO를 반복문을 활용하여  HTML 태그 문자열로 만듬
6. HTML 태그를 받은 웹 브라우저가 회원 정보를 출력

### PreparedStatement

Statement 클래스를 이용하여 데이터베이스와 연동할 경우엔 연동 할 때마다 SQL문을 다시 컴파일해서 속도가 느림

PreparedStatement 는 한번 컴파일된 SQL문은 재사용하므로 빠름

또한 SQL문에 "?" 를 넣어 손쉽게 값을 설정할 수 있음

## 7.3 DataSource 이용하여 데이터베이스 연동

### 커넥션풀의 등장배경

[MemberDAO 예제](https://github.com/jjy3385/javaWeb/blob/main/pro07/src/sec01/ex01/MemberDAO.java)

```java
Class.forName(driver);
System.out.println("Oracle 드라이버 로딩 성공");
con = DriverManager.getConnection(url, user, pwd);
```

위의 데이터베이스 연동 방식은 웹 애플리케이션이 필요할 때마다 데이터베이스에 연결하는 방식임

데이터베이스를 연결하는 과정이 시간이 많이 걸리기 때문에 **커넥션풀** 기술이 등장함

커넥션풀이란 웹 애플리케이션이 실행됨과 동시에 연동할 데이터베이스와 미리 연결하고 그 상태를 유지하는 기술

### 커넥션풀 동작과정

1. 톰캣 컨테이너 실행 시 ConnectionPool 객체 생성
2. 생성된 커넥션 객체가 DBMS와 연결
3. 데이터베이스와 연동 작업이 필요할 경우 응용 프로그램은 커넥션풀에서 제공하는 메서드를 호출

🚩톰캣 실행 시 톰캣 설정 파일에 설정된 데이터베이스 정보를 이용하여 미리 데이터베이스에 연결함

### JNDI(Java Naming and Directory Interface)

필요한 자원을 키/값 쌍으로 저장한 후 필요할 때 키를 이용해 값을 얻는 방법

톰캣 컨테이너가 ConnectionPool 객체를 생성하면 이 객체에 대한 JNDI 이름을 미리 설정해 놓음

그러면 데이터베이스 연동 시 그 이름으로 접근하여 작업함

### 톰캣의 DataSource 설정 및 사용 방법

1. jdbc 드라이버를 /WEB-INF/lib 폴더에 설치

2. ConnectionPool 기능 jar 파일을 /WEB-INF/lib 폴더에 설치

   [lib폴더](https://github.com/jjy3385/javaWeb/tree/main/pro07/WebContent/WEB-INF/lib)

3. CATALINA_HOME/context.xml 에 Connection 객체 생성 시 연결할 데이터베이스 정보를 JNDI로 설정

   [context.xml](https://github.com/jjy3385/javaWeb/blob/main/Servers/Tomcat%20v9.0%20Server%20at%20localhost-config/context.xml)

4. DAO클래스에서 데이터베이스 연동 시 미리 설정한 JNDI 이름으로 데이터베이스 연결 작업 수행

   [memberDAO](https://github.com/jjy3385/javaWeb/blob/main/pro07/src/sec02/ex01/MemberDAO.java)



