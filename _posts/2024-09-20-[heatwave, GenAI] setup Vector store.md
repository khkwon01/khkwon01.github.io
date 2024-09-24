---
layout: post
---

```
-- option 설정
> set @options = JSON_OBJECT("table_name", "demo_embeddings", "language", "en");

-- object storage bucket에 있는 문서(pdf, ppt, html...)를 vector table로 로딩
> call sys.VECTOR_STORE_LOAD('https://objectstorage.ap-chuncheon-1.oraclecloud.com/p/~~~/b/genai/o/', @options);

+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| task_id | task_status_query                                                                                                                                                                |
+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|       3 | SELECT id, name, message, progress, status, scheduled_time,estimated_completion_time, estimated_remaining_time, progress_bar FROM mysql_task_management.task_status WHERE id=3\G |
+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.0932 sec)

Query OK, 0 rows affected (0.0932 sec)

-- 진행 상태 확인
 MySQL  10.0.20.109:3306 ssl  ragdb  SQL > SELECT id, name, message, progress, status, scheduled_time,estimated_completion_time, estimated_remaining_time, progress_bar FROM mysql_task_management.task_status WHERE id=3\G
*************************** 1. row ***************************
                       id: 3
                     name: Vector Store Loader
                  message: Task starting.
                 progress: 0
                   status: RUNNING
           scheduled_time: 2024-09-20 03:30:31
estimated_completion_time: NULL
 estimated_remaining_time: NULL
             progress_bar: __________
1 row in set (0.0011 sec)

```
