## 1. 구성 아키텍처

![image](https://github.com/user-attachments/assets/13a07778-5fa5-46a4-91c5-98717b7608fe)


## 2. 구성 프로세스
- 메인 소스 데이터베이스 및 데이터 구성
- 메인 소스 데이터베이스 백업
- 백업 받은 데이터를 다른 리젼으로 이동
- 다른 리젼으로 이동된 백업 데이터로 replica용 DB 생성
- 메인 소스 데이터베이스에 replication user 생성
- replica용으로 생성된 DB에 메인 소스 DB와 연결을 위한 channel 구성 및 연결

### 1. 메인 소스 데이터베이스 및 데이터 구성
- Heatwave MySQL DB생성
![image](https://github.com/user-attachments/assets/3d33672f-df28-49fc-ae18-0de9f03b6909)

- MySQL 생성후 IP 확인 및 해당 IP로 접근하여 사용자 데이터 이관
![image](https://github.com/user-attachments/assets/d5063f6c-f2ac-4ac7-ba43-d9ef48549389)

### 2. 메인 소스 데이터베이스 백업 및 다른 리젼으로 이동
- Manual 방식으로 백업 생성
![image](https://github.com/user-attachments/assets/8cb011ed-b61e-4ba9-974b-d37f069dd679)
![image](https://github.com/user-attachments/assets/6a7ff92c-6fc1-40be-9044-9717a2301d46)

### 3. 백업 받은 데이터를 다른 리젼으로 이동
- 백업 데이터에 메뉴중 아래 "Copy to another region" 선택하여 다른 리젼으로 이동
![image](https://github.com/user-attachments/assets/ec09dbca-4142-439e-af92-b803feb4e6b8)

- 리젼과 optional 항목에 대한 데이터 입력 후 copy 수행
![image](https://github.com/user-attachments/assets/74096f42-fa3d-43a7-97ad-c844ab5aaf9c)

### 4. 다른 리젼으로 이동된 백업 데이터로 replica용 DB 생성
- 다른 리젼으로 이동된 백업 데이터를 선택하여 "Restore to new DB system" 클릭하여 replica db 생성
![image](https://github.com/user-attachments/assets/332acf4c-101e-4dfd-910d-c382846bebca)

- replica db 생성시 필요한 설정 입력후 Restore 클릭
![image](https://github.com/user-attachments/assets/2af13040-2a9c-4b2a-bf48-ad14d8ad44b9)

### 5. 메인 소스 데이터베이스에 replication user 생성
```
> CREATE USER rpl_admin@'%' IDENTIFIED BY '**********';
Query OK, 0 rows affected (0.0295 sec)
> GRANT REPLICATION SLAVE ON *.* TO rpl_admin@'%';
Query OK, 0 rows affected (0.0295 sec)
```

### 6. replica용으로 생성된 DB에 메인 소스 DB와 연결을 위한 channel 구성 및 연결
- 생성된 replica db에서 채널(replication) 생성
![image](https://github.com/user-attachments/assets/0e879c31-e12b-41f8-abc0-70e8d4955696)

- 채널 생성에 필요한 설정값 입력후 채널(replication) 생성
![image](https://github.com/user-attachments/assets/70d580fd-2b7f-47cc-bbf7-b9889b736825)
![image](https://github.com/user-attachments/assets/6f67f637-ffcf-429e-a676-26fc342757fe)

- 생성된 채널 확인
![image](https://github.com/user-attachments/assets/5963b956-b05c-4ff3-bbdf-920f617f620d)


### 참조. 다른 리젼과 연결을 위한 DRG구성은 아래 URL 참조
- https://lefred.be/content/setup-disaster-recovery-for-oci-mysql-database-service/

