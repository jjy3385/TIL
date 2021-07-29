# 5장 ASP.NET 표준 컨트롤

> 이번 단원은 그냥 컨트롤 사용법 설명해주는게  전부였음
>
> 약간의 코멘트할 거리만 정리함

## Label 컨트롤

## TextBox 컨트롤

## Button 컨트롤

## LinkButton 컨트롤

버튼은 타입이 `input` 인 `button` 태그인거고 링크버튼은 `a` 태그라고 볼 수 있음

하지만 표준 서버 컨트롤에서는 둘 다 기능은 똑같다고 보면 됨

어짜피 서버로 요청 쏘는거니까...

## ImageButton 컨트롤

페이지를 로드할 떄 이미지 경로를 수정할 수 있으므로 동적으로 이미지가 바뀌는 컨트롤을 만들 수 있음

## 파라미터들...

```c#
        protected void Page_Load(object sender, EventArgs e)
        {
            //
        }
        protected void btnImage_Click(object sender, ImageClickEventArgs e)
        {
          	//sender 는 ID가 btnImage 인 ASP 컨트롤
          	//e.X , e.Y 처럼 현재 클릭한 이미지버튼의 좌표같은 속성에 접근할 수 있음
        }
```

### sender

sender(전달자)는 그냥 현재 이벤트핸들러를 호출한 객체를 뜻한다.

그러므로 버튼클릭 이벤트라면 그 버튼이 전달자다

버튼 클래스가 있고 매핑이 되는거라고 보면 된다( System.Web.UI.WebControls.Button)

> ❓`Page_Load()` 의 전달자는 뭘까??

### XXXEventArgs

XXXEventArgs 클래스형 매개 변수는 현재 시점에서 필요한 추가 정보 제공