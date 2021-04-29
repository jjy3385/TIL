# 조건문과 반복문

프로그램의 흐름을 바꾸는 역할을 한다.

제어문이라고 함

## 조건문

if문과 switch문이 있다

### switch문의 제약조건

switch문의 조건식의 결과값은 반드시 정수값이며 중복되어선 안된다

또한 case문의 값은 반드시 상수여야 한다. 변수나 실수는 사용할 수 없다

## 반복문

* for문 - 반복횟수를 알 때 사용하면 좋다
* while문 - 반복횟수를 알 수 없을 때 좋다
* do while문 - 무조건 최소한 한번은 수행되는 경우 사용한다(잘 안쓰는거 같음)

### 중첩 for 문

[별찍기 예제](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch4/FlowEx17.java)

### 향상된 for 문

배열과 컬렉션에 저장된 요소에 접근할 때 사용(자바의 foreach문)

>for(타입 변수명 : 배열 또는 컬렉션){
>   //반복할 문장
>}

### continue

반복이 진행되는 도중에 반복문의 끝으로 이동한다

for문인 경우엔 증감식으로 while문인 경우엔 조건식으로 이동한다

특정 조건을 만족하는 경우에 그 이후의 문장을 수행하지 않고 다음 반복으로 넘어갈 때 사용한다

### 이름 붙은 반복문

반복문에 이름을 붙일 수 있고 여기에 break이랑 continue 섞어서 프로그램 흐름을 조절할 수 있다

[예제1](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch4/FlowEx33.java)

[예제2](https://github.com/jjy3385/StandardOfJava/blob/main/src/ch4/FlowEx34.java)

