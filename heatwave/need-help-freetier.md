# 도움이 필요할 경우

## 세션 소개
이 페이지는 LiveLab에서 사용자가 직면하는 몇 가지 일반적인 문제를 해결하는 데 도움을 주기 위해 설계되었습니다.

문제 해결 팁을 읽은 후에도 여전히 문제가 있거나 워크숍에 대한 문제를 보고하고 싶다면 오른쪽 상단 모서리에 있는 물음표 아이콘을 클릭하여 이메일을 통해 LiveLabs 팀에 직접 문의하세요.

![Help button](https://github.com/user-attachments/assets/2d46fe0d-355b-477b-96f3-089f9a43eeae)


이메일을 사용하여 지원을 받는 방법에 대한 자세한 내용은, [here](#HowtoFormatYourSupportEmailRequest)를 클릭.

### 일반적인 문제 목차
  - [Connectivity Issues?](#ConnectivityIssues?)
  - [Cannot Create Passwords for Database Users?](#CannotCreatePasswordsforDatabaseUsers?)
  - [Cannot find Groups under Identity and Security in my tenancy?](#CannotfindGroupsunderIdentityandSecurityinmytenancy?)

## 이메일을 사용한 Workshop에 내용 Support 요청
아래처럼 기본 메일 애플리케이션에서 LiveLabs 지원 받은 편지함에 자동으로 채워지는 이메일이 생성되고 제목 줄에 현재 워크숍도 포함됩니다. 아래 단계에 따라 문의하여 문제에 대한 빠른 해결책을 얻으세요.

1. 제목란에 **Workshop 이름**을 입력해 주세요(예 참조).
    ![Email](https://github.com/user-attachments/assets/5058b650-2aec-4af0-af78-60d27313de98)

2. 문제가 발생한 **Lab 번호**, **Task 번호**, **Step 번호**를 포함합니다. 또한 이 워크숍을 운영하는 **환경**(귀하의 테넌시 또는 LiveLabs 샌드박스 테넌시)도 포함합니다.

3. 이메일 내용에 **문제**에 대한 설명과 관련 정보를 포함하세요.

4. **스크린샷**과 시도한 **문제 해결 단계**를 첨부하면 문제를 재현하여 시기적절하고 정확한 해결책을 제공할 수 있습니다.

## Connectivity Issues?

**VPN**, **Corporate Network**에 연결되어 있나요?, 아니면 엄격한 **방화벽** 뒤에 있나요?

이 세 가지 조건 중 하나라도 해당되면 네트워크의 일부 포트가 트래픽에 대해 닫힐 수 있습니다.

웹 브라우저와 Oracle Analytics Tool과 같은 애플리케이션에서 데이터베이스 작업을 통해 데이터를 업로드하는 경우 제한이 있을 수 있으며 "Hang"되거나 멈춘 것처럼 보일 수 있습니다.

no VNC 워크숍에 연결하는 동안 "Hmmm... 이 페이지에 접근할 수 없습니다" 오류가 발생하고 워크숍에 접속하지 못할 수 있습니다.

환경에 다시 액세스하려면 다음 옵션을 시도하세요.

1. VPN 연결을 끊은 후 다시 시도해 보세요.

2. 회사 네트워크에 연결되어 있다면 허용된다면 공용 네트워크나 '일반' 네트워크로 전환해보세요.

3. 브라우저에 광고 차단 기능이 설정되어 있다면 이를 확인하고 비활성화하세요.

4. 현재 사용 중인 브라우저가 아닌 다른 브라우저에서 워크숍을 실행해 보세요.

5. noVNC 워크숍의 경우 6080 포트를 열 수 있는지 확인하세요.

6. 다른 표준 시나리오의 경우 80, 443, 22(ssh용) 등의 포트를 열 수 있는지 확인하세요.

7. 또는 IT 관리자에게 문의하여 네트워크나 방화벽에 예외를 추가하는 것이 가능한지 확인하세요.

## Cannot Create Passwords for Database Users?

1. 입력하는 비밀번호가 다음 조건을 만족하는지 확인하세요.[restrictions](https://docs.oracle.com/en/cloud/saas/marketing/responsys-user/Account_PasswordRestrictions.htm).

## Cannot find Groups under Identity and Security in my tenancy?

1. 탐색 메뉴에서, **Identity & Security** 클릭, **Domains** under **Identity** 아래 **Domains** 선택.

  ![Select Domains](https://github.com/user-attachments/assets/200af26f-f87a-42b5-9212-b2f6fc399acb " ")

2. 올바른 compartment에 있는지 확인하고 **기본값(Current domain)**을 클릭하세요.

  ![Click Default](https://github.com/user-attachments/assets/9f62c8de-858c-44c0-832f-99758375d3b9 " ")

3. 왼쪽의 ID 도메인 섹션에서 **그룹**을 클릭하여 그룹에 액세스합니다.

  ![Click Groups](https://github.com/user-attachments/assets/2baaef4d-32ff-4180-b92c-db77b7989df8 " ")

## Service request(SR) 하는 방법
1. oracle support 사이트에 접속하여 가입을 합니다. [support site](https://support.oracle.com)     
2. oci 콘솔에서 아래 버튼을 클릭하여 SR 요청을 합니다. (처음일 경우 1번에 가입한 계정과 연결 하셔야 합니다.)    
   ![image](https://github.com/user-attachments/assets/5f34059b-dbe7-4f52-a6af-e52493f4b59a)    
3. 2번에 클릭후 나타나는 화면에서 아래 **Create support Request** 버튼을 클릭하여 chatbot에 채팅 후, service request 작성합니다.
   ![image](https://github.com/user-attachments/assets/dc3ba392-c14f-4beb-9e9d-c9cfe36663a9)     
   ![image](https://github.com/user-attachments/assets/c40130cd-e022-495b-b1d3-618d7ab7eee8)   


## Acknowledgements
* **Author** - LiveLabs Team
* **Last Updated By/Date** - Kihyuk, July 2024
