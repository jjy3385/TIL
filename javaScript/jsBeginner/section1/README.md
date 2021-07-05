# 기본문법

## hello.js 작성

[예제코드](https://github.com/jjy3385/jsBeginner/blob/main/section01/hello.html)

> 📌script태그 defer 속성
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

