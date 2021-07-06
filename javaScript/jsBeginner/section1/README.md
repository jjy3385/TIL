# 기본문법

[예제코드](https://github.com/jjy3385/jsBeginner/blob/main/section01/hello.html)

> 📌**script태그 defer 속성**
> 
> defer를 쓰면 body까지 모두 렌더링한 후에 hello.js 파일을 실행함
> 
> html파일은 위에서부터 차례대로 렌더링되기 때문에 defer를 안쓰면 오류가 날 수 있음
> 
> body태그까지 모두 렌더링되지 않은 상태에서 hello.js파일을 서버에서 가져와 바로 실행하면
> 
> js파일에서 body태그의 엘리먼트로 접근할 때 오류가 날 수 있음
> 
> 따라서 head에 있는 script태그에 defer 써주는게 좋음(그냥 항상 써주는게 좋을듯)

## 데이터타입

자바스크립트는 데이터를 기준으로 타입을 결정함

자바나C#은 타입을 먼저 선언하고 거기에 맞는 값을 넣지만 자바스크립트는 반대임

## Number 타입

* Number 타입의  특수한 3개의 값

  * NaN: Not a Number;

    숫자가 아닌 값

    다른 언어라면 컴파일이 안되게 하던가 오류가 나와야되지만 JS는 NaN이라는 특수한 값을 만들어서 프로그램이 죽지 않도록 함, 이것은 JS의 특징임

    ```javascript
    console.log(1 * "A");
    //NaN
    ```

  * Infinity: 양의 무한대

  * -Infinity: 음의 무한대

## String 타입

* 큰따옴표 작은따옴표 같이 사용가능

  ```javascript
  var str = "안녕,'마이클'";
  console.log(str);
  str = '안녕,"마이클"';
  console.log(str);
  ```

## undefined 와 null

### undefined

* 변수의 디폴트값
* 변수에 값을 할당하지 않은 것을 나타내는 시맨틱

### null

* 빈 값을 할당했음을 의미함(빈 객체)

### undefined 와 null 의 차이

이 두 변수를 `typeof`로 찍어보면 차이를 알 수 있음

undefined 는 undefined 가 나오고 null 은 object 가 나옴

undefined 는 아예 할당하지 않았으므로 자료형도 알 수 없지만 null은 object 자료형임

```javascript
var book;
console.log(book);
console.log(typeof book);

var note = null;
console.log(note);
console.log(typeof note);
```

## Object 타입

* 형태
  * {name: value}

* 프로퍼티(Property)
  * name과 value 하나를 지칭
* Object 는 프로퍼티의 집합

```javascript
var phone = {
    name: "gal",
    number: 12345
};
console.log(phone);
```

## 타입 정리

```javascript
console.log(typeof 123);
console.log(typeof "안녕");
console.log(typeof true);
console.log(typeof undefined);
console.log(typeof null);
console.log(typeof {name:"주영",birthyear:88});
```

위에서부터 순서대로 number - string - boolean - undefined - object - object

