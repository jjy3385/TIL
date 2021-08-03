# 6장과 7장. HTML 태그를 대체하는 표준 컨트,ASP.NET 리치 표준 컨트롤

>  6장(HTML 태그를 대체하는 표준컨트롤)이나 7장(ASP.NET 리치 표준 컨트롤)이나 컨트롤들을 나열해서 설명하고 있음
>
> 굳이 다 정리할 필요는 없고 그때 그때 찾아서 사용하면 될듯
>
> 📌각 표준 컨트롤들이 브라우저에선 aspx 태그 형태 그대로 표현되는 것이 아니라  HTML 태그로 표현된다는 것임

## DropDownList 컨트롤

콤보박스 만드는 컨트롤임

HTML태그는 `<select/>` 와 `<option/>` 

aspx파일에서 `<asp:DropDownList />` 태그와` <asp:ListItem/>` 태그를 써서 정적으로 구성할 수도 있지만 cs단에서 동적으로 구성할 수도 있음 

[예제1 - 정적](https://github.com/jjy3385/ASP.NET-CoreSkills/blob/main/DevStandardControl/FrmDropDownList.aspx)

[예제2 - 동적](https://github.com/jjy3385/ASP.NET-CoreSkills/blob/main/DevStandardControl/FrmDropDownListDynamicCreation.aspx.cs)

## XML 컨트롤

```C#
<asp:Xml ID="xmlCompany" runat="server" DocumentSource="~/FrmXml.xml" TransformSource="~/FrmXml.xsl">
```

`DocumentSource` 속성과 `TransformSource` 속성이 각각 xml 과 xsl 파일을 참조하고 있음

xml은 뭔지 대충 알겠는데 xsl는 모르겠음

최근에는 JSON 을 더 많이 사용한다고 하는데 ....나는 아직...XML만 쓰는 환경에서만 일해봄

## 📌PlaceHolder 컨트롤

이 컨트롤은 실무에서도 꽤 보이는 듯

```C#
//PlaceHolder에 프로그래밍 방식으로 버튼 추가
PlaceHolder컨트롤ID.Controls.Add(컨트롤변수명);
//부모 컨트롤(컨테이너)로부터 자식 컨트롤을 읽어오는 코드
lblDisplay.Text = ((타입)PlaceHolder컨트롤ID.Find(컨트롤변수명.ID)).Text
```

[예제](https://github.com/jjy3385/ASP.NET-CoreSkills/blob/main/DevStandardControl/FrmPlaceHolder.aspx.cs)



