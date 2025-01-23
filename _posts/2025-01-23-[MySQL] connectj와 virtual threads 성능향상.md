---
layout: post
---

### 1. mysql connector-j 9.0 이전버전에서 발생하는 현상

- jdk21(19?) 출시 이후 microservices에 virtual thread를 사용할 수 있는데 mysql connector에 blocking 동작으로

  인해 최대성능을 사용하지 못하는 현상 발생

  ![image](https://github.com/user-attachments/assets/b3d14945-170a-400c-a1af-f9214129f441)

  위에 그림에서 200개 worker threads를 가지고 있는 tomcat은 더 많은 TPS를 처리할 수 있음에도 불구하여 mysql

  connector에 blocking 동작 방식으로 인해 200TPS 처리하는 한계가 발생.

  (JVM에서 해당 thead에 대해 thread dump를 수행하면 해당 현상을 확인 할 수가 있음)


### 2. mysql connector-j 9.0이후 해결

- mysql-connector-j/9.0.0 버전부터 해당 버그가 fix되어 해결됨 (blocking --> non-blocking으로 변경)

  (https://dev.mysql.com/doc/relnotes/connector-j/en/news-9-0-0.html)


  ![image](https://github.com/user-attachments/assets/3e312c55-02f3-4c3b-9953-2a01f4ff893a)

  위에 그림에서 보는 것처럼 mysql connector-j 9.0 사용함으로 tps 처리는 1000까지 증가함.

  tps 1000으로 제한 되는 사항은 springboot에서 사용하는 hikari 설정으로 인해 발생 하는 현상임

  (spring.datasource.hikari.maximum-pool-size=1000, spring.threads.virtual.enabled=true)

- 관련 참고 문서 : https://medium.com/naukri-engineering/virtual-threads-and-mysql-unlocking-performance-gains-with-mysql-connector-j-9-0-0-6754abc85f61
