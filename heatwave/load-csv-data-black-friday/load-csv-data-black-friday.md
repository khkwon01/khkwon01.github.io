# OCI Object Store에서 Lakehouse로 CSV 데이터 로드 - black-friday

## 세션 소개

Object Storage에서 HeatWave로 데이터를 로드하려면 Object Storage에 있는 파일이나 폴더 객체의 위치를 ​​지정해야 합니다.

1. [Resource Principal 사용](https://docs.oracle.com/en-us/iaas/autonomous-database-serverless/doc/resource-principal-enable.html) - 민감한 데이터일 경우 Object Storage에 있는 데이터에 액세스하려면 리소스 주체 기반 접근 방식을 사용하는 것이 좋습니다. 이 접근 방식이 더 안전하기 때문입니다.

2. [Pre-Authenticated Request URLs (PARs) 사용](https://docs.oracle.com/en-us/iaas/Content/Object/Tasks/usingpreauthenticatedrequests.htm) - PAR을 사용하기로 선택한 경우 Lakehouse에서 읽기 전용 PAR을 사용하고 PAR에 대한 짧은 만료 날짜를 지정하는 것이 좋습니다. 만료 날짜는 로딩 일정과 일치해야 합니다.

샘플 데이터 세트를 사용하므로 이 LiveLab에서 PAR을 활용하겠습니다. HeatWave에서 이미 MySQL에서 로드된 여러 테이블을 사용할 수 있습니다.

이제 Object Store에서 Black Friday 테이블을 로드하겠습니다.

### 목표

- "black_friday" 파일에 대한 PAR 링크 생성
- 스키마(schema)를 유추하고 용량을 추정하기 위해 Autoload를 실행합니다.
- Object Store에서 MySQL HeatWave로 전체 black_friday 테이블 로드

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험
- Lab 4에 작업1까지 완료가 필요

## 작업 1: "black\_friday" 파일에 대한 PAR 링크 생성

1. **black\_friday\_train.csv** 개체에 대한 PAR URL을 만듭니다.

    - a. OCI 콘솔에서 OCI의 lakehouse-files 버킷으로 이동합니다.
    - b. black\_friday\_train.csv 파일을 선택하고 세 개의 세로 점을 클릭합니다.

        ![black_friday_train.csv 선택](./images/storage-delivery-orders-folder.png "storage black_friday_train.csv")

    - c. '사전 인증된 요청 생성 (Pre-Authenticated Request)'을 클릭하세요.
    - d. '사전 인증된 요청 대상 (PreAuthentcated Request Target)'에서 '개체 (Object)' 옵션을 선택하려면 클릭하세요.
    - e. '액세스 유형 (Access Type)' 옵션 : '개체 읽기 허용'(Permit object reads)
    - h. '사전 인증된 요청 만들기 (Pre-Authenticated Request)' 버튼을 클릭하세요.

       ![PAR 생성](./images/storage-delivery-orders-folder-page.png "storage  folder page")

    - i. '복사' 아이콘을 클릭하여 PAR URL을 복사합니다.
    - j. 생성된 PAR URL을 저장하세요. 나중에 필요합니다.

2. **black\_friday\_test.csv** 개체에 대한 PAR URL을 생성하려면 동일한 작업을 수행하세요.

    - a. OCI 콘솔에서 OCI의 lakehouse-files 버킷으로 이동합니다.
    - b. black\_friday\_test.csv 파일을 선택하고 세 개의 세로 점을 클릭합니다.
    - c. '사전 인증된 요청 생성 (Pre-Authenticated Request)'을 클릭하세요.
    - d. '사전 인증된 요청 대상(PreAuthentcated Request)'에서 '개체 (Object)' 옵션을 선택하려면 클릭하세요.
    - e. '액세스 유형 (Access Type)' 옵션 : '개체 읽기 허용'(Permit object reads)
    - h. '사전 인증된 요청 만들기 (Pre-Authenticated Request)' 버튼을 클릭하세요.
    - i. '복사' 아이콘을 클릭하여 PAR URL을 복사합니다.
    - j. 생성된 PAR URL을 저장하세요. 나중에 필요합니다.

## 작업 2: Cloud Shell을 사용하여 MySQL HeatWave 시스템에 연결

1. SSH로 아직 연결되지 않은 경우 명령줄에서 SSH를 사용하여 Compute 인스턴스에 연결합니다. "개인 키 파일"과 "새 Compute 인스턴스 IP"를 반드시 바꿔야 합니다.

     ```bash
    <copy>ssh -i private_key_file opc@new_compute_instance_ip</copy>
     ```

2. 아직 MySQL에 연결되지 않았다면 다음 명령을 사용하여 MySQL Shell 클라이언트 도구를 사용하여 MySQL에 연결합니다.

    ```bash
    <copy>mysqlsh -uadmin -p -h 10.0.1... --sql </copy>
    ```

    ![MySQL Shell Connect](./images/mysql-shell-login.png " mysql shell login")

3. heatwave instance에 schemas를 리스트 하세요.

    ```bash
        <copy>show databases;</copy>
    ```

    ![Databse Schemas](./images/list-schemas-after.png "list schemas after")

4. 머신 러닝 스키마 (schema) 생성

    ```bash
    <copy>CREATE DATABASE heatwaveml_bench;</copy>
    ```

5. 새 데이터베이스를 기본값(default)으로 설정

    ```bash
    <copy>use heatwaveml_bench;</copy>
    ```

    이제 Autoload를 사용하여 객체 저장소에서 MySQL HeatWave로 테이블을 로드할 준비가 되었습니다.

## 작업 3: Autoload를 실행하여 Object Store의 black\_friday 테이블에 대한 스키마를 유추하고 용량을 추정합니다.

1. 데이터는 이전 작업에서 PAR URL을 만든 객체 저장소의 black\_friday\_train.csv 파일에 포함되어 있습니다. 다음 명령을 하나씩 입력하고 Enter를 누릅니다.

2. 이렇게 하면 테이블 데이터를 로드할 스키마가 설정됩니다. 이 스키마가 생성되지 않았더라도 걱정하지 마세요. 스키마가 없으면 Autopilot에서 이 스키마를 생성할 수 있는 명령을 생성합니다.

    ```bash
    <copy>SET @db_list = '["heatwaveml_bench"]';</copy>
    ```

3. 데이터를 로드하고자 하는 테이블 이름과 객체 저장소의 소스 파일에 대해 다음 정보에 대해 매개변수를 설정합니다. 아래의 **(PAR URL)**을 이전 작업에서 생성한 것으로 대체합니다.

    ```bash
    <copy>SET @dl_tables = '[{
    "db_name": "heatwaveml_bench",
    "tables": [{
        "table_name": "black_friday_train",
        "dialect": {
            "format": "csv",
            "field_delimiter": ",",
            "record_delimiter": "\\r\\n",
            "has_header": true,
            "is_strict_mode": false},
            "file": [{"par": "(PAR URL)"}]
        }
    ]}
    ]';</copy>
    ```

    - 다음 예와 같아야 합니다. (따옴표("") 안에 PAR 링크를 포함해야 합니다.)

    ![autopilot set table example](./images/set-table-example.png "autopilot set table example")

4. 이 명령은 Autoload에 필요한 모든 옵션을 채웁니다.

    ```bash
    <copy>SET @options = JSON_OBJECT('mode', 'dryrun', 'policy', 'disable_unsupported_columns', 'external_tables', CAST(@dl_tables AS JSON));</copy>
    ```

5. 이 Autoload 명령을 실행하세요:

    ```bash
    <copy>CALL sys.heatwave_load(@db_list, @options);</copy>
    ```

6. Autoload가 실행을 완료하면 출력에 여러 정보가 포함됩니다.
    - a. 식별한 스키마(schema)에 테이블이 존재하는지 여부입니다.
    - b. 자동 스키마 유추(Auto schema inference)는 테이블의 열 수를 결정합니다.
    - c. 자동 스키마 샘플링은 테이블에서 적은 수의 행을 샘플링하고 테이블의 행 수와 테이블 크기를 결정합니다.
    - d. 자동 프로비저닝은 이 테이블을 HeatWave에 로드하는 데 필요한 메모리 양과 이 데이터를 로드하는 데 걸리는 시간을 결정합니다.

    ![Dryrun script](./images/load-script-dryrun.png "load script dryrun")

7. Autoload는 아래와 같은 문장도 생성했습니다. 지금 이 문장을 실행하세요.

    ```bash
    <copy>SELECT log->>"$.sql" AS "Load Script" FROM sys.heatwave_autopilot_report WHERE type = "sql" ORDER BY id;</copy>
    ```


8. 실행 결과에는 테이블을 생성하고 이 테이블 데이터를 Object Store에서 HeatWave로 로드하는 데 필요한 SQL 문이 포함됩니다.

    ![create train table](./images/create-black-friday-train.png "create train table")

9. 결과에서 **CREATE TABLE** 명령을 복사합니다.

10. **CREATE TABLE** 명령을 실행하여 블랙 프라이데이 (black-friday) 테이블을 만듭니다.

11. 생성 명령과 결과는 다음과 같아야 합니다.

    ![ result train table](./images/create-table-black-friday.png "result train table")


## 작업 4: Object Store에서 MySQL HeatWave로 black\_friday\_train 테이블을 로드합니다.

1. 이 명령을 실행하면 생성된 테이블 구조를 확인할 수 있습니다.

    ```bash
    <copy>desc black_friday_train;</copy>
    ```

    ![black_friday_train Table structure](./images/describe-balck-friday-table.png "black_friday_train Table structure")

2. 이제 Object Store 파일에서 테이블에 데이터를 로드합니다.

    ```bash
    <copy> ALTER TABLE `heatwaveml_bench`.`black_friday_train` SECONDARY_LOAD; </copy>
    ```

3. 테이블에 로드된 행의 수를 확인하세요.

    ```bash
    <copy>select count(*) from black_friday_train;</copy>
    ```

    The black\_friday\_train table has 116698 rows.

4. 표의 데이터 샘플을 확인하세요.

    ```bash
    <copy>select * from black_friday_train limit 5;</copy>
    ```

## 작업 5: Object Store에서 MySQL HeatWave로 black\_friday\_test 테이블을 생성하고 로드합니다.

1. black\_friday\_train Create 명령을 복사하여 black\_friday\_test 테이블을 만들고 (PAR URL)을 이전에 저장한 black\_friday\_test.csv PAR URL로 바꿉니다. 이는 black\_friday\_test.csv 테이블의 소스가 됩니다:

    ```bash
    <copy>CREATE TABLE `heatwaveml_bench`.`black_friday_test`( `Gender` varchar(1) NOT NULL COMMENT 'RAPID_COLUMN=ENCODING=VARLEN', `Age` varchar(5) NOT NULL COMMENT 'RAPID_COLUMN=ENCODING=VARLEN', `Occupation` tinyint unsigned NOT NULL, `City_Category` varchar(1) NOT NULL COMMENT 'RAPID_COLUMN=ENCODING=VARLEN', `Stay_In_Current_City_Years` varchar(2) NOT NULL COMMENT 'RAPID_COLUMN=ENCODING=VARLEN', `Marital_Status` tinyint unsigned NOT NULL, `Product_Category_1` tinyint unsigned NOT NULL, `Product_Category_2` tinyint unsigned NOT NULL, `Product_Category_3` tinyint unsigned NOT NULL, `Purchase` mediumint unsigned NOT NULL) ENGINE=lakehouse SECONDARY_ENGINE=RAPID ENGINE_ATTRIBUTE='{"file": [{"par": "(PAR URL)"}], "dialect": {"format": "csv", "has_header": true, "is_strict_mode": false, "field_delimiter": ",", "record_delimiter": "\\r\\n"}}';</copy>
    ```


    - 다음 예와 같아야 합니다.
      (PAR 링크를 at of quotes("")에 포함해야 합니다.):

        ![autopilot create table with no field name](./images/create-table-no-fieldname.png "autopilot create table with no field name")

2. Run this command to see the table structure created:

    ```bash
    <copy>desc black_friday_test;</copy>
    ```

3. Load the data from the Object Store into the black\_friday\_test table.

    ```bash
    <copy>ALTER TABLE /*+ AUTOPILOT_DISABLE_CHECK */ `heatwaveml_bench`.`black_friday_test` SECONDARY_LOAD;</copy>
    ```

4. Once Autoload completes, check the number of rows loaded into the table.

    ```bash
    <copy>select count(*) from black_friday_test;</copy>
    ```

5. View a sample of the data in the table.

    ```bash
    <copy>select * from black_friday_test limit 5;</copy>
    ```

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering

- **Contributors** - Abhinav Agarwal, Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, Feburary 2025
