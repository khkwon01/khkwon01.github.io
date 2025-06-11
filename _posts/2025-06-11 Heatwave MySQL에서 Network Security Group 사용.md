---
layout: post
---

## NSG

- 네트워크 보안 그룹(NSG)을 사용하면 서브넷 수준 보안 목록에만 의존하지 않고 VNIC 수준에서 상태 저장형 가상 방화벽 규칙을 적용할 수 있는 보안 아키텍처인 마이크로세그먼테이션이 가능합니다.

  (Network Security Groups (NSGs) enable microsegmentation a security architecture that allows you to apply stateful, virtual firewall rules at the VNIC level, rather than only relying on subnet-level security lists.)

- 많은 고객 환경에서 여러 워크로드가 동일한 VCN 내에 공존합니다.
  - web tier : OCI 컴퓨팅 인스턴스가 배포
  - backend tier : HeatWave MySQL등 서비스
  * NSG를 사용하면 정확한 네트워크 경로를 적용할 수 있습니다. 애플리케이션 컴퓨팅 인스턴스(예: App-1)만 데이터베이스(예: DB-1)와 통신할 수 있습니다.

## Heatwave NSG 

- NSG는 기본 DB 시스템과 해당 읽기 복제본(RR) 모두에서 지원됩니다.
- 각 DB 시스템 또는 읽기 복제본은 최대 5개의 NSG와 연결될 수 있습니다.
- NSG는 선택된 DB 시스템 또는 읽기 전용 복제본의 고객 관리 VNIC에 연결됩니다. 데이터베이스로 유입되는 모든 트래픽은 해당 NSG에 정의된 규칙에 따라 필터링됩니다.
- 읽기 복제본이 있는 DB 시스템의 경우 복제본의 네트워크 로드 밸런서(NLB)의 개인 엔드포인트(private endpoint)는 DB 시스템에 적용된 NSG 구성을 따릅니다.

## APP 및 Heatwave NSG 구성 절차

- 아래 예제 리소스에 대해
  
 | Source	    | Destination	| Protocol	 | Port	 | Rule   | Location  |
 |:---|:---|:---|:---|:---|:---          |
 | App-VM-1	  | HeatWave DB |	TCP  	     | 3306  | NSG    | Ingress   |  

- IAM 권한 설정 (IAM policies 추가필요)
  ```
  -- Allow HeatWave MySQL to update NSG membership 
  Allow any-user to {NETWORK_SECURITY_GROUP_UPDATE_MEMBERS} in compartment <NSG_compartment_name>
  where all {request.principal.type='mysqldbsystem', request.resource.compartment.id='<DBsystem_compartment_OCID>'
  }

  -- Allow VNIC operations required by HeatWave MySQL
  Allow any-user to {
  VNIC_CREATE,
  VNIC_UPDATE,
  VNIC_ASSOCIATE_NETWORK_SECURITY_GROUP,
  VNIC_DISASSOCIATE_NETWORK_SECURITY_GROUP
  } in compartment <subnet_compartment_name> 
    where all {request.principal.type='mysqldbsystem', request.resource.compartment.id='<DBsystem_compartment_OCID>'
  }
  ```

- 단계 1: Create Two NSGs
  - Compute instance : nsg-app-dev
  - HeatWave MySQL DB System : nsg-db-dev

  ![image](https://github.com/user-attachments/assets/0b2f8696-34e2-400b-a181-b4bdd82c4c34)

- 단계 2: Attach NSGs to Resources
  - Compute의 경우 VNIC를 편집하여 nsg-app-dev를 연결합니다.
  ![image](https://github.com/user-attachments/assets/2d1a5575-90f0-43e5-b80a-dccd62e805db)

  - DB 시스템을 프로비저닝할 때 nsg-db-dev를 할당합니다.
  ![image](https://github.com/user-attachments/assets/037b56ee-1108-4f12-8fa8-34c944e1b854)

- 단계 3: NSG rule 추가
  - Egress Rule (대상 : nsg-app-dev)
    ```
    Source Type: Network Security Group
    Source: nsg-db-dev
    Protocol: TCP
    Destination Port: 3306
    Stateless: No
    ```
    ![image](https://github.com/user-attachments/assets/7ab044fc-ce40-437e-b507-3bdd108edce1)

  - Ingress Rule (대상 : nsg-db-dev)
    ```
    Source Type: Network Security Group
    Source: nsg-app-dev
    Protocol: TCP
    Destination Port: 3306
    Stateless: No 
    ```
    ![image](https://github.com/user-attachments/assets/8e7c794a-1499-4495-b761-3d8d3c752e1e)

- 동작 : 이렇게 하면 nsg-app-dev의 트래픽만 포트 3306에서 HeatWave DB에 도달할 수 있습니다.
 
```
```
