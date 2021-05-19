

# 지네릭스,열거형,애너테이션

## 1.지네릭스(Generics)

다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입체크를 해주는 기능이다.

### 지네릭스의 장점

1. 타입 안정성 제공
2. 타입체크와 형변환을 생략할 수 있다

### 지네릭스 클래스 선언

```java
class Box<T>{
    T item;
    void setItem(T item){
        this.item = item;
    }
    T getItem(){
        return item;
    }
}
```

T를 '타입 변수'라고 한다 

T말고 E나 K,V 등 다양하게 쓸 수 있다

모두 '임의의 참조형 타입'이란 뜻이다

### 지네릭스 용어

- Box<T> : 지네릭 클래스, T의 BOX  또는 T BOX라 읽음
- T : 타입 변수 또는 타입 매개변수
- Box : 원시 타입

타입 변수에 타입을 지정하는 것을 '지네릭 타입 호출'이라고 함

`Box<String> b = new Box<String>` 이 코드에서 `String`은  '대입된 타입', `Box<String>`은 '지네릭 타입 호출'

### 지네릭스 제한

객체별로 다른 타입을 지정하는 것은 적절함

```java
Box<Apple> appleBox = new Box<Apple>();	//OK 
Box<Grape> grapeBox = new BOX<Grape>();	//OK
```

>  Box에 다양한 타입을 담을 수 있지만 대입된 타입에 따라 appleBox엔 Apple만, grapeBox엔 grape만 담을 수 있다
>
> 그렇지 않으면 컴파일 오류 발생함

#### 📌1. 모든 객체에 대해 동일하게 동작해야 하는 static멤버에 타입 변수 T를 사용할 수 없음

​		왜냐하면 static멤버는 대입된 타입에 상관없이 동일해야되기 때문이다

​		인스턴스마다 다양한 타입이 대입될 수 있기 때문에 T는 인스턴스변수로 간주된다

 		static멤버에서 인스턴스멤버를 참조할 수 없으므로 static멤버는 T를 참조할 수 없다

2. #### new연산자

   `T[] arr = new T[10]` 

   오류남, new연산자는 컴파일 시점에 타입 T가 뭔지 정확히 알아야함

   똑같은 이유로 instanceof연산자도 T를 피연산자로 사용할 수 없음

### 지네릭 클래스의 객체 생성과 사용

* 참조변수와 생성자에 대입된 타입이 일치해야한다

  ```java
  Box<Apple> appleBox = new Box<Apple>(); //OK
  Box<Apple> appleBox = new Box<Grape>();	//에러
  //Apple이 Fruit의 자손이여도 마찬가지다
  Box<Fruit> appleBox = new Box<Apple>(); //에러
  ```

- 두 '지네릭 클래스의 타입'이 상속관계에 있고 대입된 타입이 같은 경우는 괜찮다

  ```java
  //FruitBox는 Box의 자손
  Box<Apple> apple = new FruitBox<Apple>();	//OK
  ```

- 추정이 가능한 경우 생략(JDK1.7부터)

  ```java
  Box<Apple> appleBox = new Box<>(); //OK, 참조변수를 보면 Box엔 Apple타입의 객체만 저장가능하다는 것을 알 수 있기 때문에 생성자에서 생략 가능
  ```

- `void add(T item)`할 때 대입된 타입과 다른 객체 추가 불가능, 단 자손들은 메서드의 매개변수로 사용 가능

  ```java
  //Apple이 Fruit의 자손이다
  Box<Fruit> fruitBox = new Box<Fruit>();
  fruitBox.add(new Fruit());		//OK
  fruitBox.add(new Apple());		//OK
  ```

  [예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/FruitBoxEx1.java)

### 제한된 지네릭 클래스

타입 문자로 사용할 타입을 명시하면 한 종류의 타입만 저장할 수 있도록 제한할 수 있지만, 여전히 모든 종류의 타입을 지정할 수 있다는 것에 변함은 없다

```java
FruitBox<Toy> fruitBox = new FruitBox<Toy>();
fruitBox.add(new Toy());	//Toy타입만 저장할 수 있지만 FruitBox는 이름으로 보아 Fruit타입과 그 자손을 저장하려고 만든 타입으로 보인다.
```

지네릭 타입에 'extends' 를 사용하면 특정 타입의 자손들만 대입할 수 있도록 제한할 수 있다

`class FruitBox<T extends Fruit>` Fruit타입과 그 자손 타입만 저장가능

인터페이스라도 'extends'를 사용한다

```java
class FruitBox<T extends Fruit & Eatable>{	//Fruit의 자손이면서 Eatable인터페이스도 구현한 타입 변수만로 제한하는 경우
    ...
}
```

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/FruitBoxEx2.java)

### 와일드 카드

지네릭 타입이 다른 것만으로는 오버로딩할 수 없다는 문제점을 해결하기 위해 나옴

