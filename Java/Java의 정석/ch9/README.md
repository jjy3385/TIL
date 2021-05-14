
# java.lang패키지

자바 프로그래밍의 가장 기본이 되는 패키지로 별다른 `import` 문 없이도 사용할 수 있다.

## Object클래스

모든 클래스의 최고 조상이기 때문에 Object클래스의 멤버들은 모든 클래스에서 사용할 수 있다.

### 1.equals(Object obj)

참조변수를 매개변수로 받고 주소값으로 두 객체가 같은지 판단한다.

그렇기 때문에 서로 다른 두 객체는 항상 false가 반환된다.

[예제1](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/EqualsEx1.java)

[예제2](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/EqualsEx2.java)

자손클래스에서 equals메서드를 오버라이딩해서 쓸 수 있다

>📌String클래스 역시 Object클래스의 equals메서드를 그대로 사용한것이 아니라 문자열 값을 비교하도록 오버라이딩했다.
>그러므로 String.Equals메서드는 주소가 아닌 문자열값을 비교한다

### 2.hashCode()

해시함수를 구현한 것

해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드를 반환한다(❓)
> 아직은 잘 모르겠음

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/HashCodeEx1.java)

### 3.toString()

인스턴스에 대한 정보를 문자열로 제공하는 함수

오버라이딩하지 않은 경우, 클래스이름 + "@" + 16진수의 해시코드 를 반환함

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/CardToString2.java)

### 4.clone()

자신을 복제하여 새로운 인스턴스를 생성하는 메서드

단, Object클래스에 정의된 clone()메서드는 인스턴스의 값만 복제하기 떄문에 참조타입의 인스턴스 변수가 있는 클래스는 완전한 복제가 이뤄지지 않음

clone메서드를 사용하려면...
1. 복제할 클래스가 cloneable 인터페이스를 구현해야함
2. clone메서드를 오버라이딩하면서 접근 제어자를 public으로 변경
> Object클래스에는 protected 로 되어 있기 때문에 접근제어자를 public으로 수정하지 않으면 상속관계가 없는 다른 클래스에서 clone() 호출할 수 없게 됨

#### 공변 반환타입

조상의 타입이 아닌, 실제로 반환되는 자손 객체의 타입으로 반환할 수 있게 JDK1.5에서 추가된 기능

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/CloneEx1.java)

#### 📌얕은 복사와 깊은 복사

clone메서드는 저장된 값만 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지 않음

이 경우, 원본의 참조객체를 수정하면 복제본도 같은 객체를 참조하고 있기 때문에 같이 변경됨

이걸 ***얕은 복사***라고 함

***깊은 복사***는 객체가 참조하고 있는 객체까지 복제하는 것임(`new`)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/ShallowDeepCopy.java)

### 5.getClass()

자신이 속한 클래스의 Class객체를 반환하는 메서드

Class객체는 클래스의 모든 정보를 담고 있으며 클래스당 1개만 존재한다

> ❓근데 static은 아니네..

클래스 파일이 클래스 로더에 의해 메모리에 올라갈 때 자동으로 생성됨

#### 클래스 객체를 얻는 방법
* `Class cObj = new Card().getClass();` 생성된 객체로부터
* `Class cObj = Card.class;` 클래스 리터럴로부터
* `Class cObj = Class.forName("Card")` 클래스 이름으로부터

동적으로 객체를 생성하고 메서드를 호출하는 방법은 리플렉션API 를 검색해보면됨
>지금은 그냥 이런게 있다 정도...

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/ClassEx1.java)

## String클래스

다른 언어는 char배열이 그냥 문자열이지만 자바에서는 char배열 + 다양한 기능까지 함께 제공하는 String클래스가 있다.

### 변경이 불가능한(immutable) 클래스

String클래스에는 문자열을 저장하기 위한 문자형 배열 참조변수 `char[] value` 가 있다.

한번 생성된 String인스턴스의 문자열은 변경할 수 없다

따라서 덧셈연산자 `+` 를 이용하여 문자열을 다룰 경우, 매번 연산할 때마다 새로운 문자열을 가진 String인스턴스가 생성되어 메모리 공간을 차지하게 된다

