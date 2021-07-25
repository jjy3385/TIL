# Number 오브젝트

* 숫자처리를 위한 프로퍼티와 함수로 이루어짐

* 오브젝트를 안다는 것은 그 오브젝트의 구성 요소인 프로퍼티와 함수를 안다는 뜻

전체적인 개요를 먼저 그리는게 중요

예를 들어, toString() 함수에 대해 설명할 때

'toString()함수는 숫자를 문자로 변환한다'라고 설명하는 것이 아니라

'숫자를 문자로 변환하기 위해 toString()을 사용한다'라고 설명하는게 맞음

왜냐면 숫자를 문자로 변환하는게 목적이고 toString()이 수단이기 때문에 목적을 기억하고 있어야함

## Number 타입으로 변환

* Number()

```javascript
console.log(Number("123")+500);
//623
console.log(Number("ABC"));
//NaN : 숫자로 변환할 수 없거나 변환했으나 숫자가 아니란 뜻
```

```javascript
console.log(Number(0x21));
console.log(Number(true));
console.log(Number(null));
console.log(Number(undefined));
/*
33
1
0
NaN
*/
```

## 인스턴스 생성(new 연산자)

* new 연산자로 Number 생성자를 호출하여 인스턴스 생성

* 첫 문자가 대문자임
* 인스턴스 생성 목적
  * 인스턴스마다 값을 갖기 위한 것

```javascript
var obj = new Number(123);
console.log(typeof obj);
//object
```

> 📌Object 는 프로퍼티들로 구성된 {name:value} 형태를 뜻하는 것이고 object 는 인스턴스를 뜻하는 것이다

```javascript
var obj1 = new Number("123");
var obj2 = new Number("456");
console.log(obj1.valueOf());
console.log(obj2.valueOf());
//123
//456
```

## 인스턴스 생성과 형태

* 빌트인 Number 오브젝트와 Number 인스턴스 비교

```javascript
        <script>
            window.onload = function(){
                "use strict";
                debugger;

                var numberObject = Number;
                var obj = new Number("123");

                debugger;

                var proto = obj.__proto__;
            }
        </script>

```

* ### numberObject의 형태(빌트인 Number)

![](D:\GitRepository\TIL\javaScript\jsBeginner\section7\images\빌트인Number오브젝트.png)

* ### obj의 형태(인스턴스)

  ![](D:\GitRepository\TIL\javaScript\jsBeginner\section7\images\Number인스턴스.png)

  > 📌둘을 비교해보면 빌트인Number의 prototype 만 인스턴스의 __ proto __ 프로퍼티에 복사되었고 나머지 프로퍼티는 복사되지 않음
  >
  > 참고로 prototype 은 시제품이라는 뜻이 있음

## 📌프리미티브 값(Primitive Value)

* 언어에 있어 가장 낮은 단계의 값

* 더 이상 분해, 전개 불가

```javascript
<!DOCTYPE html>
<html lang=ko>
<head>
    <meta charset="utf-8">
    <title>자바스크립트</title>
    <script>
        window.onload = function () {
            "use strict";
            debugger;
            var book = "책";
            var point = 123;
            var obj = { book: "책" };
            var num = new Number(123);
        }
    </script>
</head>
<body>
</body>
</html>
```

* `var book = "책";`과 `var point = 123;` 의 두 프로퍼티의 "책" 과 123이 프리미티브 값임

  즉, 더 이상 분해,전개할 수 없으며 가장 낮은 단계의 값이다

![](D:\GitRepository\TIL\javaScript\jsBeginner\section7\images\프리미티값1.png)

* 📌Object 는 프리미티브값을 제공하지 않는 형태임

![](D:\GitRepository\TIL\javaScript\jsBeginner\section7\images\프리미티값2.png)

​	❓`__ proto __ : Object` 가 있음

​	여하튼 이름과 값만 있는 형태가 아니기 때문에 프리미티브값을 제공하지 않는 형태라고 할 수 있음

* 인스턴스는 프리미티브값을 제공함

  그냥 시멘틱적으로 제공하고 있는 것을 확인할 수 있음

![](D:\GitRepository\TIL\javaScript\jsBeginner\section7\images\프리미티브값3.png)

* `var num = new Number("123");` 로 바꿔도 primitiveValue 는 123 임

* 대괄호 두개 열고 닫기는 자바스크립트 엔진이 만들었다는 뜻임 `[[]]`

## 인스턴스의 프리미티브 값

* 인스턴스를 생성하면 파라미터 값을 인스턴스의 프리미티브 값으로 설정

* `var obj = new Number(123);` 라면 파라미터인 123을 프리미티브값으로 하는 인스턴스를 생성함

* 프리미티브 값을 갖는 빌트인 오브젝트
  * Boolean,Date,Number,String

```javascript
var obj = new Number(123);
console.log(obj + 500);
//623
//num 는 인스턴스이지만 프리미티브값인 123 + 500 이 게산됨 
```

### Number 인스턴스의 프리미티브 값을 반환

* valueOf()

```javascript
var obj = new Number(200);
console.log(obj);
console.log(obj.valueOf());
//{Number(200)}
//200
```

## data를 String타입으로 변환

* toString()
* 파라미터는 진수(2~36)opt 를 의미함, 디폴트는 10진수

```javascript
var value = 20;
console.log(20 === value.toString());
console.log(value.toString(16));
//false <== 값은 둘 다 20이지만 타입이 다름
//14 <== 20을 16진수로 바꿈
```

* 변환 시 주의사항

  자바스크립트에서 숫자는 실수이기 때문에 아래와 같은 코드가 나올 수 있음

```javascript
console.log(20..toString());
//20
console.log(20.toString());
//오류
//20. 까지가 숫자표현이고 .toString() 이 함수호출임
```

## 지역화 문자

* toLocaleString()
* ES5까지는 파라미터 사용 불가였지만 ES6부터는 파라미터 사용 가능

```javascript
var value = 1234.56;
console.log(value.toLocaleString());
console.log(value.toLocaleString('de-DE'));
console.log(value.toLocaleString('zh-Hans-CN-u-nu-hanidec'));
/*
1,234.56
1.234,56
一,二三四.五六
*/
```

## 지수표기

* toExponential()
* 파라미터는 소수 이하 자릿수를 의미함(0~20)

```javascript
var value = 123456;
console.log(value.toExponential());
console.log(value.toExponential(3));
//1.23456e+5
//1.235e+5
```

## 고정 소수점 표기

* toFixed()
* 파라미터는  반환할 소수 이하 자릿수

```javascript
var value = 1234.567;
console.log(value.toFixed());
console.log(value.toFixed(2));
console.log(value.toFixed(5));
//1235
//1234.57
//1234.56700
```



