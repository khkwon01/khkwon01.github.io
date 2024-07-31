# OCI Bastion를 사용하여 Heatwave 접속

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## 세션 소개
클라우드에서 작업할 때 서버와 서비스가 퍼블릭 인터넷에 노출되지 않는 경우가 종종 있습니다. Oracle Cloud Infrastructure(OCI) MySQL 클라우드 서비스는 프라이빗 네트워크를 통해서만 액세스할 수 있는 서비스의 예입니다. 이 서비스는 완벽하게 관리되므로 잠재적인 공격과 취약성으로부터 데이터를 보호하기 위해 인터넷에서 분리하여 보관합니다. 리소스 노출을 최대한 제한하는 것이 좋지만 언젠가는 해당 리소스에 연결하고 싶을 것입니다. 바로 여기서 배스천 호스트가 등장합니다. 배스천 호스트는 프라이빗 리소스와 프라이빗 네트워크에 액세스해야 하는 엔드포인트 사이에 있는 리소스로, SSH 또는 RDP와 같은 프로토콜을 통해 프라이빗 리소스에 로그인할 수 있도록 하는 "jump box" 역할을 할 수 있습니다. 배스천 호스트에는 MySQL DB 시스템에 연결하기 위한 가상 클라우드 네트워크가 필요합니다.


Oracle은 OCI에 Bastion Service를 추가했습니다. 그리고 OCI 대시보드에서 브라우저 기반 터미널인 Cloud Shell을 사용할 수 있는 환경도 제공하고 있습니다.

오늘은 이 두 가지 구성 요소를 사용하여 브라우저에서 MDS DB 시스템에 연결합니다.

_Estimated Lab Time:_ 15 minutes 소요

### 목표

이 Lab에서는 다음 작업을 안내해 드립니다.

- Bastion Service 구성
- Bastion session 생성
- MySQL Heatwave 접속

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험

## 작업 1: Bastion Service 구성

새로운 Bastion 서비스를 사용하면 MySQL DB 시스템에 대한 SSH 터널을 생성할 수 있습니다.

1. Navigation Menu > Identity Security > Bastion 로 이동

    ![bastion menu](./images/bastion-menu.png " bastion menu")

2. Create Bastion 클릭

    ![bastion menu create](./images/bastion-menu-create.png "bastion menu create ")

3. Create bastion 화면에서, 다음 필드를 완성하세요:

    Bastion Name

     ```bash
     <copy>MDSBastion</copy>
     ```

    Target virtual Cloud network in .. (root)

    `HEATWAVE-VCN` 선택

    Target subnet in .. (root)

    `Private Subnet-HEATWAVE-VCN` 선택

    CIDR block allowlist (As you don’t know the IP of the Cloud Shell, use 0.0.0.0/0)

     ```bash
     <copy>0.0.0.0/0</copy>
     ```

    `0.0.0.0/0(New)` 클릭

     ![bastion create page](./images/bastion-create.png "bastion create page ")

4. `Create Bastion` 버튼 클릭

    완료되면 화면이 다음과 같아야 합니다:

    ![bastion list](./images/bastion-menu-list.png "bastion list ")

## 작업 2: Bastion session 생성

1. Bastion 세션을 만들기 전에 메모장을 엽니다. 다음 단계를 수행하여 MySQL 데이터베이스 시스템 private IP 주소를 기록합니다.:

    - Navigation Menu > Databases > MySQL 로 이동
     ![db list](./images/db-list.png "db list")

    -  `HEATWAVE-DB` Database System link 클릭

     ![active ](./images/db-active.png "active ")

    - **Connections** tab 으로 이동 및 **Private IP address** 를 메모장에 복사

2. public SSH 키를 메모장에 복사하려면 다음 단계를 수행하세요.

    - Cloud shell 오픈
     ![cloud shell open](./images/cloudshell-open.png "cloud shell open")

    - 다음 명령을 입력하세요

    ```bash
     <copy>cat .ssh/id_rsa.pub</copy>
    ```

    ![new cloud shell get ssh](./images/cloudshell-get-ssh.png "new cloud shell det ssh")

3. 메모장에 id\_rsa.pub 내용을 복사합니다.
        Your notepad should look like this
    ![notepad](./images/notepad-display.png "notepad ")  

    >**Note** Make sure you have a copy of your id\_rsa and Id\_rsa.pub files in your local ~/.ssh folder. If not download it from the cloud shell where you originally created it. 

4. Go to Navigation Menu > Identity Security > Bastion

5. Click the `MDSBastion` link

     ![bastion display](./images/bastion-display.png "bastion display ")

6. Click `Create Session`

7. Set up the following information
    - Session type
      Select `SSH port forwarding session`
    - Session Name
        *Keep Default*
    - IP address
        *Enter HeatWave DB IP address ( from notepad)*

8. Enter the Port

    ```bash
        <copy>3306</copy>
    ```

9. Add SSH Key -  Copy SSH Key from notepad
    - The screen should look like this
    ![ssh key](./images/bastion-ssh-key.png "ssh key ")
    - Click the `Create Session` button
10. The completed Bastion Session should look like this
    ![bastion session display](./images/bastion-session-display.png "bastion session display")

    **Note: The Session will expire in 180 minutes**

## 작업 3: MySQL Heatwave 접속

1. Click on the 3 vertical dots on the Bastion Session

    ![connect with bastion](./images/bastion-connect.png "connect with bastion ")

2. Click `View SSH Command`  

    ![bastion view ssh](./images/bastion-view.png "bastion view ssh ")

3. Click copy and paste the information to your notepad and hit Close

4. update the session command on notepad
    - Set the beginning of the command `ssh -i <privateKey> -N -L 3306`
    - Add the verbose (-v) option to the SSH command for detailed information about the connection.

    The command from your notepad should look like this

    ![notepad display](./images/notepad-connect-command.png "notepad display")

5. Open a Windows PowerShell or Mac Terminal and enter the command from the notepad. Add  the ssh file name  and the Database Port  value (3306) It should like this..

    *Don't forget the -v  character*

    `ssh -i ~/.ssh/id_rsa -N -L 3306:10.0.1.17:3306 -p 22 ocid1.bastionsession.oc1.iad.amaaaaaa47ys2xaabm3koownovovwekvkitudcvdjk6dc5qtl6c6mtwxdkuq@host.bastion.us-ashburn-1.oci.oraclecloud.com -v`

6. Use MySQL Shell to connect to the MySQL Database Service. Enter:

     ```bash
     <copy>mysqlsh admin@127.0.0.1 --sql</copy>
     ```

7. View  the airportdb total records per table in

    ```bash
    <copy>SELECT table_name, table_rows FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'airportdb';</copy>
    ```

    ![view arportdb](./images/airport-db-view.png "view arportdb ")

**Note** You can also use  the bastion service to connect to your local computer and access  MySQL  with Workbench or Visual Studio Code

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, July 2024