그러므로 여러번 문자열을 합칠 경우엔 `+` 보다는 `StringBuffer` 를 사용하는 것이 좋다

### 문자열의 비교

두 가지 방식으로 String 참조변수에 문자열을 할당할 수 있다

#### 생성자 호출할 떄(`String str = new String("abc")`)

새로운 String인스턴스가 생성된다

#### 문자열 리터럴을 그대로 저장할 떄(`String str = "abc"`)

기존에 같은 문자열을 갖는 String인스턴스가 존재한다면 재사용한다.

[📌예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringEx1.java)

### 문자열 리터럴

컴파일 시 같은 내용의 문자열 리터럴은 클래스 파일에 한번만 저장된다

즉 JVM이 클래스 파일을 해독할 때 문자열이 같은 인스턴스는 한번만 생성되고 여러 참조변수에 의해 공유되어 효율적으로 메모리를 사용할 수 있도록 구성하는 것이다

### join() 과 StringJoiner

join() 은 여러 문자열 사이에 구분자를 넣어 결합하는 메서드다

split() 과 반대의 작업을 한다고 이해하면 된다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringEx4.java)

### 문자 인코딩 변환

서로 다른 문자 인코딩을 하는 컴퓨터 간에 데이터를 주고받을 때 적절한 문자 인코딩이 필요하다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringEx5.java)

### 기본형 값을 String으로 변환

* 숫자에 빈 문자열 "" 더해주기
* valueOf() 사용하기

### String을 기본형 값으로 변환

* valueOf() 사용하기
* parseInt() 사용하기

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringEx6.java)


## StringBuffer와 StringBuilder

String클래스는 한번 생성한 문자열을 변경할 수 없어 문자열에 대한 `+` 연산이 반복될 경우 문자열이 계속 생성되어 메모리에 안좋은 영향을 줄 수 있다

이런 경우엔 `StringBuffer` 를 사용하면 좋다

### StringBuffer 생성자

```java

public StringBuffer(int length) {
  value = new char[length];
  shared = false;
}
public StringBuffer(){    
  this(16); //버퍼의 크기를 지정하지 않으면 16으로 만들어짐
} 
public StringBuffer(String str){
  this(str.length + 16);
  append(str);
```

편집할 문자열의 길이를 고려하여 충분한 버퍼를 잡아두는게 좋다

편집 중인 문자열이 버퍼의 길이를 넘어서게 되면 버퍼의 길이를 늘려주는 작업이 따로 수행되므로 성능이 떨어지게 된다.

### StringBuffer의 변경

append() 함수를 사용하여 문자열을 추가할 수 있다

이 함수의 반환형이 다시 StringBuffer인스턴스이다

### StringBuffer의 비교

String클래스와 달리 equals메서드를 오버라이딩하지 않았기 떄문에 equals()의 결과가 등가비교연산자(`==`)의 결과와 동일하다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringBufferEx1.java)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/StringBufferEx2.java)

### StringBuilder?

StringBuffer는 멀티쓰레드에 안전(thread safe)하도록 동기화되어 있다...(❓)

잘 모르겠지만 StringBuffer와 StringBuilder는 하는 일이 똑같다.

이번 장에서는 멀티쓰레드 동기화 관련해서 둘 사이의 성능차이가 있다는 것 정도만 기억한다

## Math클래스

기본적인 수학계산에 유용한 메서드를 제공하는 정적 클래스

### 올림,반올림,버림

정수형간의 연산에서 소수점 아래가 항상 버려진다는 것을 이용한다

rint()도 round()처럼 소수점 첫 째자리에서 반올리하지만 반환형이 double이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/MathEx1.java)

### 예외를 발생시키는 메서드

메서드 이름에 'Exact'가 포함된 메서드들은 연사 시 발생할 수 있는 오버플로우를 감지할 수 있다

즉,오버플로우 발생 시 예외를 발생시킨다(다른 메서드들은 그냥 오버플로우가 발생해도 예외가 발생되진 않는다)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/MathEx2.java)

### 삼각함수,지수,로그

삼각함수가 기억이 안나는데 여하튼 이런게 있다는 것 정도만 기억하자

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/MathEx3.java)

## 래퍼(wrapper) 클래스

기본형을 객체처럼 다루기 위한 클래스

