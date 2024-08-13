---
layout: post
---

## Heatwave Lakehouse 초기 데이터 load
- 다음 SQL로 object storage에 있는 파일 데이터를 heatwave cluster로 초기 적재함
  
```sql
SET @input_list = '[   {"db_name": "AutoML", "tables": [{ "table_name": "bank_marketing",    
                              "engine_attribute": {       
                                "dialect": {         
                                        "format": "csv",
                                        "has_header": true,
                                        "field_delimiter": ";", 
                                        "record_delimiter": "\\n"  },   
                              "file": [{"par": "https://objectstorage.ap-chuncheon-1.oraclecloud.com/p/~~~/b/ml-lake-test/o/", "pattern" : "bank.*"}]     }   }]} ]';

SET @options = JSON_OBJECT('mode', 'normal');

call sys.heatwave_load(@input_list, @options);
```

## 초기 적재 후 object storage에 새로 데이터 추가, 삭제, 변경시
- object storage에 새로운 파일들을 추가 하거나, 변경후 아래 명령어를 수행하면 자동으로 반영됨.
  
```sql
SET SESSION rapid_lakehouse_refresh = TRUE;
ALTER TABLE /*+ AUTOPILOT_DISABLE_CHECK */ AutoML.bankfull secondary_load;
SET SESSION rapid_lakehouse_refresh = FALSE;

or 

SET @db_list = '[<schema>]';
SET @options = JSON_OBJECT('mode','normal','refresh_external_tables', TRUE,'include_list',JSON_ARRAY(<tables>));
CALL sys.heatwave_load(@db_list, @options);
```


