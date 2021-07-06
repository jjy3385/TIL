# 연산자

## 산술연산자 + 

* 한쪽이라도 숫자가 아니면 연결
* -,*,/ 등 다른 산술연산자는 연결하지 않고 다른 방법을 취함

```javascript
var value = 1 + 5 + "ABC";
console.log(value);
```

## 숫자로 변환

* 연산하기 전에 우선 숫자로 변환함

  | 값 타입   | 변환 값                                               |
  | --------- | ----------------------------------------------------- |
  | Undefined | NaN                                                   |
  | Null      | 0                                                     |
  | Boolean   | true:1,false:0                                        |
  | Number    | 변환 전/후 같음                                       |
  | String    | 값이 숫자면 숫자로 연산<br />단 더하기(+)는 연결 연산 |

```javascript
var number;
console.log(1+number);
//1 + NaN => NaN
console.log(10 + true);
//11
console.log(10 + false);
//10
console.log(10 + "123");
//10123
console.log(123 - "23");
//100
```

## -,*,/,% 연산자

### 곱하기 연산자(*)

* 소수 값이 생기는 경우엔 정수로 만든 후 다시 나눠줌
* IEEE 754의 유동소수점처리때문임
* 자바스크립트는 정수,실수 타입이 아니라 그냥 모든 수가 실수타입(유동소수점)임

```javascript
console.log(2.3 * 3);
//6.8999999999999995
console.log(2.3 * 10 * 3 / 10);
//6.9
```

### 나머지 연산자(%)

* 마찬가지로 실수이므로 딱 떨어지는 정수가 안나오는 것에 주의!

```javascript
console.log(5%2.3);
//0.4가 아니라 0.40000000000000036

```

### 전치,후치 연산자

#### 전치 ++ 연산자(--도 같음)

* 형태: ++value
* 값을 자동으로 1증가시킴
* 표현식 평가 전에(세미콜론)에 증가시킴

#### 후치 ++ 연산자(--도 같음)

* 전치와 다르게 표현식 평가 후에(세미콜론)에 증가시킴

```javascript
var value = 1;
console.log(++value + 1);
//3 = 2 + 1
console.log(value++ + 1);
//3 = 2 + 1 (log에 표현할떄까진 증가 X)
console.log(value);
//3(두번쨰 문장의 평가가 종료되는 시점(세미콜론)에 value가 1 증가함)
```

논리 NOT 연산자(!)

```javascript
console.log(!"A");
//false
console.log(!!"A");
//true
```

## 유니코드

* 세계의 모든 문자 통합하여 코드화
* 0000~FFFF, 10000~1FFFF 값에 문자 매핑

#### 표기법

```javascript
console.log("\u0031");
//1
```

### UTF

* Unicode Transformation Format

* 유니코드에 코드포인트를 매핑하는 방법
* UTF-8은 8비트로 매핑, 8비트 인코딩이라고 부름

> 사실 뭔 뜻인지 잘 모르겠음

## 비교 연산자(부등호 >,<,>= 등)

* 양쪽이 Number 타입일 땐 비교가 제대로 됨

### String 타입 비교

* 한쪽이 String타입이면 false;
* 양쪽이 모두 String타입이면 유니코드 사전 순서대로 비교

```javascript
console.log("A" > "1");
//true
console.log("\u0031" > "\u0033");
//false
```

* 문자 하나씩 비교

```javascript
console.log("A01" > "A21");
//false 왼쪽부터 문자 하나씩 비교함
```

## 동등,일치 연산자

### 동등(==) 연산자

* 값만 비교함

* 타입은 비교하지 않음

  따라서 1과 "1"은 같음

```javascript
console.log(1=="1");
//true 
//"1"을 1로 변환, 즉 숫자로 변환하여 비교
var value1;
console.log(value1==undefined);
//true
var value2;
console.log(value2==null);
//true
//undifined 가 값이고 타입도 undefined , null은 타입은 object이고 값은 null
//이 둘의 값만 비교하므로 둘은 같음
//정확하게는 아직 잘 모르겠음
```

### 일치 연산자(===)

* 값과 타입 둘다 비교함

* 따라서 1과 "1"은 일치하지 않음

```javascript
console.log(1==="1");
//false
var val;
console.log(val==null);
//true
console.log(val===null);
//false
```

📌값과 타입 둘 다 비교하는 === 를 먼저 고려하고 그 다음 == 를 고려하세요

분명 여기서 삽질 한번은 할거임

> 불일치연산자(!==)는 값 또는 타입이 다르면 false임

## 논리 OR  연산자(||)

* 왼쪽 결과가 true면 오른쪽은 비교하지 않음

```javascript
var value, zero = 0,two =2
console.log(value || zero || two);
//2
```

* value는 undefined 이므로 false

* zero는 0 이므로 false

* two 는 2 이므로 true

* 해당 평가식의 평가결과는 true인데 반환은 2임

  > 이쪽은 정확한 의미를 모르겠음

```javascript
var one = 1;
console.log(one===1 || two ===2);
//true
```

📌`one===1`의 결과가 true이므로 그 다음 평가식은 평가하지 않음

`&&`의 경우엔 반대로 왼쪽 평가식 결과가 false면 그 다음은 평가하지 않음

## 조건 연산자

3항 연산자라고도 함

```javascript
console.log(1===1?"같다":"다르다");
//같다
console.log(1==="1"?"같다":"다르다");      
//다르다
```