래퍼 클래스의 equals는 모두 객체 주소값이 아닌 객체가 갖고있는 값을 비교하도록 오버라이딩되어 있다

#### number 클래스 

숫자형 래퍼 클래스들의 부모클래스

객체가 갖고 있는 값을 숫자와 관련된 기본형으로 변환하여 반환하는 메서드들을 정의하고 있는 추상 클래스이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/WrapperEx2.java)

### 오토박싱&언박싱

#### 오토박싱

기본형 값을 래퍼 클래스의 객체로 자동 변환해주는것 

#### 언박싱

래퍼 클래스 객체를 기본형 값으로 변환하는 것

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/WrapperEx3.java)



# 유용한 클래스

## 1.java.util.Objects클래스

객체의 비교나 널체크에 유용

### equals메서드

Objects클래스의 equals() 메서드는 null검사를 함께 해준다

즉 `if(a!=null && a.equals(b))` 와 같은 뜻이다

### deepEquals()메서드

객체를 재귀적으로 비교하기 때문에 다차원 배열의 비교도 가능하다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/ObjectsTest.java)

## 2.java.util.Random클래스

같은 종자값(seed)를 사용할 경우 같은 값들을 순서대로 얻게 된다

## 3.정규식(Regular Expression) - java.util.regex패키지

정규식이란 텍스트 데이터 중 원하는 패턴과 일치하는 문자열을 찾아내기 위한 것으로 **미리 정의된 기호와 문자를 이용해 작성한 문자열**을 말한다

`Pattern` 클래스는 정규식을 정의하는데 사용되고 `Matcher`는 정규식(패턴)을 데이터와 비교하는 역할을 한다

[예제1](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/RegularEx1.java)

#### 예제1 설명(정규식 사용하는 법)

1. 정규식을 매개변수로 Pattern클래스의 static메서드인 compile(Stirng regex)를 호출하여 Pattern인스턴스를 얻는다

   `Pattern p = Pattern.compile("c[a-z]");`

2. 정규식으로 비교할 대상 문자열을 매개변수로 Pattern클래스의 matcher(CharSequence input)을 호출하여 Matcher인스턴스를 얻는다

   즉,matcher메서드의 반환형이 Matcher 클래스이다.

   `Matcher m = p.matcher(data[i]);`

3. Matcher인스턴스의 boolean matches()를 호출하여 정규식에 부합하는지 확인한다

   `if(m.matches())`

   

[예제2](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/RegularEx2.java)

[예제3](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/RegularEx3.java)

[예제4](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/RegularEx4.java)

## 4.java.util.Scanner클래스

화면,파일,문자열과 같은 입력소스로부터 문자데이터를 읽어오는데 도움주는 클래스다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/ScannerEx1.java)

## 5.StringTokenizer

긴 문자열을 지정된 구분자(delimiter)를 기준으로 여러 개의 문자열로 자르는 데 사용된다

똑같은 기능을 `String`의 `split(String regex)` 과 `Scanner`의 `useDelimiter(String pattern)`을 사용하여 구현할 수 있다

다만, `StringTokenizer`는 정규식에 익숙하지 않은 경우 사용하기 편하다

## 6.java.math.BigInteger클래스

가장 큰 정수형 타입인 long으로 표현할 수 있는 10진수는 19자리 정도이다

`BigInteger`는 이보다 더 큰 정수를 표현하기 위해 사용된다

내부적으로 int배열을 사용하여 값을 저장하는 방식이다

```java
final int signum;	//부호
final int[] mag;	//값
```

부호만 다른 두 값은 meg는 같고 signum만 다르다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/BigIntegerEx.java)

## 7.java.math.BigDecimal클래스

가장 큰 실수형 타입인 double의 경우 정밀도가 최대 13자리정도이다

`BigDecimal`은 실수형과 달리 정수를 이용해서 실수를 표현한다
$$
정수 * 10^{-scale}
$$

```java
private final BigInteger intVal;	//정수
private final int scale;			//지수
private transient int precision; 	//정밀도
```

* 정수부를 표현하는데 `BigInteger`를 사용한다

* 지수부인 scale이  -scale로 올라가므로 소수점 자릿수를 의미한다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch9/BigDecimalEx.java)











