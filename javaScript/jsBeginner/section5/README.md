# 오브젝트(Object)

여러 프로퍼티를 그룹화한 것

## 프로퍼티

* {name: value} 형태
* value 에 다시 오브젝트를 넣어서 계층적으로 만들 수 있음

```javascript
var book = {
    title: "네트워크 교실",
	author:{
        name:"아미노 에이지",
		age: 50
    }
};
console.log(book.title);
console.log(book.author.name);
console.log(book.author.age);
/*
네트워크 교실
아미노 에이지
50
*/
```

## 프로퍼티 추가와 변경

* 오브젝트에 프로퍼티를 추가하거나 변경할 수 있음
* 없으면 추가되고 있으면 변경됨
* 형태
  * obj.abc = 123;
  * obj["abc"] = 123;
  * 프로퍼티 이름을 변수에 작성하고 사용하는 방법

```javascript
var book = {};
book.title = "아마존 웹 서비스";
console.log(book);
//{title: "아마존 웹 서비스"} <== 추가됨
book.title = "하루 3분 네트워크 교실";
console.log(book);
//{title: "하루 3분 네트워크 교실"} <== 변경됨
```

```javascript
var book = {};
book["title"] = "아마존 웹 서비스";
console.log(book);
//{title: "아마존 웹 서비스"} <== 추가됨
book["title"] = "하루 3분 네트워크 교실";
console.log(book);
//{title: "하루 3분 네트워크 교실"} <== 변경됨
```

```javascript
//프로퍼티 이름을 변수에 작성하여 사용하기
var book = {};
var valueName = "title";
book[valueName] = "하루 3분 네트워크 교실";
console.log(book);
//{title: "하루 3분 네트워크 교실"}
```

## Object 프로퍼티 열거(읽기)

### for ~ in 문

* 형태: for( 변수 in 오브젝트)문장;
* 변수에 프로퍼티의 name이 매핑됨
* 그러므로 value에 접근하기 위해선 오브젝트[변수명]을 사용(프로퍼티 이름을 변수로 접근하는 사용법)

```javascript
var sports = {
    football: "축구",
	basketball: "농구"
};
for(var item in sports){
    console.log(item);
	console.log(sports[item]);
};
/*
football
축구
basketball
농구
*/
```

