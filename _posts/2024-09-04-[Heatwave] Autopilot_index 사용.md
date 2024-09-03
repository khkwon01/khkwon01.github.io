---
layout: post
---


## 1. Autopilot index 설명

MySQL 9.0.0부터 HeatWave Autopilot Advisor에는 워크로드 성능을 향상시키기 위해 보조 인덱스 제안을 제공할 수 있는 Autopilot Indexing이 포함되어 있습니다.

- Autopilot Indexing은 인덱스 추가 및 삭제에 대한 권장 사항을 생성합니다.

## 2. 사용방법

### 1) 전체 schema 대상 확인
```
CALL sys.autopilot_index_advisor(NULL);
```

### 2) 특정 스키마 대상 확인
```
-- test가 확인 스키마
CALL sys.autopilot_index_advisor(JSON_OBJECT('target_schema', JSON_ARRAY('test')));
```

### 3) 수행 결과 화면
```
+----------------------------+
| INITIALIZING INDEX ADVISOR |
+----------------------------+
| Version: 1.00              |
|                            |
| Output Mode: normal        |
| Target Schemas: All        |
|                            |
+----------------------------+
5 rows in set (0.0093 sec)

+---------------------------------------------------------+
| ANALYZING DATA                                          |
+---------------------------------------------------------+
| Total 32 table(s) for 3 schema(s)                       |
|                                                         |
| Total Data size:  2.32 GiB                              |
| Total Index size: 4.74 GiB                              |
|                                                         |
| SCHEMA                             TABLE         COLUMN |
| NAME                               COUNT          COUNT |
| ------                             -----         ------ |
| `airportdb`                           14            106 |
| `sakila`                              16             90 |
| `test`                                 2              4 |
|                                                         |
| TOTAL                                 32            200 |
|                                                         |
+---------------------------------------------------------+
14 rows in set (0.0093 sec)

+------------------------------------------------------------------------+
| INDEX SUGGESTIONS                                                      |
+------------------------------------------------------------------------+
| Statements analyzed: 12                                                |
|                                                                        |
| No Index suggestion produced                                           |
|   Reason: Current Indexes found to be optimal for the executed queries |
+------------------------------------------------------------------------+
```

### 4) 결과 별도로 확인
```
SELECT log->>"$.sql" AS "SQL Script" FROM sys.autopilot_index_advisor_report WHERE type = "sql" ORDER BY id;
SELECT JSON_PRETTY(log) AS "Explanations" FROM sys.autopilot_index_advisor_report WHERE type = "explain" ORDER BY id;
```
