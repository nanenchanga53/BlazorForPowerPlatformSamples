# 블레이저 웹 어셈블리에서 AAD B2C 설정 - 2
> [블레이저 웹 어셈블리에서 AAD B2C 설정 - 1](https://nanenchanga.tistory.com/entry/%EB%B8%94%EB%A0%88%EC%9D%B4%EC%A0%80-%EC%9B%B9-%EC%96%B4%EC%85%88%EB%B8%94%EB%A6%AC%EC%97%90%EC%84%9C-AAD-B2C-%EC%84%A4%EC%A0%95-1) 에서 이어진다.



## Balzor Web Assembly 프로젝트 생성

1. Visual Studio를 켜서(Visual Studio 2022 기준) '새 프로젝트 만들기' 화면에서 Blazor WebAssembly앱을 선택 후 '다음'<br><br>![화면 캡처 2022-11-22 134624](https://user-images.githubusercontent.com/39551265/203460913-a67a3f8d-7ada-465d-a79b-964bcba7e785.png)<br>

2. '인증 유형'을 <span style="color:red">Microsoft ID 플랫폼</span>을 선택한다.  이후 ASP.NET Core 호스팅을 체크한다.(해당 체크를 하면 클라이언트와 통신 인증이 미리 정의된 Server를 담당할 .NET 프로젝트가 생성된다. 만약 별도의 서버(Django 등)를 사용하려면 그것에 맞는 인증방법에 대해 알아봐야 할 것이다.)<br><br>![화면 캡처 2022-11-22 134742](https://user-images.githubusercontent.com/39551265/203460906-bef32abe-0410-496d-9191-379ac98efabc.png)<br>

3. 필수 구성요소를 확인 후 '다음'을 클릭<br><br>![화면 캡처 2022-11-22 134800](https://user-images.githubusercontent.com/39551265/203460903-ef948416-0917-4752-8199-76b0b561e0c3.png)<br>

4. 우선 이전 문서에서 테넌트를 생성한 ID로 로그인과 선택이 되어있는 것을 확인후 '테넌트'를 선택한다. 이후 테넌트에서 생성된 애플리케이션 리스트가 보일 것인데 이전 문서에서 생성한 애플리케이션을 선택 후 '다음'을 클릭<br><br>![화면 캡처 2022-11-22 134935](https://user-images.githubusercontent.com/39551265/203460898-9c068f16-579b-4fb1-b59d-b3a061741b6a.png)<br>

5. 이후에는 따로 선택할 것 없이 '마침'을 클릭하면 구성요소가 프로젝트에 설치된다.

## B2C 애플리케이션 클라이언트 설정
1. Azure 포탈에서 이전 문서에서 생성한 Azure AD B2C 테넌트에 접속한다.

2. '앱 등록' 메뉴를 열고 '새로고침'을 한번 한다. 이후 이전에 만들었던 애플리케이션 외에 똑같은 이름에 '-Client'가 붙어있는 애플리케이션이 생성된 것을 확인 가능하다. 해당 애플리케이션을 클릭한다.<br><br>![화면 캡처 2022-11-25 112422](https://user-images.githubusercontent.com/39551265/203888350-b9538435-d085-45f8-81f5-6883441b8087.png)<br>

3. '인증' 메뉴로 넘어가면 '플랫폼 구성'의 '단일 페이지 애플리케이션'에 리디렉션 URI가 기재되어 있을 것이다. 이곳에서 각각 중간에 authentication을 추가해 `https://localhsot:포트번호/authentication/login-callback`형식으로 변경한다.<br><br>![화면 캡처 2022-11-25 131904](https://user-images.githubusercontent.com/39551265/203901057-999ac831-a8a8-42af-86ac-5460e0fded02.png)<br>

## 로그인/회원가입 사용자 흐름 생성
1. Azure AD B2C 테넌트로 돌아와서 '사용자 흐름' 메뉴에 들어와 <span style="color:red">+ 새 사용자 흐름</span> 클릭<br><br>![화면 캡처 2022-11-25 143118](https://user-images.githubusercontent.com/39551265/203909988-8cd0ec55-59dd-4763-8510-f7f3699d23b3.png)<br>

2. 사용자 흐름 형식 선택'에서 <span style="color:red">등록 및 로그인</span>을 선택후 '만들기' 클릭<br><br>![화면 캡처 2022-11-25 150559](https://user-images.githubusercontent.com/39551265/203912035-9a730ba4-3a0d-472a-9afe-8cda55b77225.png)<br>

3. '이름' 항목에 해당 회원가입 흐름의 이름을 입력하고 필자의 경우에는(signupsignin1)  ID공급자를 선택한다.<br><br>![화면 캡처 2022-11-25 161859](https://user-images.githubusercontent.com/39551265/203923405-a8b7e8a3-104d-4e91-a317-dc7e19fa595b.png)<br>

4. '사용자 특성 및 토큰 클레임' 항목에서 '자세히 표시'를 클릭한다. '특성 수집' 항목에서는 회원 가입시 필수로 입력하게될 항목을 선택한다. '클레임 반환'은 사용자 로그인시 반환될 클레임값을 선택한다. 최소한 이메일 주소, 표시 이름 정도는 전부 체크하는 것이 좋다.<br><br>![화면 캡처 2022-11-25 163346](https://user-images.githubusercontent.com/39551265/203925835-ae40c8e9-a1b9-4a85-9747-80da7a85b5ff.png)<br>

5. 전부 체크되었으면 '만들기' 클릭


6. 해당 사용자 흐름이 만들어진 것을 확인한다.<br><br>![화면 캡처 2022-11-25 164303](https://user-images.githubusercontent.com/39551265/203927387-da9673da-49b7-4242-8392-9f45c23b86bf.png)<br>


> 여기까지는 Azure AAD B2C 웹 어셈블리의 클라이언트에서 회원가입과 로그인이 가능한 작업까지 끝났다. 다음 문서에서는 블레이저 WASM 프로젝트의 웹 세팅을 변경하여 해당 B2C서비스를 사용할 수 있도록 설정한다.