# 함수

* 선언은 2가지 형태로 할 수 있음

```javascript
function book(){
	var title = "책";
	console.log(title);  
};
book();
//책
```

```javascript
var point = function(one,two){
    return one + two;
};
console.log(point(10,20));
//30
```

## 함수 이름 규칙

* 첫 문자

  * 영문자, $, 언더바(_) 사용가능
  * 숫자,&,*,@,+ 는 사용 불가

* 함수 이름 작명 시 권장사항

  * 함수 코드를 읽지 않더라도 함수 이름과 파라미터로 기능을 알 수 있도록 시맨틱(의미)를 부여하여 작명

  * 동사로 시작, 동사 + 명사 형태
  * 두 개 이상 단어일 때 두번째 단어 명사 사용, 명사의 첫 문자는 대문자
  * camelCase 형태라고 함

  