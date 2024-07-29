# Introduction

![image](https://github.com/user-attachments/assets/73823634-c6c1-491f-88ce-86fa1ac13060)


## Workshop에 대해서

MySQL HeatWave는 통합 쿼리 가속기를 갖춘 완벽하게 관리되는 데이터베이스 서비스로, 조직이 MySQL 데이터베이스 또는 객체 저장소에 저장된 데이터에 대해 트랜잭션 처리, 실시간 분석, 데이터웨어하우스 및 머신 러닝, Gen-AI을 효율적으로 실행할 수 있도록 합니다.

MySQL HeatWave는 분석 또는 머신 러닝을 실행하기 위해 MySQL에서 데이터를 옮기는 데 복잡한 ETL 작업이 필요 없습니다. 기존 MySQL 애플리케이션은 아무런 변경 없이 MySQL HeatWave에서 실행될 수 있으며 기본 제공 쿼리 가속기를 통해 훨씬 더 나은 쿼리 성능을 얻을 수 있습니다. MySQL HeatWave를 사용하면 조직은 CSV, Parquet, Aurora 또는 Redshift에서 내보낸 파일과 같은 다양한 파일 형식의 객체 저장소에서 수백 테라바이트의 데이터에 대한 분석을 실행할 수 있으며, 데이터를 MySQL 내부에 저장할 필요가 없습니다.

이 워크숍에서는 MySQL HeatWave 클러스터를 만들고, MySQL Shell을 사용하여 클러스터에 연결하고, HeatWave에서 쿼리를 실행하고, Oracle Cloud에서 분석 워크로드를 실행합니다.

전반적으로 이 워크숍에서는 MySQL HeatWave를 생성하고 관리하는 것이 얼마나 쉬운지, 그리고 MySQL HeatWave를 통해 실시간 통찰력을 바탕으로 비즈니스에 중요한 결정을 내리는 것이 어떻게 가능한지 보여줍니다.

_Estimated Lab Time:_ 4 hours 소요

## Heatwave 제품/기술 소개

MySQL HeatWave는 Oracle MySQL Database Service를 위한 대량 병렬, 고성능, 메모리 내 쿼리 가속기로, 분석 및 혼합 워크로드에 대해 MySQL 성능을 엄청나게 가속화합니다. ETL 프로세스 없이 고객이 MySQL 데이터베이스에서 직접 OLTP 및 OLAP 워크로드를 실행할 수 있는 유일한 서비스입니다. MySQL Autopilot은 고급 머신 러닝 기술을 사용하여 프로비저닝, 데이터 로딩, 쿼리 처리 및 오류 처리를 포함한 데이터베이스 수명 주기 작업을 자동화합니다. 이를 통해 수동 관리 작업이 최소화되고 HeatWave의 유용성, 성능 및 확장성이 더욱 향상됩니다. MySQL HeatWave는 또한 Data Integration Service 및 Oracle Analytics Cloud와 같은 다른 Oracle Cloud 서비스와 통합되어 원활한 엔드투엔드 통합을 제공합니다.

MySQL Database Service with HeatWave is a fully managed service, optimized for Oracle Cloud Infrastructure. It enables you to:

- Instantly provision MySQL instances and connect to a production ready, pre-configured MySQL database.
- Run OLTP and OLAP workload directly on a single MySQL platform without the need of ETL, and no change in your applications.
- Efficiently run mixed and analytics workloads with best price performance. HeatWave is 6.5X faster than Amazon Redshift at half the cost, 7X faster than Snowflake at one-fifth the cost, and 1400X faster than Amazon Aurora at half the cost.
- Make more informed business decision by getting real-time insights from your operational data.
- Free up time of developers, DBAs, and DevOps to focus on value added tasks that are core to your business.
- Access to dozens of additional Oracle Cloud Services enabling organizations to embrace the shift to the cloud.

_Lab Setup

![image](https://github.com/user-attachments/assets/3d3a2b35-f9ab-4f86-acbf-548b159c5a4a)

[//]:    [](youtube:6nsgwclsnaM)

## Objectives

This Workshop provides you with the knowledge required to Provision, Configure, and Manage MySQL HeatWave for OLTP / OLAP/ AutoML / Lakehouse. You will be guided through the following steps:

- Create MySQL HeatWave Instance
- Create Compute Instance
- Connect to HeatWave with MySQL Shell and Workbench
- Connect to HeatWave with OCI Bastion
- Connect to HeatWave with OCI SQL Worksheet
- Manage MySQL HeatWave DB System
- Backup MySQL HeatWave DB System
- Configure MySQL HeatWave DB System
- Setup MySQL HeatWave Read Replicas
- Setup MySQL HeatWave Inbound Replication
- Migrate Data Into MySQL HeatWave
- Setup MySQL HeatWave High Availability
- Load Airportdb Data into HeatWave
- Run Queries in HeatWave and MySQL
- Create and Test HeatWave Lakehouse
- (Bonus) Build Oracle Analytics Cloud Dashboard with HeatWave
- Create and Test HeatWave Machine Learning
- (Bonus) Build LAMP Application with MySQL HeatWave
- (Bonus) Develop MySQL HeatWave Apps with Oracle APEX
- Stop OCI Services


## Prerequisites

- An Oracle Trial, Paid or LiveLabs Cloud Account
- Some Experience with MySQL Shell - [MySQL Site](https://dev.MySQL.com/doc/MySQL-shell/8.0/en/).

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, March 2024
