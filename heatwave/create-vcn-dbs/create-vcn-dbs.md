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

## 작업 3: MySQL HeatWave (DB System) instance 생성

1. Navigation Menu > Databases > MySQL 클릭
    ![home menu mysq](https://github.com/user-attachments/assets/545d13c3-8ba9-4be2-965f-b808ff8adf1d "home menu mysql")

2. 'Create DB System' 클릭
    ![mysql create button](https://github.com/user-attachments/assets/b51d2259-047a-4063-a6aa-6526d0d274a6 " mysql create button")

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

    ![heatwave db option](https://github.com/user-attachments/assets/557838a4-0f82-4474-befd-6af387cd6752 "heatwave db option")

5. DB System 기본 정보 입력:

    a. Compartment **(root)** 선택

    b. Name 입력

    ```bash
    <copy>HEATWAVE-DB</copy>
    ```

    c. Description 입력

    ```bash
    <copy>MySQL HeatWave Database Instance</copy>
    ```

    d. **Standalone** 선택 및 **Configure MySQL HeatWave** Disable
    ![heatwave db stand alone](https://github.com/user-attachments/assets/ad2584eb-38c6-43f1-8590-15e24d896d46 "heatwave db stand alone ")

6. DB admin(Administrator Credentials) 생성 - **중요** 이 워크숍을 성공적으로 완료하려면 사용자 이름을 **admin**으로 설정해야 합니다.

    Username : **admin**

    Password*  (나중에 사용하기 위해 메모장에 비밀번호를 쓰세요)

    **Confirm Password** (위에 패스워드와 동일해야 합니다)

    ![heatwave db admin](https://github.com/user-attachments/assets/dfb4272a-079f-496a-8230-dc76a75b0a52 "heatwave db admin ")

7. networking 설정에서, 기본값을 유지 하시면 됩니다.

    a. Virtual Cloud Network: **HEATWAVE-VCN**

    b. Subnet: **Private Subnet-HEATWAVE-VCN (Regional)**

    c. On Configure placement under 'Availability Domain'

    AD-1 선택 ...  DB System에서 'Choose a Fault Domain'를 선택하지 마십시요.

    ![heatwave db network ad](https://github.com/user-attachments/assets/5a9e307d-8c2b-4e0a-a991-4c79fb3ee83d "heatwave db network ad ")

8. Backups 설정에서, 'Enable Automatic Backup' 선택해제(disable, workshop에서는 불필요) 

    ![heatwave db  backup](https://github.com/user-attachments/assets/f06a2b4c-747c-4180-88c0-290ef34a00af " heatwave db  backup")

9. hardware 설정에서
    - 1. **중요** **Heatwave Enable** 상자를 체크하세요
    - 2. **Change shape** 버튼을 클릭하여 **ECPU**를 선택한 다음 **MySQL.8** 모양을 선택하고 **Select a Shape** 버튼을 클릭합니다.
    - 3. **Configure HeatWave Cluster** 버튼을 클릭하세요.
        - **Change shape** 선택
        - **HeatWave.512GB** shape 선택
        - **Node**를 1로 선택
        - **MySQL HeatWave Lakehouse** box 체크
        - **Save Changes** 버튼 클릭
    - 4. Data Storage Size (GB)에 대해 값 설정 :  **512**

    ![heatwave db  hardware heatwave](https://github.com/user-attachments/assets/33610613-26bf-435c-8d1f-c633f380b688 "heatwave db hardware heatwave")

10. **중요**
    > **NOTE** 이 워크숍을 성공적으로 완료하려면 다음을 실행해야 합니다. **steps 11, 12, and 13**

11. Show Advanced Options를 클릭

12. **중요** Configuration tab으로 이동. **Select a MySQL version** 클릭 및 최신 MySQL version of the DB system 선택.

    ![HeatWave add host](https://github.com/user-attachments/assets/e79fd01f-e7a7-4ce4-9cbc-c556baf98632 "mysql host ")

13. **중요** Connections tab으로 이동, Hostname field에서 아래 이름 입력 (DB System Name):

    ```bash
        <copy>HEATWAVE-DB</copy> 
    ```  

    ![heatwave db advanced](https://github.com/user-attachments/assets/dc849855-9077-422b-973a-55bbf2480337 "heatwave db advanced ")

14. **Create MySQL DB System**  화면에서 상세 검토

    ![heatwave db create](https://github.com/user-attachments/assets/8603452e-2076-4985-9c77-b8e87b6eba6a "heatwave db create ")
  
    '**Create**' 버튼 클릭

15. 새로운 MySQL DB 시스템은 몇 분 후에 사용할 수 있습니다.
    
    생성 중에는 상태가 '생성 중'으로 표시됩니다.
    ![show creeation state](https://github.com/user-attachments/assets/41e0d527-126d-43da-bea2-92d30b5acc80 "show creeation state")

17. 'Active' 상태는 DB 시스템이 사용할 준비가 되었음을 나타냅니다.

    HEATWAVE-HW 페이지에서, **Connections** tab 선택하고 **Private IP** 를 따로 저장

    ![heatwave endpoint](https://github.com/user-attachments/assets/f167c081-b1f0-45bc-a0bf-da94fd3bb122 "heatwave endpoint")

이제 **next lab으로 진행**할 수 있습니다.

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, July 2024
