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

## Support 이메일 요청 서식 지정 방법
아래처럼 기본 메일 애플리케이션에서 LiveLabs 지원 받은 편지함에 자동으로 채워지는 이메일이 생성되고 제목 줄에 현재 워크숍도 포함됩니다. 아래 단계에 따라 문의하여 문제에 대한 빠른 해결책을 얻으세요.

1. 제목란에 **Workshop 이름**을 입력해 주세요(예 참조).
    ![Email](https://github.com/user-attachments/assets/5058b650-2aec-4af0-af78-60d27313de98)

2. 문제가 발생한 **Lab 번호**, **Task 번호**, **Step 번호**를 포함합니다. 또한 이 워크숍을 운영하는 **환경**(귀하의 테넌시 또는 LiveLabs 샌드박스 테넌시)도 포함합니다.

3. 이메일 내용에 **문제**에 대한 설명과 관련 정보를 포함하세요.

4. **스크린샷**과 시도한 **문제 해결 단계**를 첨부하면 문제를 재현하여 시기적절하고 정확한 해결책을 제공할 수 있습니다.

## Connectivity Issues?

**VPN**, **Corporate Network**에 연결되어 있나요?, 아니면 엄격한 **방화벽** 뒤에 있나요?

If any of these three conditions are true, some ports in your network may be closed to traffic.

For uploading data through Database Actions in your web browser and applications like the Oracle Analytics Tool could be restricted and may appear to "Hang" or freeze.

While connecting to a noVNC workshop, you might get "Hmmm... can't reach this page" error and could not access the workshop.

Try these options to access the environment again:

1. Please disconnect from your VPN and try again if applicable.

2. If you are connected to a corporate network, try switching to a public or a "clear" network if allowed.

3. Check and disable the ad blocker if there is one setup for your browser.

4. Try running the workshop in a different browser other than your current browser.

5. For the noVNC workshop, check if you can open port 6080.

6. For other standard scenarios, check if you can open ports such as 80, 443, and 22 (for ssh).

7. Alternatively, contact your IT Administrator to see if adding exceptions to your network or firewall would be viable.

## Cannot Create Passwords for Database Users?

1. Make sure the password you enter satisfies the following [restrictions](https://docs.oracle.com/en/cloud/saas/marketing/responsys-user/Account_PasswordRestrictions.htm).

## Cannot find Groups under Identity and Security in my tenancy?

1. From the navigation menu, click **Identity & Security** and select **Domains** under **Identity**.

  ![Select Domains](./images/select-domain.png " ")

2. Make sure you are in the correct compartment and click **Default(Current domain)**

  ![Click Default](./images/domain-groups.png " ")

3. From the Identity domain section on the left, click **Groups** to access the groups.

  ![Click Groups](./images/click-groups.png " ")

## Acknowledgements
* **Author** - LiveLabs Team
* **Contributors** - LiveLabs Team, Arabella Yao
* **Last Updated By/Date** - Kihyuk, July 2024
