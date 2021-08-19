# 11장. ASP.NET 상태 관리 기법 소개

> 필요한 데이터를 임시 또는 반영구적으로 서버 또는 클라이언트에 보관하고 사용하는 방법



## 📌상태 관리 기법(State Management)

### 클라이언트 측 상태 관리 기법

* Hidden Field
* View State
  * 사용 개체: ViewState
  * 설명: 해당 웹 페이지 내에서만 어떤 정보를 입시로 보관하고자 할 때 사용
* Cookies
  * 사용 개체: HttpCookie(Cookie)
  * 설명: 클라이언트 측 웹 브라우저에 간단한 데이터를 보관해 서버 성능을 향상시킴
* Control State
* Query Strings
  * 사용 개체: QueryString
  * 설명: 현재 페이지에서 다음 페이지로 간단한 정보를 전달할 때 사용

### 서버 측 상태 관리 기법

* Session
  * 사용 개체: Session
  * 설명: 전체 웹 사이트 내에서 현재 사용자에게만 제공되는 데이터를 저장할 때 사용
* Application 
  * 사용 개체: Application
  * 설명: 해당 웹 사이트 내에서 공유되어야할 데이터를 저장하는데 사용


* Cache
  * 사용 개체: Cache
  * 설명: 서버 측 메모리에 데이터를 보관해 응답 속도를 향상시킬 수 있음

>❓위의 설명들이 정확한지 잘 모르겠음
>
>아무튼 대략적인 개요가 그렇다

