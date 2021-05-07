# 예외처리

* 에러 - 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
* 예외 - 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

## 예외 클래스의 계층 구조

크게 두 그룹으로 나눌 수 있다

### Exception 클래스와 그 자손들
* 프로그래머의 실수로 발생하는 예외와 관련이 깊다
* ArrayIndexOutofBoundsException,NullPointerException,ClassCastException,ArithmeticException 등

### RuntimeException 클래스와 그 자손들
* 외부의 영향으로 발생할 수 있는 예외들로 사용자들의 동작과 관련이 깊다
* FileNotFoundException,ClassNotFoundException,DataFormatException 등

## 예외처리하기 -try-catch문

예외가 발생하면, 발생한 예외에 해당하는 클래스의 인스턴스가 만들어진다

try문에서 예외가 발생하면 catch블럭 중 발생한 예외와 일치하는 블럭이 있으면 해당 catch문이 수행된다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx3.java)

## 예외 발생시키기

1. 발생시키려는 예외 클래스의 인스턴스를 생성한다
2. 키워드 throw 를 이용해서 예외를 발생시킨다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx9.java)

### RuntimeException클래스들

* 컴파일러가 예외처리를 확인하지 않음
* unchecked예외라고 부름

### Exception클래스들

* 컴파일러가 예외처리를 확인함. 즉,예외처리를 하지 않으면 컴파일이 되지 않음
* checked예외라고 부름

## 메서드에 예외 선언하기

메서드의 선언부에 키워드 throws 를 사용하여 메서드에서 발생할 수 있는 예외를 적어준다

```java
void method() throws Exception1,Exception2, ... ExceptionN {
  //메서드 내용
}
```

메서드의 throws에 예외를 명시하는 것은 예외를 처리하는 것이 아니라 예외를 호출자에게로 떠넘기는 것이다

예외처리는 try-catch문에서 하고 throws는 예외를 호출자에게 떠 넘기는 것임

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx12.java)

예외가 발생한 메서드에서 예외처리를 하면 호출자는 그 메서드에서 예외가 발생했는지 알지 못한다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx15.java)

예외를 호출자로 넘겨서 처리하는 경우

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx16.java)

## finally 블럭

예외의 발생여부와 상관없이 항상 실행되어야할 코드를 넣는 블럭

try문에서 return을 하더라도 finally블럭의 문장은 정상적으로 수행됨

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/FinallyTest3.java)

## 자동 자원 반환 - try - with - resource 문

사용한 후 꼭 닫아줘야 하는 클래스들이 있는데 이런 것을 지원하기 위해 JDK1.7에 추가됨(C#의 using() 이랑 똑같음)

괄호() 안에 객체 생성하는 문장을 넣으면 이 객체에 대해서 따로 close()를 호출하지 않아도 try블럭을 벗어날 때 자동적으로 close()가 호출됨

이 기능을 사용할 수 있는 클래스는 AutoCloseable 인터페이스를 구현한 것이어야함

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/TryWithResourceEx.java)

## 예외 되던지기

예외를 처리한 후 인위적으로 다시 발생시켜서 호출자에게 던지는 처리방식

예외가 발생할 메서드에 try - catch 문을 써서 예외를 처리하는 동시에 메서드 선언부에 발생할 예외를 throws 키워드로 지정해줌

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ExceptionEx17.java)

## 연결된 예외(👽이부분은 제대로 이해 못한듯)

한 예외가 다른 예외를 발생시킬 수도 있음

### 사용하는 이유

1.여러가지 예외를 하나의 큰 분류의 예외로 묶어서 다루기 위해 사용
2.checked예외를 unchecked예외로 바꿀 수 있도록 하기 위해 ...❓

* Throwable initCause(Throwable cause) 지정한 에외를 원인 예외로 등록
* Throwable getCause() 원인 예외를 반환

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch8/ChainedExceptionEx.java)



