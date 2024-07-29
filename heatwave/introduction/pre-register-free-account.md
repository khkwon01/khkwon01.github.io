# 시작 - Free Tier account 등록

## 세션 소개

시작하기 전에 Oracle Cloud 계정이 필요합니다. 이 랩은 Oracle Cloud Free Tier 계정을 얻고 로그인하는 단계를 안내합니다.

Estimated Time: 5 minutes 소요

### 기존 클라우드 계정

이미 Oracle Cloud 계정에 대한 액세스 권한이 있는 경우 **작업 2**로 건너뛰어 클라우드 테넌시에 로그인하세요.

### 목표

- Oracle Cloud Free Tier 계정 생성
- 귀하의 계정에 로그인하세요

### Prerequisites (요구조건)

* 유효한 email address
* 이메일이 인식되지 않는 경우에만 SMS text verification 코드가 필요함

> **참고**: 다음 스크린샷에 나와 있는 인터페이스는 실제로 볼 수 있는 인터페이스와 다를 수 있습니다.

## 작업 1: Free Trial Account 생성

이미 클라우드 계정이 있는 경우 **작업 2**로 넘어가세요.

1. Oracle Cloud 계정 등록 양식에 액세스하려면 웹 브라우저를 엽니다 : [oracle.com/cloud/free](![image](https://github.com/user-attachments/assets/e37916d7-f1eb-41fa-ab60-75a9ee7eed70)).

   등록 페이지가 나타납니다.
       ![image](https://github.com/user-attachments/assets/4273af51-dd3d-4b40-9cee-30cebfcb8d07 " ")
2.  Oracle Cloud Free Tier 계정을 만들려면 다음 정보를 입력하세요.
    * Choose your **Country**
    * Enter your **Name** and **Email**
    * hCaptcha를 사용하여 신원을 확인하세요


3. 유효한 이메일 주소를 입력한 후 Verify my email 버튼을 선택합니다. 버튼을 선택하면 다음과 같은 화면이 나타납니다.
       ![Verify Email](https://github.com/user-attachments/assets/3b291f8b-54be-4e11-88cd-436dbae508b7 " ")

4. 이메일로 이동하세요. 받은 편지함에 Oracle의 계정 검증 이메일이 표시됩니다. 이메일은 다음과 유사합니다.
       ![Verification Mail](https://github.com/user-attachments/assets/ec4a8245-db40-4ebe-86e7-1de9686440bf " ")

5. **이메일 확인**을 클릭하세요.

6. Oracle Cloud Free Tier 계정을 만들려면 다음 정보를 입력하세요.
    - Choose a **Password**
    - Enter your **Company Name**
    - **클라우드 계정 이름**은 입력 내용에 따라 자동으로 생성됩니다. 새 값을 입력하여 이름을 변경할 수 있습니다. 작성한 내용을 기억하세요. 나중에 로그인할 때 이 이름이 필요합니다.
    - **Home Region**을 선택하세요. 가입 후에는 홈 지역을 변경할 수 없습니다.
    >**참고:** 현재 워크숍 설계와 리소스 가용성을 토대로 볼 때, 현재로서는 이 워크숍에 런던 지역을 사용하지 않는 것이 좋습니다.
    - **계속**을 클릭하세요
    ![Account Info](https://github.com/user-attachments/assets/68533442-3ae5-42e6-b3cf-2bbfb4d71a08 " ")

7. 주소 정보를 입력하세요. 국가를 선택하고 전화번호를 입력하세요. **계속**을 클릭하세요.
          ![Free Tier Address](https://github.com/user-attachments/assets/2c3b6765-0e3d-4cbd-b45c-ed57e2842788 " ")

8. **결제 확인 방법 추가** 버튼을 클릭합니다.
          ![Payment Verification](https://github.com/user-attachments/assets/9d755793-03d0-4af7-895f-1c2be1070adf " ")

9. 검증 방법을 선택하세요. 이 경우 **신용 카드** 버튼을 클릭하세요. 귀하의 정보와 결제 세부 정보를 입력하세요.

    >**참고:** 이것은 무료 신용 프로모션 계정입니다. 계정을 업그레이드하기로 선택하지 않는 한 요금이 청구되지 않습니다.

    ![Credit Card](https://github.com/user-attachments/assets/1166113b-79b8-48c4-abb9-213bc61528d6 " ")

10. 결제 확인이 완료되면 확인란을 클릭하여 계약을 검토하고 수락합니다. **무료 체험 시작** 버튼을 클릭합니다.

    ![Start Free Trial](https://github.com/user-attachments/assets/00143bdd-ca24-4248-800f-f2105ef2f847 " ")

11. 귀하의 계정이 프로비저닝 중이며 곧 사용할 수 있을 것입니다! 계정이 프로비저닝될 때까지 로그아웃하는 것이 좋습니다. Oracle에서 프로비저닝이 완료되었다는 내용의 이메일을 받게 되며, 귀하의 클라우드 계정과 사용자 이름이 포함됩니다.

## 작업 2: OCI Account 로그인

*tenancy가 처음 생성될 때는 직접 로그인만 볼 수 있습니다. tenancy가 완전히 프로비저닝되면 아래에 설명된 대로 화면이 표시됩니다.*

1. [cloud.oracle.com](https://cloud.oracle.com)으로 이동합니다. 클라우드 계정 이름을 입력하고 **다음**을 클릭합니다. 이는 이전 섹션에서 계정을 만들 때 선택한 이름입니다. 이메일 주소가 아닙니다. 이름을 잊은 경우 확인 이메일을 참조하세요.

    ![Oracle Cloud](https://github.com/user-attachments/assets/ec26be7d-5c9b-4e05-96cf-efae871b3adb " ")

2. **계속**을 클릭하여 *"oraclecloud identityservice"*를 사용하여 로그인하세요.

   ![Sign In](https://github.com/user-attachments/assets/c2a087d0-cebe-488a-a6ff-624f31b01489 " ")

   Oracle Cloud 계정에 가입하면 선택한 사용자 이름과 비밀번호로 Oracle Identity Cloud Service에서 사용자가 생성됩니다. 이 단일 로그인 옵션을 사용하여 Oracle Cloud Infrastructure에 로그인한 다음 재인증 없이 다른 Oracle Cloud 서비스로 이동할 수 있습니다. 이 사용자는 계정에 포함된 모든 Oracle Cloud 서비스에 대한 관리자 권한을 가지고 있습니다.

3. 클라우드 계정 자격 증명을 입력하고 **로그인**을 클릭합니다. 사용자 이름은 이메일 주소입니다. 비밀번호는 계정에 가입할 때 선택한 것입니다.

     ![Username and Password](https://github.com/user-attachments/assets/489448bc-6f93-47f7-9217-b22fc23b6eed " ")

4. 보안 검증을 활성화하라는 메시지가 표시됩니다. **보안 검증 활성화**를 클릭합니다. 자세한 내용은, [다중 인증 관리 문서](https://docs.oracle.com/en-us/iaas/Content/Identity/Tasks/usingmfa.htm)를 참조 하세요.

    ![Enable secure verification](https://github.com/user-attachments/assets/38902c1a-a98a-42b1-88c7-5c31167b4933 " ")

5. 안전한 확인을 위해 **Mobile App** 또는 **FIDO Authenticator** 중 하나를 선택하세요.

    ![Choose method](https://github.com/user-attachments/assets/75441764-a083-41ae-9b77-afb0a30cc861 " ")

6. 선택한 경우:
    - **Mobile App** - 스크린샷에 표시된 단계에 따라 인증을 설정하세요.

        ![Mobile App](https://github.com/user-attachments/assets/1c291688-9254-4990-830d-70f7c8cd0638 " ")

    -  **FIDO Authenticator** - **설정**을 클릭하고 단계에 따라 인증을 설정합니다.

        ![FIDO Authenticator](https://github.com/user-attachments/assets/3489c0a0-1c24-40ee-b2fa-ef587ec2e0d9 " ")

7. 인증을 확인하면 이제 Oracle Cloud에 로그인할 수 있습니다!

    ![OCI Console Home Page](https://oracle-livelabs.github.io/common/images/console/home-page.png " ")

이제 **Next Lab로 진행**할 수 있습니다.

## **Acknowledgements**

- **Created By/Date** - Kay Malcolm, Database Product Management, Database Product Management, March 2020
- **Last Updated By** - Kihyuk, July 2024
