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




