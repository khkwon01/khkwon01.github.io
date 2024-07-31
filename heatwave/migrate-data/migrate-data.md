# MySQL HeatWave 데이터 마이그레이션

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## 세션 소개

export 및 import 방법을 사용하여 MySQL 인스턴스에서 MySQL HeatWave 서비스로 데이터를 전송합니다..

자세한 내용은 OCI 문서를 참조하세요:
- [MySQL HeatWave Exporting and Importing](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/exporting-and-importing.html).

- https://plforacle.github.io/mysql-mgrate-apex/workshops/freetier/index.html


_Estimated Time:_ 20 minutes 소요

### 목표

이 Lab에서는 다음 작업을 안내해 드립니다.:

- Data import 사용하여 DB system 생성
- DB system에 data를 import
- MySQL servers and DB systems에서 data export
- Replication를 사용하여 data migrate

### Prerequisites (필수사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험


## 작업 1: Data import 사용하여 DB system 생성

데이터 import 기능을 사용하면 Object Storage bucket에서 standalone DB 시스템으로 데이터를 가져올 수 있습니다.

Object Storage bucket에서과 동일한 지역의 standalone DB 시스템으로만 가져올 수 있습니다. 또한, Object Storage bucket으로 데이터를 내보내는 동안 dump를 가져올 수 있습니다.

고가용성 DB 시스템(high availability DB system)으로 데이터를 가져오려면 먼저 standalone DB 시스템으로 데이터를 가져온 다음 고가용성(high availability) 기능을 활성화합니다.

아래 링크로 이동하여 **Importing Using the Data Import Feature** 지침을 따르세요.

[Importing Using the Data Import Feature](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/importing-using-data-import-feature.html)

## 작업 2: DB system에 data를 import

Oracle Cloud Infrastructure 컴퓨팅 인스턴스에서 MySQL Shell을 사용하여 MySQL HeatWave Service DB 시스템으로 데이터를 가져옵니다.

아래 링크로 이동하여 **Importing Using MySQL Shell** 지침을 따르세요:

[Importing Using MySQL Shell](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/importing-using-mysql-shell.html)

## 작업 3: MySQL servers and DB systems에서 data export

MySQL Shell의 dump 유틸리티를 사용하여 MySQL 인스턴스 데이터를 Object Storage bucket으로 내보냅니다. 그런 다음 데이터 import 기능을 사용하여 Object Storage bucket에서 동일한 지역에 있는 DB 시스템으로 데이터를 가져올 수 있습니다.

아래 링크로 이동하여 **Importing Using the Data Import Feature** 지침을 따르세요.:

[Exporting a MySQL Instance](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/exporting-mysql-instance.html)

## 작업 4: Replication를 사용하여 data migrate

Console과 MySQL Shell을 사용하여 MySQL 인스턴스를 MySQL HeatWave Service로 마이그레이션합니다. MySQL 인스턴스는 온프레미스, 다른 클라우드 공급업체에서 관리형 또는 비관리형 서비스로 실행되거나 MySQL HeatWave Service 인스턴스로 실행될 수 있습니다.

아래 링크로 이동하여 **Migrating a MySQL Instance to MySQL HeatWave Service** 지침을 따르세요:

[Migrating a MySQL Instance to MySQL HeatWave Service](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/migrating-mysql-instance-mysql-heatwave-service.html)


이제 **다음 Lab으로 진행**할 수 있습니다.

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, July 2024
