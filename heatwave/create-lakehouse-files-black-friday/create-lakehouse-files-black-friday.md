# HeatWave Lakehouse의 Object Storage에 데이터 업로드 - 블랙 프라이데이

## 세션 소개

이 워크숍에서 사용할 데이터(파일 세트)가 생성합니다. 개체 저장소 버킷을 생성하고 여기에 파일을 업로드합니다.

### 목표

- 샘플 파일을 다운로드하고 압축 해제하세요
- 개체 저장소 버킷 생성(Object Storage bucket)
- 저장된 PAR URL을 사용하여 버킷에 파일 추가

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험
- Lab 4까지 생성 및 테스트 완료

## 작업 1: 샘플 파일을 다운로드하고 압축 해제하세요

1. SSH로 아직 연결되지 않은 경우 명령줄에서 SSH를 사용하여 Compute 인스턴스에 연결합니다. "private key file"과 "생성된 Compute 인스턴스 IP"를 반드시 바꿔야 합니다.

     ```bash
    <copy>ssh -i private_key_file opc@new_compute_instance_ip</copy>
     ```

2. 가져온 샘플 데이터를 보관할 폴더 설정

    a. 홈 디렉토리로 이동

    ```bash
    <copy>cd ~ </copy>
     ```

    b. 홈 디렉토리에 폴더 생성

    ```bash
    <copy>mkdir lakehouse</copy>
     ```

    c. 해당 폴더로 이동

    ```bash
    <copy>cd lakehouse</copy>
     ```

3. 샘플 파일 다운로드

    ```bash
    <copy>wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/Ukv1g5qyvJK6asGvVoksGkUDIu8KaoVfmbhBzpmbRahXu7a2EmaVTJev2a-lHvUa/n/mysqlpm/b/mysql_customer_orders/o/black_friday.zip</copy>
     ```

4. black_friday.zip 파일을 압축 해제하면 서로 다른 파일 2개가 생성됩니다.

    ```bash
    <copy>unzip black_friday.zip</copy>
     ```

5. 파일을 리스트 하세요

    ```bash
    <copy>ls -l</copy>
    ```

    ![bucket file list](./images/datafiles-list.png "datafiles list")

## 작업 2: 개체 저장소 버킷 생성 (Object Storage bucket)

1. From the Console navigation menu, click **Storage**.
2. Under Object Storage, click Buckets
    ![bucket menu](./images/cloud-storage-menu.png "cloud storage menu")

    **NOTE:** Ensure the correct Compartment is selected : Select **lakehouse**

3. Click Create Bucket. The Create Bucket pane is displayed.

    ![bucket create pane](./images/cloud-storage-bucket.png "cloud storage bucket")

4. Enter the Bucket Name **lakehouse-files**
5. Under Default Storage Tier, click Standard. Leave all the other fields at their default values.

    ![Add bucket name](./images/create-lakehous-bucket.png "create bucket")

6. Create the  Pre-Authenticated Request URL for the bucket
     - a. Click on the 3 dots to the right of the **lakehouse-files** bucket  Click on ‘Create Pre-Authenticated Request’
        ![lakehouse-files 3 dots](./images/create-lakehous-bucket-par-dots.png "bucket par dots")
        ![Create PAR](./images/create-lakehous-bucket-par-load.png "bucket par load")
     - b. The ‘Bucket’ option will be pre-selected
     - c. For 'Access Type' select 'Permit object write
     - d. Click the Create "Pre-Authenticated Request' button
        ![PAR Button](./images/create-lakehous-bucket-par-load-button.png " bucket par load button")
     - e. Click the ‘Copy’ icon to copy the PAR URL
        ![Copy PAR](./images/create-lakehous-bucket-par-copy-load.png "bucket par load copy")
     - f. Save the generated PAR URL; you will need it in the next task

## Task 3: Add files into  the Bucket using the saved PAR URL

1. Go into the lakehouse folder and list all of the files

    ```bash
    <copy>cd ~/lakehouse</copy>
    ```

    ```bash
    <copy>ls -l</copy>
    ```

    ![bucket file list](./images/datafiles-list.png "datafiles list")

2. Add the black\_friday\_train.csv file to the storage bucket by modifying the following statement with the example below. You must replace the **(PAR URL)** value with the saved generated **PAR URL** from the previous Task.

    ```bash
    <copy>curl -X PUT --data-binary '@black_friday_train.csv' (PAR URL)black_friday_train.csv</copy>
     ```

     **Example**  
     curl -X PUT --data-binary '@black\_friday\_train.csv' https://objectstorage.us-ashburn-1.oraclecloud.com/p/RfXc55AGpLSu26UgqbmGxbWZwh4hPhLkVWYMg4f5pNerQx_1NghgSKJHLzE4IWxH/n/******/b/lakehouse-files/o/black_friday_train.csv

3. Add the @black\_friday\_test.csv file to the storage bucket by modifying the following statement with the example below. You must replace the **(PAR URL)** value with the saved generated **PAR URL** from the previous Task.

    ```bash
    <copy>curl -X PUT --data-binary '@black_friday_test.csv' (PAR URL)black_friday_test.csv</copy>
     ```

     **Example**  
     curl -X PUT --data-binary '@black\_friday\_test.csv' https://objectstorage.us-ashburn-1.oraclecloud.com/p/RfXc55AGpLSu26UgqbmGxbWZwh4hPhLkVWYMg4f5pNerQx_1NghgSKJHLzE4IWxH/n/******/b/lakehouse-files/o/black_friday_test.csv

4. Your **lakehouse-files** bucket should look like this:
    ![cloud storage bucket](./images/lakehouse-bucket.png "lakehouse bucket")

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering

- **Contributors** - Abhinav Agarwal, Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Kihyuk, MySQL Solution Engineering, Feburary 2025
