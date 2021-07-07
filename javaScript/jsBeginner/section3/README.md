# 문장(Statement)

## debugger

* debugger 위치에서 실행 멈춤
* 브라우저의 개발자 도구가 열려있을 때만...

```javascript
var sports = "스포츠";
debugger;
console.log(sports);
```

## for문

* 형태: for(초기값opt; 비교opt;증감opt)문장

* 실행과정

  1. 초기값opt

  2. 비교opt

  3. 문장

  4. 증감opt

  5. 비교opt
  6. 3 ~ 5 반복하다 비교opt 가 false면 종료

```javascript
for(var i = 0; i < 0; i++){
    console.log(i);
}
//최초 비교opt가 false이므로 실행안됨
for(var i = 0; i < 3; i++){
    console.log(i);
}
//마지막 회차에서 i = 2 일때 console.log(2); 표시한 후 증감opt가 먼저 수행되기 때문에 비교opt가 false가 됨
```

## break,continue

### break

* 반복문이나 switch를 빠져나감

### continue

* 반복문의 증감opt로 바로 점프함

```javascript
for(var k = 0; k<5; k++){
    if(k===2||k===3){
        continue;//증감opt로 바로 점프하기 때문에 그 다음 문장은 수행안됨
    }
	console.log(k);
}
/*
0
1
4
*/
```

## switch

* break; 없으면 그 다음 case 로 넘어감

```javascript
var k = 1,value = 0;
switch(k){
    case 1:
        value = 100;
    case 2:
		value = 200;	
}
console.log(value);
//200
```

```javascript
var k = 1,value = 0;
switch(k){
    case 1:
        value = 100;
	break;
    case 2:
		value = 200;
	break;	
}
console.log(value);
//100;
```

## 📌strict 모드

* "use strict"; 를 스크립트 맨 위에 작성

* 엄격하게 JS문법 사용하겠다는 선언
* ES5부터 지원되며 항상 하면 좋음

```javascript
"use strict";
try{
    book = "책";
    console.log(book);
}catch(error){
    console.log(error.message);
};
//book is not defined

```

>  "use strict" 를 사용하지 않으면 예외가 발생하지 않지만 사용했기 때문에 `book = "책";` 에서 예외발생

### label(레이블)

* 이제 사용하지 않는다
* 문장에 이름을 줘서 원하는 문장에서 break;continue 등의 처리를 할 수 있도록 해준다
* 왜 사용하지 않을까?
* 일단 코드흐름이 복잡해져서 개발자가 실수할 여지가 많아질 것 같다
* 다른 이유는??

```javascript
loop1:
for(var i = 0; i < 3; i++){
    loop2:
    for(var j = 0; j < 3; j++){
        if(i === 1 && j === 1){
            continue loop1;
        }
        console.log("i = " + i + ", j = " + j);
    }
}
/*
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
i = 2, j = 0
i = 2, j = 1
i = 2, j = 2

i = 1,j=1 일 때 loop1의 i++ 로 넘어갔음
*/
```

## strict 모드와 with

* strict 모드에서 with 구문을 사용하면 에러가 발생한다

❓with가 뭔데?

* 특정 Object를 기본값으로 설정하게 해줌

```javascript
console.log(PI);
//에러
```

```javascript
with(Math){
    console.log(PI);
}
//3.141592653589793
```

```javascript
"use strict";
with(Math){
    console.log(PI);
}
//Uncaught SyntaxError: Strict mode code may not include a with statement
```

