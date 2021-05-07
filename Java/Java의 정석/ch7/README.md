# 객체지향 프로그래밍 2

## 상속

기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것

* 생성자와 초기화 블럭은 상속되지 않고 멤버만 상속된다
* 자손 클래스의 멤버변수는 조상 클래스의 멤버변수보다 항상 많거나 같다
* 형제 클래스 같은건 없다, 상하관계만 존재한다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/CaptionTvTest.java)

📌자손클래스의 인스턴스를 생성한다는 것은 조상클래스를 포함하고 있는 인스턴스를 생성한다는 뜻이다

### 상속관계와 포함관계
* 상속관계 : ~은 ~이다
* 포함관계 : ~은 ~을 가지고 있다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/DrawShape.java)

* Circle is a shape => 상속
* Circle has a point => 포함

### 단일 상속

자바는 다중 상속을 허용하지 않는다

즉, 자손클래스의 조상클래스가 여럿일 수 없다

다중상속을 허용할 경우, 클래스 간의 관계가 매우 복잡해진다. 상속받은 두 조상클래스에 같은 이름의 메소드나 변수가 있는 경우를 생각해볼 수 있다

## 오버라이딩 

자손클래스에서 조상클래스로부터 상속받은 메서드의 내용을 변경하는 것

메서드의 반환형/이름/매개변수가 모두 동일할 때, 즉 선언부가 동일한 경우임

### 오버라이딩의 조건
* 접근제어자 - 조상클래스의 메소드보다 좁은 범위로 변경할 수 없다
* 예외 - 조상클래스의 메소드보다 많은 수의 예외를 선언할 수 없다
* 인스턴스메서드를 static메서드로 변경하거나 그 반대로 변경할 수 없다

### 오버로딩과 오버라이딩

이름만 비슷할 뿐...

* 오버로딩 : 메서드명이 동일하고 매개변수가 다른 여러 메서드를 선언하는 것(new)
* 오버라이딩 : 자손클래스에서 조상클래스로부터 상속받은 메소드를 변경하는 것(modify)

### super 

자손클래스에서 조상클래스의 멤버 변수를 참조하고자 할 때 사용하는 참조변수

그냥 this랑 똑같은데 super는 조상클래스 멤버변수 접근할 때 사용함

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/SuperTest2.java)

```java
class Point {
  int x;
  int y;
  String getLocation() {
    return "x :" + x + ", y :" + y;
  }
}

class Point3D extends Point{
  int z;
  String getLocation() {
    //return "x :" + x + ", y :"+ y + ", z : " + z;  
    return super.getLocation() + ", z : " + z;  //조상메서드가 변경되는 경우에도 바로 반영됨
  }
}
```
### super() - 조상 클래스의 생성자

생성자의 첫 줄에서 조상클래스의 생성자를 호출해야함

그래야 조상클래스 멤버들의 초기화가 먼저 끝날 수 있기 때문이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/PointTest2.java)

## 패키지(package)

패키지는 클래스의 묶음이고 하나의 디렉토리이다

패키지명은 소문자로 하는 것을 원칙으로 한다

## 제어자(modifier)

### final

* final 클래스 : 변경할 수 없는 클래스 = 확장할 수 없는 클래스
* final 메서드 : 변경될 수 없는 메서드 = 오버라이딩할 수 없는 메서드
* final 멤버변수,지역변수 : 변경할 수 없는 변수 = 상수 

생성자를 이용한 final멤버 변수의 초기화

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/FinalCardTest.java)

### abstract - 추상의,미완성의

* abstract 클래스 : 클래스 내에 추상 메서드가 선언되어 있음을 의미
* abstract 메서드 : 선언부만 작성하고 구현부가 없는 추상 메서드

### 접근제어자

외부에서 접근하지 못하도록 제한하는 역할을 함 

접근 범위
|제어자|같은 클래스|같은 패키지|자손 클래스|전체|
--|--|--|--|--|
|public|O|O|O|O|
|protected|O|O|O|X|
|(default)|O|O|X|X|
|private|O|X|X|X|

### 캡슐화 

접근제어자를 통해 클래스 내부의 데이터를 보호한다

### 생성자의 접근제어자

생성자에 접근제어자를 사용하면 인스턴스 생성을 제한할 수 있다

new 생성자가 아닌 메서드를 호출함으로 인스턴스 생성을 제한 할 수 있게됨

또한 생성자가 private이면 다른 클래스의 조상이 될 수 없다

왜냐하면 자손클래스의 인스턴스를 생성할 때 조상클래스의 생성자도 호출해야되는게 그게 안되기 떄문

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/SingletonTest.java)


## 다형성(polymorphism)

자바에선 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있게 함으로써 다형성을 구현함

조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있게 함

하지만 반대로 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 순 없다

### 참조변수의 형변환

자손타입 -> 조상타입 : 업캐스팅,형변환 생략가능
조상타입 -> 자손타입 : 다운캐스팅,형변환 생략불가

>📌참조변수의 타입을 바꾸는거지 인스턴스 자체를 바꾸는게 아니다. 
>그래서인지 기본자료형의 형변환과는 좀 다른거 같다.

