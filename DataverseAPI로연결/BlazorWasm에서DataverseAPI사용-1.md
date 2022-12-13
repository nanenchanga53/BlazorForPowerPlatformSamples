# Blazor Wasm 에서 Dataverse API 연결
> 블레이저 웹 어셈블리에서 Dataverse를 서버로서 사용하는 방법에 대해 알아본다. Dataverse API를 사용하고 Azure AD를 통해 인증을 실행한다.

## Azure AD에서 앱 등록 만들기

1. Power Platform [관리센터](https://admin.powerplatform.microsoft.com/) 에서 <span style="color:red">Azure Active Directory</span> 를 클릭해 접속한다. <br><br>![image](https://user-images.githubusercontent.com/39551265/174248733-66214cd1-c73c-4fbc-a24f-0c90ef0c93b2.png)<br>

2. <span style="color:red">앱 등록</span> 메뉴로 들어와 <span style="color:red">+ 새 등록</span>을 클릭<br><br>![image](https://user-images.githubusercontent.com/39551265/174249798-1ce0c042-0080-4a7a-89e7-b461c46a5ad8.png)<br>

3. '애플리케이션 이름' 항목에서 해당 앱을 등록할 이름을 입력한다.<br>'지원되는 계정 유형' 항목에서 엑세스 가능한 영역을 선택한다.<br>리디렉션 URI는 Web을 선택 후 적당한 URL을 입력한다. <span style="color:red">등록</span> 클릭<br><br>![image](https://user-images.githubusercontent.com/39551265/174253040-d5e4cc33-b809-472f-98eb-1306301b1388.png)<br>

4. 'API 사용 권한' 메뉴로 들어와 <span style="color:Red">+ 권한 추가</span> 클릭<br><br>![image](https://user-images.githubusercontent.com/39551265/174484418-20178365-3f68-4701-a433-5f320fbce958.png)<br>

5. 'API 사용 권한 요청'에서 <span style="color:red">Dynamics CRM</span> 클릭<br><br>![image](https://user-images.githubusercontent.com/39551265/174484521-8fe2a809-1028-4458-a2a7-551c91e6f7b2.png)<br>

6. 'API 사용 권한 요청'에서 <span style="color:Red">권한을 체크</span>하고 <span style="color:red">권한 추가</span> 클릭<br><br>![image](https://user-images.githubusercontent.com/39551265/174484565-f5a295f0-84b0-49e9-a1ee-3cec8577406a.png)<br>

7. 이후 API 권한이 새로 생성되었을 것이다. 생성된 권한 오른쪽에 '관리자 동의가 필요함'이 예로 되어 있을텐데 상단의 <span style="color:red">~ 에 대한 관리자 동의 허용</span> 을 클릭<br><br>![화면 캡처 2022-11-22 143846](https://user-images.githubusercontent.com/39551265/203722526-0e800333-8545-48d1-89bc-aa46cb87b430.png)<br>

# Blazor WASM 프로젝트 생성
1. Visual Studio를 켜서(Visual Studio 2022 기준) '새 프로젝트 만들기' 화면에서 Blazor WebAssembly앱을 선택 후 '다음'<br><br>![화면 캡처 2022-11-22 134624](https://user-images.githubusercontent.com/39551265/203460913-a67a3f8d-7ada-465d-a79b-964bcba7e785.png)<br>

2. 프로젝트 위치를 결정 후 '다음'으로 넘거가면. '추가 정보' 화면에서 '인증 유형'을 <span style="color:red">Microsoft ID 플랫폼</span>을 선택한다. 그 후 <span style="color:red">만들기</spn><br><br>![image](https://user-images.githubusercontent.com/39551265/206653133-f078b751-3c04-4119-bfad-e05095b06a23.png)<br>

3. 필수 구성요소를 확인 후 '다음'을 클릭<br><br>![화면 캡처 2022-11-22 134800](https://user-images.githubusercontent.com/39551265/203460903-ef948416-0917-4752-8199-76b0b561e0c3.png)<br>

4. 우선 이전 문서에서 테넌트를 생성한 ID로 로그인과 선택이 되어있는 것을 확인후 '테넌트'를 선택한다. 이후 테넌트에서 생성된 애플리케이션 리스트가 보일 것인데 이전 문서에서 생성한 애플리케이션을 선택 후 '다음'을 클릭<br><br>![화면 캡처 2022-11-22 134935](https://user-images.githubusercontent.com/39551265/203460898-9c068f16-579b-4fb1-b59d-b3a061741b6a.png)<br>

5. 이후에는 따로 선택할 것 없이 '마침'을 클릭하면 구성요소가 프로젝트에 설치된다.

6. 프로젝트를 실행해본다. 이후 로그인을 버튼을 눌러 로그인이 되는지 확인한다.(로그인이 가능한건 등록한 Azure AD의 디렉토리에 등록된 ID들이다.)

7. Fetch Data 목록에 접속이 되는지 확인되면 Azure AD에 제대로 연결된 것이다.

> 여기까지는 Azure AD 사용할 수 있도록 설정하였다. 다음에는 Dataverse와 연결된 페이지를 작성해 보겠다.