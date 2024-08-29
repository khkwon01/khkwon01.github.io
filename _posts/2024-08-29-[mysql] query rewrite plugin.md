---
layout: post
---

MySQL에 들어오는 query문을 query rewriter plugin를 사용하여 변경 처리 할 수 있습니다.

(사용예, 제약조건으로 forigen key를 가지지 못하는 파티션 테이블에 대해서 forigen key를 가진 원테이블을 통해서 무결성 검증을 할수 있습니다.)

## 1. 설치
```bash
mysql -u root -p < install_rewriter.sql
```

## 2. enable 체크
```sql
SHOW GLOBAL VARIABLES LIKE 'rewriter_enabled';

SET GLOBAL rewriter_enabled = ON;
SET GLOBAL rewriter_enabled = OFF;
```

## 3. 사용
query rewriter는 select, insert, replace, update, delete 구문에 적용 가능함

- rule 등록
  
```sql
INSERT INTO query_rewrite.rewrite_rules (pattern, replacement)
VALUES('SELECT ?', 'SELECT ? + 1');
```

- rule 반영
  
```sql
CALL query_rewrite.flush_rewrite_rules();
SELECT * FROM query_rewrite.rewrite_rules\G;
```

- rule 수정
  
```sql
UPDATE query_rewrite.rewrite_rules SET enabled = 'NO' WHERE id = 1;
CALL query_rewrite.flush_rewrite_rules();
```