조상타입 -> 자손타입 형변환생략이 안되는 이유

📌조상타입의 참조변수를 자손타입의 참조변수로 형변환하는 것은 참조변수가 다룰 수 있는 멤버의 수가 늘어나는 효과가 있다

따라서 이 경우엔 형변환 생략할 수 없다

또한 참조변수의 형변환은 인스턴스에 아무런 영향을 주지 않는다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/CastingTest1.java)

### instanceof 연산자

어떤 타입에 대한 instanceof 연산이 true라는 뜻은 형변환이 가능하다는 뜻이다

조상 인스턴스의 참조변수를 자손타입으로 형변환할 수 없다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/InstanceofTest.java)

### 참조변수와 인스턴스의 연결

메서드의 경우엔 항상 실제 인스턴스 타입의 메서드를 호출하지만 멤버변수의 경우엔 참조변수의 타입에 따라 달라지낟

참조변수의 타입이 조상타입인 경우 조상타입의 멤버변수가 자손타입인 경우엔 자손타입의 멤버변수가 선택된다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/BindingTest.java)

### 매개변수의 다형성

매개변수가 조상타입이면 그 자손타입은 어떤 것이든 매개변수로 사용할 수 있다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/PolyArgumentTest.java)

이런 성질을 이용하면 배열이나 Vector클래스를 이용하여 여러 타입의 객체를 한꺼번에 다루는 것이 가능해진다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/PolyArgumentTest2.java)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/PolyArgumentTest3.java)

## 추상클래스(abstract class)

미완성 메서드를 포함하고 있는 클래스

추상클래스로는 인스턴스를 생성할 수 없지만 추상클래스를 상속받은 자손클래스에서 해당 메서드를 구현하면 인스턴스를 생성할 수 있음

클래스 구현을 도와주는 틀이라고 생각할 수 있음

조상으로부터 받은 모든 추상 메서드를 구현해야만 인스턴스를 생성할 수 있는 클래스가 되며 그렇지 않으면 이 클래스 역시 추상클래스가 됨

### 추상클래스(추상메서드)의 작성

>📌추상이란?
>어떤 개념에서 공통된 성질을 뽑아 일반적인 개념으로 파악하는 것
>즉 추상클래스를 작성하는 것은 기존 클래스의 공통부분을 뽑아내서 조상클래스를 만드는 것이라고 할 수 있음

```java
abstract 클래스명 {
  abstract 반환형 메서드명();
}
```

## 인터페이스

추상 메서드와 상수만을 멤버로 가질 수 있음

추상클래스보다 더 추상화정도가 높음

### 인터페이스의 작성

```java

interface 인터페이스이름 {
  public static final 타입 변수명 = 값;
  public abstract 반환형 메서드이름(매개변수목록);  
}
```

* 모든 상수는 public static final 이며 생략가능
* 모든 메서드는 public abstract 이며 생략가능

### 인터페이스의 상속과 구현

상속
* 인터페이스는 인터페이스로부터만 상속받을 수 있으며 다중상속도 가능

구현 
* 인터페이스 이름은 주로 ~able 로 짓는 경우가 많음, ~하는데 필요한 기능을 제공한다는 의미

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/FighterTest.java)

### 인터페이스와 다형성

인터페이스 역시 이를 구현한 클래스의 조상이므로 해당 인터페이스 타입의 참조변수로 이를 구현한 자손클래스를 참조할 수 있다

마찬가지로 매개변수의 타입으로도 사용할 수 있다

📌리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것을 의미한다(외워)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/ParserTest.java)

### 인터페이스의 장점

* 개발시간 단축
* 표준화
* 클래스들에게 관계를 맺어줄 수 있다
  * 서로 상속관계가 아닌 클래스들에게 같은 인터페이스를 구현하게 함으로써 관계를 맺어줄 수 있다
* 독립적인 프로그래밍이 가능하다
  * 클래스와 클래스 간의 직접적인 관계를 인터페이스를 이용하여 간접적인 관계로 변경하면 독립적인 프로그래밍이 가능하다...❓

### 인터페이스의 이해

인터페이스란 도대체 무엇인가??

* 클래스를 사용하는쪽(user)과 클래스를 제공하는 쪽(Provider)이 있다.
* 메서드를 사용하는 쪽(user)에서는 사용하려는 메서드(Provider)의 선언부만 알면 된다. 내용은 몰라도 된다...❓

[예제1](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/InterfaceTest.java)

클래스 A 에서 클래스 B를 직접 매개변수로 받음

[예제2](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch7/InterfaceTest2.java)

클래스 A에서 인터페이스 I 를 매개변수로 받지만 I를 구현한 B를 매개변수로 받아 메서드를 실행할 수 있음

인터페이스가 껍데기 역할을 해주고 클래스 A는 그 안에 어떤 클래스가 들어있는지 몰라도 상관이 없다

### 디폴트 메서드

인터페이스에 추가하는 추상메서드가 아닌 메서드

일단은 참고적으로만 알고 있어도 될듯





