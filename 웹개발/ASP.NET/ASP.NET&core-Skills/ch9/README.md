# 9장. 웹 폼 사용자 정의 컨트롤과 마스터 페이지

> 페이지 레이아웃 구성에 쓰이는 요소들에 대한 내용이다

## 웹 폼 사용자 정의 컨트롤

* 웹 페이지에서 반복 사용되는 부분을 따로 파일로 구성해 사이트 제작의 효율성을 높여줌

* 확장자명은 .ascx

* 웹 폼에 올라갈 부분 페이지를 나타냄

  즉, 웹 폼안에 포함되어야만 실행이 된다	

```c#
<%@ Master Lanuage="C#"  ...%>
<%@ Register TagPrefix="uc1" TagName="이름" src="~/사용자정의 컨트롤.ascx" %>

<uc1:이름 ID="gadget" runat="server" />
		<!--
			사용자정의 컨트롤.ascx 의 소스로 대체됨
		-->
```

* 위의 예문은 사용자 정의 컨트롤(.ascx) 을 사용하는 웹 폼(aspx) 파일 내의 코드영역임
* 그러므로 aspx 소스의  `<uc1:이름 ID="gadget" runat="server" />`  이 태그가 .ascx 파일의 소스로 대체되어 브라우저에 뿌려짐

## 마스터 페이지

> 웹 페이지 전체에 공통적으로 사용되는 뼈대를 구성할 때 사용할 수 있다
>
> ASP.NET MVC 에서는 레이아웃(Layout)으로 마스터 페이지 기능을 구현함

* 웹 사이트의 개별 페이지들이 동일한 룩앤필을 제공하기 위해 사용됨

```C#
<%@ Master Lanuage="C#" MasterPageFile="~/최상단마스터.master" ...%>
		<!--
			최상단마스터.master 의 하위 페이지인 중간 마스터페이지임
			즉, 이 페이지의 하위에 페이지가 또 있을 수 있음
		-->
<asp:Content ID="Content1" ContentPlaceHolderID="cphHeader" runat="Server">
		<!--
			이 페이지의 영역
			최상단마스터.master 페이지에 ID가 cphHeader인 ContentPlaceHolder 컨트롤이 있음
			최상단마스터.master 의 cphHeader 가 이 문서에서 작성된 코드로 바뀜
		-->
	<asp:ContentPlaceHolder ID="cphHeader" runat="server">
		<!--
			이 페이지의 하위 페이지 소스 영역
			따라서 이 문서에서 이 영역에 소스를 코딩해도 아무것도 출력되지 않음			
		-->
	</asp:ContentPlaceHolder>
</asp:Content>
```

* 위의 소스코드는 마스터 페이지가 다른 마스터 페이지를 사용하고 있는 형태임
* aspx파일 상단에 마스터 페이지를 사용하겠다는 지시문을 작성`MasterPageFile=""` 
* `<asp:Content>` 태그 안쪽 영역
  * 상단 지시문의 마스터 페이지에 적용될 소스를 작성하는 부분
  * 즉, 여기에 코드를 작성해야 코드가 적용됨
* `<asp:ContentPlaceHolder>` 
  * 이 마스터 페이지를 사용하는 하위 페이지 소스 영역
  * 여기에 코드를 작성하더라도 하위 페이지(aspx 또는 mater)의 소스코드로 대체되기 때문에 그 코드는 적용되지 않음

### 공통점과 차이점

* 공통점

  * 아무튼 둘 다 aspx파일을 실행시킴

* 차이점

  * 사용자 정의 컨트롤에서는 aspx파일에 사용자 정의 컨트롤의 소스가 들어올 영역을 잡아놓음

    (위 코드의 `<uc1:이름 ID="gadget" runat="server" />`)

  * 반대로 마스터 페이지는 .master에 영역을 잡아놓고 aspx파일의 소스가 마스터 페이지에 적용되는 형태

  * 또한 여러 마스터 페이지를 둬서 마스터 페이지의 마스터 페이지 같은 계층형태로 구성할 수 있음 