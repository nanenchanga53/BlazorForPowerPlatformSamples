# 블레이저 웹 어셈블리에서 AAD B2C 설정 - 3
> [블레이저 웹 어셈블리에서 AAD B2C 설정 - 2](https://nanenchanga.tistory.com/entry/%EB%B8%94%EB%A0%88%EC%9D%B4%EC%A0%80-%EC%9B%B9-%EC%96%B4%EC%85%88%EB%B8%94%EB%A6%AC%EC%97%90%EC%84%9C-AAD-B2C-%EC%84%A4%EC%A0%95-2) 에서 이어진다.



## Blazor 클라이언트 프로젝트 설정 변경

1. Visual Studio로 생성했었던 Blazor 솔루션을 연다. 그 후 클라이언트 프로젝트의 세팅값을 설정해야한다.

2. 클라이언트 프로젝트의 wwwroot/appsettings.json 파일을 연다.<br><br>![화면 캡처 2022-11-29 183128](https://user-images.githubusercontent.com/39551265/204491993-4f005dc8-766c-4319-bb09-a929eeb8c288.png)<br>

3. 클라이언트 세팅값을 각각 복사한다.<br><br>Azure AD B2C 테넌트에서 도메인명을 복사한다.<br>![화면 캡처 2022-11-29 184007](https://user-images.githubusercontent.com/39551265/204495126-94f15bd4-5143-4a95-a950-d454de35ca44.png)
<br>클라이언트 앱을 열어 애플리케이션(클라이언트 ID)를 복사한다.<br>![화면 캡처 2022-11-29 183747](https://user-images.githubusercontent.com/39551265/204495142-38c519d8-1316-4b6a-9c10-7e4416cd740e.png)<br>API 사용 권한의 API/권한이름을 복사한다.<br>![화면 캡처 2022-11-29 195806](https://user-images.githubusercontent.com/39551265/204512273-b295d723-53f3-4764-bb23-c73303356ed5.png)<br>사용자 흐름 등록 및 로그인의 이름을 복사한다.<br>
![화면 캡처 2022-11-29 184622](https://user-images.githubusercontent.com/39551265/204495315-73eb27e3-374b-4e7e-821d-96010896350f.png)

4. appsettings.json에 다음과 같은 형식으로 입력한다.(기본값으로 빠진 부분만 입력하자)

```json

{
  "AzureAd": {
    "ClientId": "{Azure AD B2C 클라이언트 앱 ClientID}",
    "Authority": "https://{도메인명}.b2clogin.com/{테넌트 도메인}/{사용자 흐름 등록 및 로그인 명}",
    "ValidateAuthority": true
  },
  "ServerApi": {
    "BaseUrl": "https://{도메인명}.onmicrosoft.com/{API 호출권한 기본값}",
    "Scopes": "https://{도메인명}.onmicrosoft.com/{API 호출권한 기본값}/{API/권한 이름(예 : API.Access)}"
  }
}

```

## Blazor 서버 프로젝트 설정 변경

1. Visual Studio로 생성했었던 Blazor 솔루션을 연다. 그후 서버 프로젝트의 세팅값을 설정해야한다.

2. 서버 프로젝트의 wwwroot/appsettings.json 파일을 연다.<br><br>![화면 캡처 2022-11-30 104326](https://user-images.githubusercontent.com/39551265/204688695-6c6a6673-c5fc-447f-a514-fdc8f16fae2f.png)<br>

3. 서버 세팅값을 각각 복사한다.<br><br>Azure AD B2C 테넌트에서 도메인명을 복사한다.<br>![화면 캡처 2022-11-29 184007](https://user-images.githubusercontent.com/39551265/204495126-94f15bd4-5143-4a95-a950-d454de35ca44.png)
<br>서버 앱을 열어 애플리케이션(클라이언트 ID)를 복사한다.<br>![화면 캡처 2022-11-29 183747](https://user-images.githubusercontent.com/39551265/204495142-38c519d8-1316-4b6a-9c10-7e4416cd740e.png)<br>API 사용 권한의 API/권한이름을 복사한다.<br>![화면 캡처 2022-11-29 195806](https://user-images.githubusercontent.com/39551265/204512273-b295d723-53f3-4764-bb23-c73303356ed5.png)<br>사용자 흐름 등록 및 로그인의 이름을 복사한다.<br>
![화면 캡처 2022-11-29 184622](https://user-images.githubusercontent.com/39551265/204495315-73eb27e3-374b-4e7e-821d-96010896350f.png)

4. appsettings.json에 다음과 같은 형식으로 입력한다.(기본값으로 빠진 부분만 입력하자)

```json

{
  "AzureAd": {
    "Instance": "https://{도메인명}.b2clogin.com/",
    "Domain": "{도메인 주소}",
    "TenantId": "{테넌트 ID}",
    "ClientId": "{서버앱 클라이언트 ID}",
    "CallbackPath": "/signin-oidc",
    "Scopes": "{API/권한 이름(예 : API.Access)}",
    "SignUpSignInPolicyId": "{사용자 흐름 등록 및 로그인 명}",
    "ClientSecret": "Client secret from app-registration. Check user secrets/azure portal.",
    "ClientCertificates": []
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}

```

## 실행, 회원가입 확인

1. 프로젝트를 실행하여 <span style="color:blue">Login</span>을 클릭한다.<br><br>![화면 캡처 2022-11-30 112827](https://user-images.githubusercontent.com/39551265/204692905-c048a746-e33b-4033-90cd-77b3b846cba4.png)<br>

2. 로그인 버튼 아래쪽에 '등록' 버튼이 있다. 회원가입화면으로 넘어가니 클릭하자. 회원가입화면에서 '이메일주소'를 입력하고 '확인코드 보내기'를 통해 이메일로 받은 코드를 인증한다.<br><br>![화면 캡처 2022-11-30 113033](https://user-images.githubusercontent.com/39551265/204705269-519b6177-be26-43cb-adfa-63bebc6b08c6.png)<br>

3. 이후 사용자 흐름에서 정한 등록시 입력할 항목들을 채우고 회원가입을 한다.

4. 이후 로그인시 상단에 등록한 이름이 표시되며 'Fetch Data' 메뉴가 접속되고 데이터를 불러오는지 확인한다.<br><br>![화면 캡처 2022-11-30 133028](https://user-images.githubusercontent.com/39551265/204707948-8e139d1b-d881-4fcd-815e-f544e3ce1fe4.png)<br>

5. Azure AD B2C 테넌트의 '사용자' 메뉴를 확인하여 회원가입시 등록한 사용자가 추가된 것을 확인한다.<br><br>![화면 캡처 2022-11-30 133505](https://user-images.githubusercontent.com/39551265/204708459-558d1131-8569-45a7-812a-6b0db60e99d3.png)<br>