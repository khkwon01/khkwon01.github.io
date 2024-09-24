---
layout: post
---

## 1. HA(high availability) 및 DR(disaster recovery) 성능 향상

- DR를 위해 다른 리젼에 백업 copy 및 복구 지원
![image](https://github.com/user-attachments/assets/9d31779f-bce7-43ad-9495-08f2cfb28ae8)

- Heatwave cluster를 사용중인 MySQL HA에 대해서 shape 변경 지원
  - 기존에는 MySQL HA에서 shape 변경시 Heatwave cluster를 삭제하고 다시 만들어야 했으나, shape 변경 지원예정

## 2. 성능 향상 

- Hypergraph-based optimizer for MySQL 지원
  - 연관된 joins이 많은 복잡한 쿼리에 대해서 쿼리 plan를 cost 베이스로 최적화 지원
  - 사용방법
    ```
    -- 기능 on
    set optimizer_switch="hypergraph_optimizer=on”

    -- 기능 off
    set optimizer_switch="hypergraph_optimizer=off”
    ```

- Autopilot Indexing 지원
  - secondary indexes에 대해서 ML-based 데이터 기반으로 부하에 따라 사용자에게 index가 필요한지 필요없는지 가이드 제공
  ![image](https://github.com/user-attachments/assets/fb2332dc-3182-41eb-bf63-a7fe8537bb68)

- Bulk Ingest
  - MySQL 인스턴스 생성시 bulk 데이터 ingest 기능을 제공
  ![image](https://github.com/user-attachments/assets/0f62bd45-c634-4515-bd78-e38c4ea1b29d)


## 3. 관리 및 모니터링

- OCI Ops insight service 통합지원
  - OCI ops insight가 Heatwave MySQL에 대해서 ML-based 기반에 데이터 성능 관리 및 모니터링 기능을 확장하여 제공
  ![image](https://github.com/user-attachments/assets/b9e8742c-1b42-4092-90f6-3f5c41b61ecb)
    - 성능 사용 패턴 및 workload 트랜드 분석
    - MySQL에 성능 예측 및 분석
    - CPU, storage, 데이터베이스 등 포함하여 전체적으로 용량 계획 이점 제공
    - 구성된 리소스에 기반하여 향후 예상 사용량(consumption) 예측
    - 적정한 장애 조치를 위해 사전 사용률 기반 사전 알람 설정 지원

- Automatic Storage Expansion 지원
  - 서비스 부하에 추가적인 스토리지 리소스가 필요할 경우 해당 사항을 인지하여 스토리지를 자동으로 확장지원
  ![image](https://github.com/user-attachments/assets/0ad3ada0-6155-43c8-be4d-8c934b085f2c)

- inbound replication에 대해 virtual ip 주소 (vip) 지원
  - firewall 설정 및 security 구성을 간편하게 관리하기 위해 데이터베이스에 대한 virtual ip 지원


