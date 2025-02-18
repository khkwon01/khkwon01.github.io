---
layout: post
---

## 소개

OCI Database Migration 서비스는 MySQL 마이그레이션을 지원합니다. 이 가이드를 사용하여 최소한의 다운타임으로 AWS RDS for MySQL 데이터베이스를 HeatWave MySQL 데이터베이스로 마이그레이션하는 방법에 대한 단계별 지침을 확인하세요.

이 서비스는 검증된, 교차 버전, 내결함성 및 증분적 동종 Oracle 및 MySQL 마이그레이션을 제공합니다. 고급 오케스트레이션 자동화, 소스 및 대상 호환성 진단 및 수정, 통합된 사용자 경험을 통해 데이터베이스 마이그레이션 워크플로를 간소화합니다. 마이그레이션 시나리오는 단기 또는 장기적일 수 있으며 데이터베이스 다운타임이 있거나 없이 수행되어 운영 중단을 제거합니다.

![image](https://github.com/user-attachments/assets/3f0a922e-976c-41e4-856a-2e4d914cdd7c)


## 이관 시나리오

### MySQL 인스턴스용 AWS RDS:

- MySQL Community version 8
- Non-multitenant architecture
- 바이너리 로깅을 활성화합니다. 백업 보관 기간을 0이 아닌 양의 값으로 설정합니다
- 인스턴스를 공개적으로 접근 가능하게 설정합니다.
- DB 인스턴스 매개변수 그룹에는 다음 값이 포함되어야 합니다.
  - binlog_row_metadata=FULL
  - binlog_row_image= FULL
  - binlog_format= ROW
  - log_bin=1

### Oracle 클라우드 인프라:

- 다음 [지침](https://docs.oracle.com/en/cloud/paas/database-migration/dmsus/getting-started-oracle-cloud-infrastructure-database-migration.html#GUID-30481DFD-08D7-4D38-A952-3D81138AB71C) 에 따라 OCI 데이터베이스 마이그레이션 작업에 필요한 리소스를 생성하세요.
- 이 블로그에서는 타겟으로 사용할 기존 OCI HeatWave MySQL 데이터베이스인 버전 8.4.0을 사용했습니다.

### 1단계: AWS RDS 인스턴스 연결 세부 정보 식별

먼저 RDS DB 인스턴스의 엔드포인트(DNS 이름)와 포트 번호를 찾습니다.

탐색: Amazon RDS 홈페이지>데이터베이스>귀하의 DB> 연결 및 보안 탭

![image](https://github.com/user-attachments/assets/ee9cebf9-7e77-403a-838c-4a153ef8bfed)

OCI 데이터베이스 마이그레이션에는 IP 주소가 필요합니다 . 다음 명령인 nslookup + RDS Private Endpoint는 다음과 유사한 응답을 표시해야 합니다. IP 주소를 기록해 두세요.

![image](https://github.com/user-attachments/assets/ae10eef9-c0ee-4e1a-9349-546bf15a5b65)

구성 탭 에서 다음 정보를 찾으세요.

- DB 이름 (DB 인스턴스 ID가 아님)
- 마스터 사용자 이름

![image](https://github.com/user-attachments/assets/ac77719a-a1ab-48d0-853f-13f00b690d75)

### OCI 데이터베이스 마이그레이션 시작하기

### 2단계: OCI 데이터베이스 마이그레이션에서 소스 RDS 데이터베이스에 대한 데이터베이스 연결 생성

데이터베이스 연결 리소스는 소스 및 대상 데이터베이스 간의 네트워킹과 연결을 활성화합니다.

탐색: 마이그레이션 및 재해 복구 > 데이터베이스 마이그레이션 > 데이터베이스 연결 로 이동: 연결 만들기를 누릅니다 . 일반 정보
페이지에서 다음 항목을 채우고, 그렇지 않으면 기본값을 그대로 둡니다.

- Name : 데이터베이스 연결에 대한 이름을 제공합니다
- Compartment : 구획을 선택하세요
- Type : Amazon RDS for MySQL
- Vault : Select your previously created vault
- Encryption key: Select your previously created key

![image](https://github.com/user-attachments/assets/3e43c8f8-6412-48cc-a064-f46956a6555e)

연결 세부 정보 페이지에서 다음 항목을 입력하고, 그렇지 않은 경우 기본값을 그대로 둡니다.

- 데이터베이스 이름: 데이터베이스의 이름
- 호스트 : 소스 데이터베이스의 공개 IP
- 포트 : 3306
- 초기 로드 데이터베이스 사용자 이름 : 마스터 사용자 이름을 입력하세요(이 연습에서는 admin)
- 초기 로드 데이터베이스 비밀번호 : 비밀번호를 입력하세요
- 이 데이터베이스에 액세스하려면  개인 엔드포인트 만들기를 선택하세요

![image](https://github.com/user-attachments/assets/610c1dcf-8424-4d55-b34d-49e734ab5216)

연결이 활성화 되면 연결 테스트 버튼을 클릭하여 연결이 작동하는지 확인합니다. 성공적인 결과를 받지 못한 경우 연결 메시지를 검토하고 연결 세부 정보를 수정합니다.

![image](https://github.com/user-attachments/assets/a2466f7b-bcb4-40cd-80d7-706006585726)

### 3단계: HeatWave MySQL 데이터베이스 시스템(대상)에 대한 데이터베이스 연결 생성

일반 정보 페이지에서 다음 항목을 입력하고, 그렇지 않은 경우 기본값을 그대로 두세요.

- Name: 데이터베이스 연결에 대한 이름을 제공합니다.
- Compartment : 구획을 선택하세요
- Type: OCI MySQL Heatwave
- Vault: Select your previously created vault
- Encryption key: Select your previously created key

![image](https://github.com/user-attachments/assets/ad189d8a-4cd0-49dc-8613-79caa3de9b55)

연결 세부 정보 페이지에서 다음 항목을 입력하고, 그렇지 않은 경우 기본값을 그대로 둡니다.

- 데이터베이스 세부 정보, MySQL 데이터베이스 시스템 선택
- 데이터베이스 시스템 : 값 목록에서 Heatwave 인스턴스를 선택하세요
- 데이터베이스 이름 : RDS for MySQL과 동일한 데이터베이스 이름을 입력하세요.
- 초기 로드 데이터베이스 사용자 이름 : 마스터 사용자 이름을 입력하세요(이 연습에서는 admin)
- 초기 로드 데이터베이스 비밀번호 : 비밀번호를 입력하세요
- 이 데이터베이스에 액세스하려면 개인 엔드포인트 만들기를 선택하세요
- 올바른 개인 서브넷을 선택하세요

![image](https://github.com/user-attachments/assets/5b90986c-9c77-42e9-9597-0aeddd03ea7f)

새로운 연결을 테스트하기 위해 단계를 반복합니다. 연결이 활성화되면 연결 테스트 버튼을 클릭하여 연결이 작동하는지 확인하고 테스트가 성공하면 계속 진행합니다.

### 4단계: 마이그레이션 만들기

OCI Database Migration으로 마이그레이션을 만들 때 마이그레이션을 어떻게 실행해야 하는지 지정하고, 소스 및 대상 데이터베이스 연결을 선택한 다음 데이터 전송 설정을 구성합니다. 선택적으로 고급 GoldenGate 및 MySQL Shell 설정을 구성할 수 있습니다.

탐색: 마이그레이션 및 재해 복구 > 데이터베이스 마이그레이션 > 마이그레이션 으로 이동 : 마이그레이션 생성을 누릅니다.

일반 정보 페이지에서 다음 항목을 입력하고, 그렇지 않은 경우 기본값을 그대로 둡니다.

- 이름 : 마이그레이션에 대한 이름을 제공합니다.
- Compartment : 구획을 선택하세요

![image](https://github.com/user-attachments/assets/951a41cf-dbc0-46d1-911f-b06ebded1201)

데이터베이스 선택 페이지에서 다음 항목을 입력하고, 그렇지 않으면 기본값을 그대로 둡니다.

- 소스 데이터베이스, 데이터베이스 연결: 소스 데이터베이스 연결 (RDS 데이터베이스의 데이터베이스 연결)을 선택합니다.
- 대상 데이터베이스, 데이터베이스 연결: HeatWave MySQL 데이터베이스 시스템에 대한 대상 데이터베이스 연결을 선택하세요 .

![image](https://github.com/user-attachments/assets/87d66d44-7e66-49e6-a8d4-3663d45ede00)

마이그레이션 옵션 페이지에서 다음 항목을 입력하고, 그렇지 않은 경우 기본값을 그대로 둡니다.

- Object Storage bucket: 값 목록을 사용하여 이전에 만든 스토리지 버킷을 선택합니다.
- Online replication option 사용 체크
  - 이렇게 하면 서비스에 OCI GoldenGate 인스턴스를 프로비저닝하도록 지시하게 되며 , 이는 사용자에게 투명하게 이루어지며 관리나 모니터링이 필요하지 않습니다.

![image](https://github.com/user-attachments/assets/96b87def-9deb-4575-8ece-d4f74bb4815a)

### 5단계: 마이그레이션 검증

OCI 데이터베이스 마이그레이션에서 마이그레이션 리소스에 대한 마이그레이션 작업을 실행 하려면 먼저 마이그레이션 리소스의 유효성을 검사 해야 합니다.

탐색: 마이그레이션 및 재해 복구 > 데이터베이스 마이그레이션 > 마이그레이션 > 마이그레이션 선택 > 마이그레이션 세부 정보 로 이동

![image](https://github.com/user-attachments/assets/81f02a36-2c79-4e15-aa87-d0bc60a25526)

마이그레이션 리소스가 검증된 후 마이그레이션 작업을 실행할 수 있습니다.

### 6단계: 마이그레이션 작업 시작

탐색: 마이그레이션 및 재해 복구 > 데이터베이스 마이그레이션 > 마이그레이션 > 마이그레이션 선택 > 마이그레이션 세부 정보 로 이동

마이그레이션 작업이 시작되면 지정된 단계에서 일시 중지 하도록 구성한 다음 준비가 되면 다시 시작할 수 있습니다.

확인 대화 상자가 열리고, 거기서 작업을 Require User Input After에서 단계를 선택하여 언제든지 일시 중지하도록 구성할 수 있습니다. 사전 선택된 값은 Monitor replication lag 입니다 . 이 단계는 Replicat이 대상 데이터베이스를 따라잡을 때까지 Oracle GoldenGate Extract 및 Replicat 작업을 모니터링합니다. 종단 간(E2E) 복제 지연은 30초 미만이어야 합니다.

![image](https://github.com/user-attachments/assets/4a0e618b-a50c-4027-9c54-55daf726b502)

일시 중지할 선택된 단계 가 완료 되면 작업은 재개(또는 종료)될 때까지 대기 상태로 전환됩니다. Monitor Replication Lag 단계 후에 일시 중지하도록 선택된 경우 트랜잭션 복제는 대기 상태 동안 계속됩니다. 재개 시 중지됩니다.

![image](https://github.com/user-attachments/assets/029e25d3-6caa-4f14-805d-a96d0c24cdcd)

이 단계에서는 다음을 수행합니다.

- 복제 E2E 지연이 30초 이내로 유지되도록 보장합니다.
- Extract가 소스 데이터베이스에서 미처리 거래를 캡처했는지 확인합니다.
- 추출 중지
- Replicat이 나머지 모든 트레일 파일 데이터를 적용했는지 확인합니다.
- 복제 중지

단계 전환이 완료된 후 대상 데이터베이스의 작업 부하(다운타임 종료)를 시작할 수 있습니다.

마지막 단계는 정리 입니다 . 이 단계는 GoldenGate Extract 및 GoldenGate Replicat 프로세스와 소스 및 대상 데이터베이스의 연결 세부 정보를 각각 삭제하는 것과 같은 정리 작업을 수행합니다. 

![image](https://github.com/user-attachments/assets/26a07c0b-64e5-47e8-a817-30bd9fdc63b4)

### 결론:

OCI Database Migration(DMS)은 온프레미스 또는 클라우드 배포에서 OCI로 Oracle 데이터베이스를 마이그레이션합니다. 사용하기 쉬운 그래픽 사용자 환경은 마이그레이션 워크플로를 검증하고 관리합니다. MySQL 마이그레이션을 위한 DMS는 MySQL Shell을 초기 로드 엔진으로, Premigration Advisor Tool 및 Oracle GoldenGate 서비스를 사용하여 안전하고 내결함성이 뛰어나며 증분형 마이그레이션을 수행합니다.





