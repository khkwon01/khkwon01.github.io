# MySQL HeatWave Instance 생성

![mysql heatwave](https://github.com/user-attachments/assets/f97318c4-97b5-468e-8abf-6207850fac98 "mysql heatwave")

## 세션 소개

이 Lab에서는 MySQL DB 시스템을 만들고 구성합니다. 자세한 내용은 OCI 문서를 참조하세요.
[Creating a DB System Using the Console](https://docs.oracle.com/en-us/iaas/mysql-database/doc/creating-db-system1.html#GUID-AE89C67D-E1B1-4F11-B934-8B0564B4FC69).

_Estimated Time:_ 20 minutes 소요

### 목표

이 Lab에서는 다음 작업을 안내해 드립니다.

- Virtual Cloud Network (VCN) 생성
- MySQL HeatWave (DB System) Instance 생성

### Prerequisites (요구조건)

- An Oracle Trial, Paid or LiveLabs Cloud Account
- MySQL Shell에 사용경험

## 작업 1: Virtual Cloud Network 생성

1. Oracle Cloud에 로그인해야 합니다!

    **탐색 메뉴**를 클릭하세요.

    ![OCI Console Home Page](https://github.com/user-attachments/assets/51609651-9416-47c4-9315-deeaa76e0ddd " home page")

2. **Networking** 클릭, 다음 **Virtual Cloud Networks** 클릭
    ![menu vcn](https://github.com/user-attachments/assets/deffa714-6cd6-4245-8283-95ecb5dde36b "home menu networking vcn ")

    root compartment 선택
    ![vcn wizard Select Root compartment](https://github.com/user-attachments/assets/f46635d5-8288-4922-8b8f-46697ab168ac "vcn menu compartmen root ")

3. **Start VCN Wizard** 선택 및 클릭
    ![vcn start wizard](https://github.com/user-attachments/assets/216f4865-7252-4941-ad9a-784fa6a94357 "vcn wizard menu")

4. 'Create VCN with Internet Connectivity' 생성

    'Start VCN Wizard' 클릭
    ![vcn wizard start create](https://github.com/user-attachments/assets/e5c425d1-b78f-41f9-8c80-8bc8deca0afc "start vcn wizard start")

5. VCN with Internet Connectivity 생성

    기본 정보에서 다음 필드를 작성하세요.

    VCN Name:

    ```bash
    <copy>HEATWAVE-VCN</copy>
    ```

    Compartment: **(root)** 선택
   
    화면은 다음과 유사해야 합니다.
    ![select compartment](https://github.com/user-attachments/assets/f4d21356-9dc1-4b3e-964a-7cdf9cb5e277 "select compartment")

7. 화면 하단의 '다음'을 클릭하세요

8. Oracle Virtual Cloud Network(VCN), 서브넷 및 게이트웨이 검토

    '생성'을 클릭하여 VCN을 생성합니다.
    ![create vcn](https://github.com/user-attachments/assets/615f4e26-581d-420e-9aa7-2f13710e5aed "create vcn")

9. 가상 클라우드 네트워크 생성이 완료되면 '가상 클라우드 네트워크 보기'를 클릭하여 생성된 VCN을 표시합니다.
    ![vcn creation completing](https://github.com/user-attachments/assets/3e933bf1-bce3-41b0-98b4-1d2c342240c0 "vcn creation completing")

## 작업 2: MySQL 수신을 허용하도록 Security list을 구성

1. On HEATWAVE-VCN page under 'Subnets in (root) Compartment', '**Private Subnet-HEATWAVE-VCN**' 클릭
     ![vcn subnet](https://github.com/user-attachments/assets/0dc67da9-904b-456a-b389-db78d42a0a0c "vcn details subnet")

2. On Private Subnet-HEATWAVE-VCN page under 'Security Lists', '**Security List for Private Subnet-HEATWAVE-VCN**' 클릭
    ![vcn private security list](https://github.com/user-attachments/assets/d92bbfb1-1b27-4b05-8a43-06d9a6a08f42 "vcn private security list")

3. On Security List for Private Subnet-HEATWAVE-VCN page under 'Ingress Rules', '**Add Ingress Rules**' 클릭
    ![vcn private subnet](https://github.com/user-attachments/assets/788253be-3378-4c8c-8d83-56db90d1ed22 "vcn private security list ingress")

4. Ingress Rule 1 아래 Ingress Rules page에서

    a. Add an Ingress Rule with Source CIDR

    ```bash
    <copy>0.0.0.0/0</copy>
    ```

    b. Destination Port Range

    ```bash
    <copy>3306,33060</copy>
     ```

    c. Description

    ```bash
    <copy>MySQL Port Access</copy>
    ```

    d. 'Add Ingress Rule' 클릭
    ![add ingres rule](https://github.com/user-attachments/assets/e84d8f43-61ba-440a-bc49-a79a3b699972 "vcn private security list ingress rukes mysql")

5. On Security List for Private Subnet-HEATWAVE-VCN page, 새로운 Ingress 규칙은 Ingress 규칙 목록 아래에 표시됩니다.
    ![show ingres rule](https://github.com/user-attachments/assets/222d6dbc-2711-4f87-863f-faa3b71915ad "vcn private security list ingress display")

## 작업 3: MySQL Database for HeatWave (DB System) instance 생성

1. Navigation Menu > Databases > MySQL 클릭
         Databases
         MySQL
    ![home menu mysq](https://github.com/user-attachments/assets/545d13c3-8ba9-4be2-965f-b808ff8adf1d "home menu mysql")

2. 'Create DB System' 클릭
    ![mysql create button](https://github.com/user-attachments/assets/b51d2259-047a-4063-a6aa-6526d0d274a6" mysql create button")

3. 데이터베이스 구성을 위해 아래 필드 각각에 대해 값을 입력

    - Provide DB System information
    - Setup the DB system
    - Create Administrator credentials
    - Configure Networking
    - Configure placement
    - Configure hardware
    - Exclude Backups
    - Set up Advanced Options

4. DB System Option에서 **Development or Testing** 선택

    ![heatwave db option](./images/mysql-create-option-develpment.png "heatwave db option")

5. Provide basic information for the DB System:

    a. Select Compartment **(root)**

    b. Enter Name

    ```bash
    <copy>HEATWAVE-DB</copy>
    ```

    c. Enter Description

    ```bash
    <copy>MySQL HeatWave Database Instance</copy>
    ```

    d. Select **Standalone** and DISABLE **Configure MySQL HeatWave**
    ![heatwave db stand alone](./images/mysql-create-stand-alone.png "heatwave db stand alone ")

6. Create Administrator Credentials - **IMPORTANT** username must be set to **admin**  in order to successfully complete this workshop

    Username : **admin**

    Password*  (write password to notepad for later use)

    **Confirm Password** (value should match password for later use)

    ![heatwave db admin](./images/mysql-create-admin.png "heatwave db admin ")

7. On Configure networking, keep the default values

    a. Virtual Cloud Network: **HEATWAVE-VCN**

    b. Subnet: **Private Subnet-HEATWAVE-VCN (Regional)**

    c. On Configure placement under 'Availability Domain'

    Select AD-1  ...  Do not check 'Choose a Fault Domain' for this DB System.

    ![heatwave db network ad](./images/mysql-create-network-ad.png "heatwave db network ad ")

8. On Configure Backups, disable 'Enable Automatic Backup'

    ![heatwave db  backup](./images/mysql-create-backup.png " heatwave db  backup")

9. On Configure hardware
    - 1. **IMPORTANT** Check the  **Enable Heatwave** box
    - 2. Click the **Change shape** button to select **ECPU** then **MySQL.8** shape and and click the **Select a Shape** button
    - 3. Click the **Configure HeatWave Cluster** button 
        - Select **Change shape**
        - Select **HeatWave.512GB** shape
        - Set **Node** to 1
        - Check the **MySQL HeatWave Lakehouse** box
        - Click the **Save Changes** button
    - 4. For Data Storage Size (GB) Set value to:  **512**

    ![heatwave db  hardware heatwave](./images/mysql-create-db-hardware-heatwave-ecpu.png "heatwave db hardware heatwave")

10. **IMPORTANT**
    > **NOTE** In order to successfully complete this workshop you must execute **steps 11, 12, and 13**

11. Click on Show Advanced Options

12. **IMPORTANT** Go to the Configuration tab. Click on **Select a MySQL version** and select the latest MySQL version of the DB system.

    ![HeatWave add host](./images/mysql-configuration-version.png "mysql host ")

13. **IMPORTANT** Go to the Connections tab, in the Hostname field enter (your DB System Name):

    ```bash
        <copy>HEATWAVE-DB</copy> 
    ```  

    ![heatwave db advanced](./images/mysql-create-advanced-connections.png "heatwave db advanced ")

14. Review **Create MySQL DB System**  Screen

    ![heatwave db create](./images/mysql-create.png "heatwave db create ")
  
    Click the '**Create**' button

15. The New MySQL DB System will be ready to use after a few minutes

    The state will be shown as 'Creating' during the creation
    ![show creeation state](./images/mysql-create-in-progress.png "show creeation state")

16. The state 'Active' indicates that the DB System is ready for use

    On HEATWAVE-HW Page, select the **Connections** tab and save the **Private IP**

    ![heatwave endpoint](./images/mysql-detail-active.png "heatwave endpoint")

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, March 2024
