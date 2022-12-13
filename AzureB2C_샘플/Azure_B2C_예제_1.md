# 블레이저 웹 어셈블리에서 AAD B2C 설정 - 1
> Azure Active Directory B2C는 주로 사용자의 소셜 ID나 이메일 또는 로컬 계정을 이용해 비지니스 고객 ID로 사용하며 인증할 수 있도록 하는 서비스이다. 자세한건   [공식문서](https://learn.microsoft.com/ko-kr/azure/active-directory-b2c/overview)에서 확인하는 것이 좋다. 해당 서비스를 사용하기 위해서는 Azure 계정과 디렉터리를 생성할 수 있는 권한이 있어야한다. 이번에는 Azure Web Assembly에서 로그인할 수 있도록 생성해 본다.



## Azure Active Directory B2C 테넌트 생성
> 고객을 관리하기 위한 별도 테넌트를 생성해 관리하게 된다. 우선 테넌트를 생성하는 방법에 대해 알아본다.

1. Azure 포탈에 들어가 리소스 생성 -> Azure Active Directory B2C '만들기' 선택<br><br>![화면 캡처 2022-11-23 115232](https://user-images.githubusercontent.com/39551265/203460865-89f0338c-bef9-4050-9ff8-348793d20d54.png)<br>

2. <span style="color:red">새 Azure AD B2C 테넌트 만들기</span> 선택<br><br>![화면 캡처 2022-11-24 113117](https://user-images.githubusercontent.com/39551265/203691875-64da3060-5db7-429e-96da-0e9a5c09088a.png)<br>

3. 필수 입력항목을 입력 후 '만들기' 테넌트를 생성한다.<br><br>![화면 캡처 2022-11-24 132543](https://user-images.githubusercontent.com/39551265/203697996-af60ae24-7978-4008-bb50-b50529597538.png)<br>

4. 생성한 B2C 테넌트 리소스를 연다. 그 후 <span style="color:red">Open B2C Tenant</span> 를 클릭(클릭하면 새로 생성한 테넌트로 이동하게 된다. 이후부터는 새로 생성한 테넌트에서 작업이 이루어진다.)<br><br>![화면 캡처 2022-11-24 140709](https://user-images.githubusercontent.com/39551265/203698798-c164e797-8ad6-4b1f-8690-71c0b0df2870.png)<br>

## 앱 등록

1. '앱 등록' 메뉴를 열고 <span style="color:red">+ 새 등록</span>을 클릭<br><br>![화면 캡처 2022-11-24 144538](https://user-images.githubusercontent.com/39551265/203703680-6b208bb5-7fae-4ff8-b117-ec083e827152.png)<br>

2. 등록할 애플리케이션 '이름' 항목을 입력 후 '지원되는 계정 허용', '권한'을 체크하고 <span style="color:red">등록</span>한다.(기본값으로 체크되어있다.) <br><br>![화면 캡처 2022-11-22 102503](https://user-images.githubusercontent.com/39551265/203460935-ed5a9228-1f9f-424a-bc27-ad643a4935ae.png)<br>

3. 새로 등록한 애플리케이션의 항목으로 들어왔을 것이다. 이곳에서 'API 표시' 메뉴를 연다. 이후 <span style="color:red">+ 범위 추가</span> 클릭. 이후 오른쪽에 나오는 '추가 범위' 에서 <span style="color:red">저장 후 계속</span>을 선택한다.<br><br>![화면 캡처 2022-11-22 105628](https://user-images.githubusercontent.com/39551265/203460929-4aaf52f4-f2ee-4e07-a2c5-46eacd32106b.png)<br>

4. '범위 이름' 항목에 인증을 위한 API 이름을 입력한다. 이후 어플리케이선 ID URL/{범위 이름}으로 B2C인증을 위한 URL로 설정된다. '관리자 동의 표시 이름' 항목에는 해당 범위의 표시할 이름을 입력한다. '관리자 동의 설명'에는 해당 범위의 설명을 입력한다.<br><br>![화면 캡처 2022-11-22 112608](https://user-images.githubusercontent.com/39551265/203460920-13138779-2e70-4692-bb68-c37120059881.png)<br>

5. 이후 API 권한이 새로 생성되었을 것이다. 생성된 권한 오른쪽에 '관리자 동의가 필요함'이 예로 되어 있을텐데 상단의 <span style="color:red">~ 에 대한 관리자 동의 허용</span> 을 클릭<br><br>![화면 캡처 2022-11-22 143846](https://user-images.githubusercontent.com/39551265/203722526-0e800333-8545-48d1-89bc-aa46cb87b430.png)<br>

>여기까지는 Azure AAD B2C 웹 어셈블리의 서버를 위한 작업이 끝났다 다음 문서에서는 블레이저 WASM 프로젝트를 만들고 클라이언트에 대한 등록에 대해 설명한다.