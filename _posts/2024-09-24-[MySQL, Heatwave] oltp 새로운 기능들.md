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