```java
static Juice makeJuice(FruitBox<Fruit> box){};
static Juice makeJuice(FruitBox<Apple> box){};	//오류, 지네릭 클래스는 FruitBox이고 타입만 다름
```

* **<? extends T>** : 와일드카드의 상한 제한, T와 그 자손들만 가능
* **<? super T>** : 와이들카드의 하한 제한, T와 그 조상들만 가능
* **<?>** : 제한 없음, 모든 타입이 가능, <? extends Object> 와 동일

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/FruitBoxEx3.java)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/FruitBoxEx4.java)

### 지네릭 메서드

메서드의 선언부에 지네릭 타입이 선언된 메서드

반환타입 바로 앞에 선언함

```java
static <T> void sort(List<T> list,Comparator<? super T> c){
    ...
}
```

지네릭 클래스에 정의된 타입 매개변수와 지네릭 메서드에 정의된 타입 매개변수는 전혀 별개의 것이다

이 타입 매개변수는 메서드 내에서만 지역적으로 사용된다. 따라서 메서드가 static이건 아니건 상관없다

> ❓❓반대편에서 호출할 때 지네릭 메서드와 그냥 메서드에 지네릭이 붙은것의 차이를 잘 모르겠음

### 지네릭 타입의 형변환

> ❓❓마찬가지로 지네릭스 사용에 대해 좀 더 익숙해져야 이해가 될 듯

* 지네릭 타입과 원시 타입은 형변환 가능
* 대입된 타입이 다른 경우 형변환 불가능
* `Box<? extends Object> wBox = new Box<String>();`가능

### 지네릭 타입의 제거

컴파일러는 지네릭 타입을 이용하여 소스파일을 체크하고 필요한 곳에 형변환을 넣어준 후 지네릭 타입을 제거한다

즉,컴파일된 파일(*.class)에는 지네릭에 대한 정보가 없다

#### 기본적인 제거과정

1. 지네릭 타입의 경계(bound)를 제거한다
2. 지네릭 타입을 제거한 후 타입이 일치하지 않으면 형변환 추가

## 2.열거형(enums)

서로 관련된 상수를 편리하게 선언하기 위한  것으로 여러 상수를 정의할 때 사용하면 유용하다

값과 타입 모두 관리하기 때문에 논리적인 오류를 줄여준다

### 열거형의 정의와 사용

`enum 열거형이름 {상수명1,상수명2...}`

모든 열거형의 조상은 `java.lang.Enum` 이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/EnumEx1.java)

### 열거형에 멤버 추가하기

열거형 상수의 값이 불 연속적인 경우엔 열거형 상수의 이름 옆에 원하는 값을 괄호()와 함께 적어준다

```java
enum EDirection {EAST(1), SOUTH(5), WEST(-1), NORTH(10)}
```

열거형 상수를 모두 추가한 후 인스턴스 변수와 생성자 등을 추가할 수 있다

생성자는 외부에서 호출하지 못하게 묵시적으로 `private`이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/EnumEx2.java)

#### 열거형에 추상 메서드 추가

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/EnumEx3.java)

### 열거형의 이해

열거형 상수 하나하나가 해당 열거형 클래스의 객체이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch12/EnumEx4.java)

> ❓❓뭔가 부족함
>
> 열거형이 사실은 enum을 상속받은 클래스이고 열거형 상수 하나하나가 그 클래스의 객체라고 한다
>
> 하지만 내부적인 구현은 이해가 잘 안되는데...

## 3.애너테이션(annotation)

> 책에도 쓰라고만 나와있고 내부적으로 구현이 어떻게 됐는진 설명이 부족함
>
> 🚩**따라서 실제 사용하면서 그때 그때 이해되는대로 다시 정리할 계획임**

프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것

### 표준 애너테이션

#### @Override

컴파일러에게 오버라이딩하는 메서드라는 것을 알려줌

간혹 오버라이딩하는 메서드명을 잘못 작성하는 경우가 있는데 이 애너테이션을 사용하면 그런 경우 컴파일 오류를 발생시켜줌

따라서 항상 사용해야좋음

#### @Deprecated

앞으로 사용하지 않을 것을 권장하는 대상에 붙임

#### @SuppressWarnings

컴파일러의 특정 경고메시지가 나타나지 않게함

#### @SafeVararges

지네릭스 타입의 가변인자에 사용

#### @FunctionalInterface

함수형 인터페이스라는 것을 알림(JDK1.8)

#### @Native

native메서드에서 참조되는 상수 앞에 붙인다(JDK1.8)

#### @Target

애너테이션이 적용가능한 대상을 지정하는데 사용

#### @Documented

애너테이션 정보가 javadoc으로 작성된 문서에 포함되게 한다

#### @Inharited

애너테이션이 자손 클래스에 상속되게 함

#### @Retention

애너테이션이 유지되는 범위를 지정

#### @Repeatable

애너테이션을 반복해서 적용할 수 있게함(JDK1.8)







