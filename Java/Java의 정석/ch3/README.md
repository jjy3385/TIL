# 연산자(operator)

연산을 수행하는 기호

## 연산자의 종류

1.기능별 분류
* 산술 연산자 : 사칙연산,나머지연산,비트연산 등
* 비교 연산자 : <,>,==,!= 등
* 논리 연산자 : ||,&& 등 (AND,OR)로 조건을 연결
* 대입 연산자 : 우변항의 값을 좌변에 대입
* 기타 : 형변환연산자,삼항연산자 등...

2.피연산자의 개수에 따른 분류
* 단항연산자 : 부호연산자,증감연산자 등
* 이항연산자 : 사칙연산자,비교연산자 등
* 삼항연산자 : 삼항연산자는 하나뿐임 
> 항의 갯수가 적을수록 우선순위가 높음

## 연산자의 우선순위와 결합규칙

### 기억해야할 연산자 우선순위
|우선순위높음|우선순위낮음|식 예제|우선순위를 괄호로 표현한 식|
|--|--|--|--|
|쉬프트연산자(<<,>>)|산술연산자(+,- 등)| x << 2 + 1| x << (2 + 1)|
|비트연산자(&,|,^,~)(|비교연산자(==,!=,<,>)| num & 0xFF == 0| num & (0xFF == 0)|
|AND(&,&&)|OR( &#124;,&#124;&#124;)| x < -1 &#124;&#124; x > 3 && x < 5 | x < -1 &#124;&#124; (x > 3 && x < 5)|

### 연산자 우선순위 정리

산술&#62;비교&#62;논리&#62;대입

단항&#62;이항&#62;삼항

단항 연산자와 대입 연산자를 제외한 모든 연산의 진행방향은 ->

## 산술 변환

연산 수행 직전에 발생하는 피연산자의 자동 형변환

이항 연산자는 두 피연산자의 타입이 일치해야 연산이 가능하다.

따라서 연산 전에 형변환 연산자로 타입을 일치시켜야한다.

>대표적인 예로 피연산자의 타입이 int보다 작은 타입이면 피연산자를 int로 변환한 후 연산한다.  

## 단항 연산자

### 증감연산자와 부호연산자

증감연산자는 전위와 후위가 있음

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx2.java)

## 산술 연산자

### 사칙 연산자(+,-,&#42;)와 나머지 연산자(%)

사칙연산 시 int보다 작은 타입이면 피연산자를 int로 변환한 후 연산한다.

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx6.java)

char형의 사칙연산도 int로 변환한 후 연산하므로 다시 char형 변수에 데이터를 담기 위해선 명시적 형변환이 필요하다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx12.java)

리터럴 간의 연산은 명시적 형변환하지 않아도 컴파일 오류가 발생하지 않는다.

왜냐하면 컴파일러가 미리 연산을 수행하기 때문이다.

(❓잘 이해는 안됨, 컴파일러가 연산할 땐 자동형변환을 하지 않는다는 뜻?)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx13.java)

[소수점 버림 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx16.java)

[소수점 반올림 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx17.java)

## 비교연산자

비교연산자 역시 이항연산자이므로 두 피연산자의 타입이 다를 경우 자료의 범위가 큰 쪽으로 형변환 후 비교연산을 수행한다

### 실수형 비교

실수형은 근사값으로 저장되기 때문에 오차가 발생할 수 있다.

float 과 double 을 비교하기 위해선 double 타입 자료를 float 타입으로 명시적 형변환해야한다.

더 작은 범위를 갖는 자료로 형변환하여 오차가 발생하지만 그 오차를 무시하고 비교하는 개념임)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx22.java)

### 문자열 비교

문자열 비교의 경우 == 대신 equals()를 사용해야 한다

== 는 두 문자열이 완전히 같은 것인지 비교하는 것이다

(❓여기서 완전히 같다는 얘기는 참조하는 주소값이 같은지를 물어보는 것으로 생각되지만 9장의 내용이므로 패스)

반면 equals()는 두 문자열의 내용이 같은지 비교할 때 쓴다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx23.java)

## 논리 연산자

두 개의 조건이 결합된 경우 사용하는 연산자

논리연산자의 피연산자는 boolean 형 혹은 boolean 형을 결과로 갖는 조건식만 허용된다

### 효율적인 연산(short circuit evaluation)

논리연산자는 효율적인 연산을 한다.

* OR연산'||'의 경우, 좌측 피연산자가 true이면 우측의 결과에 상관없이 항상 true이므로 우측 피연산자의 값을 평가하지 않는다.
>📌이때, 평가순서와 우선순위는 헷갈리면 안된다.평가순서는 시퀀스포인트 왼쪽에 있는 표현식을 먼저 평가하는 것이기 때문에 왼쪽에서 오른쪽으로 흐른다.
* 위와 마찬가지로 AND연산'&&'의 경우, 좌측 피연산자가 false이면 우측의 결과에 상관없이 항상 false이므로 우측 피연산자의 값을 평가하지 않는다.
* 이와 같은 내용을 숙지하고 있다면 || 를 사용할 경우, true일 확률이 높은 조건식을 좌측에 두어 빠른 연산결과를 얻을 수 있다.

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx26.java)

### 논리 부정연산자 !

이해하기 좋은 코드를 짤 때 유용하다

단항연산자이므로 결합방향이 오른쪽에서 왼쪽이다

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx27.java)

### 비트 연산자

* 비트 연산자는 비트 단위로 논리 연산을 한다
* 피연산자를 이진수로 표현했을 때 각 자리에 연산을 수행한다
* 피연산자는 정수형만 사용 가능하다

비트XOR연산자 '^' 는 피연산자의 값이 서로 다를 때 1, 같을 때는 0 을 반환한다

|x|y|x&#124;y|x&y|x^y|
|--|--|--|--|--|
|1|1|1|1|0|
|1|0|1|0|1|
|0|1|1|0|1|
|0|0|0|0|0|

* 비트OR연산자 '|' 는 주로 비트의 값을 변경할 때 사용한다
* 비트AND연산자 '&' 는 특정 비트의 값을 뽑아낼 때 사용한다
* 비트XOR연산자 '^' 는 같은 값을 두고 해당 연산을 수행하면 원래의 값으로 돌아오는 특징이 있다.

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx28.java)

### 비트전환연산자 '~' 

논리부정 연산자 ! 와 유사하다

1이면 0, 0이면 1을 반환한다

피연산자의 1의 보수를 얻을 수 있어 1의 보수 연산자라고도 한다

>양수 p 에 대한 음의 정수를 얻으려면 ~p + 1 
>음수 n 에 대한 양의 정수를 얻으려면 ~(n - 1)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx29.java)

### 비트 쉬프트 연산자 <<,>>

피연산자의 각 자리를 왼쪽,또는 오른쪽으로 이동시키는 연산자

>> 연산자의 경우 각 자리를 오른쪽으로 이동시키기 때문에 왼쪽 끝에서 부터 숫자를 채워야된다.

이때, 부호있는 정수의 경우 부호유지를 위해 양수면 0을 음수면 1을 채운다

(❓정확히 이해는 못했음,다만 음수를 2의 보수법에 의해 이진수로 만들었기 때문에 이렇게 된다고 생각함)

[예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch3/OperatorEx30.java)

>좌측 피연산자엔 산술 변환이 적용되어 int보다 작은 경우엔 int로 자동형변환된다
>하지만 우측 피연산자는 산술 변환이 적용되지 않는다

## 그 외 연산자

### 조건 연산자

삼항연산자라고도 한다

(조건식) > 식1 : 식2

조건식이 참이면 식1 수행, 거짓이면 식2 수행










