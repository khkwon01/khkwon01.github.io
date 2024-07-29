# 도움이 필요할 경우

## 세션 소개
이 페이지는 LiveLab에서 사용자가 직면하는 몇 가지 일반적인 문제를 해결하는 데 도움을 주기 위해 설계되었습니다.

문제 해결 팁을 읽은 후에도 여전히 문제가 있거나 워크숍에 대한 문제를 보고하고 싶다면 오른쪽 상단 모서리에 있는 물음표 아이콘을 클릭하여 이메일을 통해 LiveLabs 팀에 직접 문의하세요.

![Help button](https://github.com/user-attachments/assets/2d46fe0d-355b-477b-96f3-089f9a43eeae)


For more about getting support using our email, click [here](#HowtoFormatYourSupportEmailRequest).

### Common Issues Table of Contents
  - [Connectivity Issues?](#ConnectivityIssues?)
  - [Cannot Create Passwords for Database Users?](#CannotCreatePasswordsforDatabaseUsers?)
  - [Cannot find Groups under Identity and Security in my tenancy?](#CannotfindGroupsunderIdentityandSecurityinmytenancy?)

## How to Format Your Support Email Request
This will construct an email in your default mail application that is auto-populated to address our LiveLabs support inbox and will also include your current workshop in the subject line. Follow the steps below to contact us and get a quick resolution to your issue.

1. In the subject line please provide the **Workshop Name** (see example).
    ![Email](./images/e-mail.png)

2. Include the **Lab Number**, **Task Number**, and **Step Number** where you've encounter the issue. Also, include the **environment** where you are running this workshop (your tenancy or the LiveLabs sandbox tenancy).

3. Include the description of your **issue** and any pertinent information in the contents of your email.

4. Attach a **Screenshot** and **Any Troubleshooting Steps** you've tried, so that we can recreate the issue and provide a timely and accurate solution.

## Connectivity Issues?

Are you connected to a **VPN**, **Corporate Network**, or behind a strict **Firewall**?

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
