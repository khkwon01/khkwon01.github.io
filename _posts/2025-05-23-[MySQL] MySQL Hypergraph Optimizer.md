---
layout: post
---

## MySQL Hypergraph Optimizer 소개 (8.0.31 부터)

MySQL 또는 Heatwave에서 복잡한 쿼리에 대상으로 사용할 수 있습니다.


- Hypergraph 설정
```sql
MySQL > SET SESSION optimizer_switch='hypergraph_optimizer=on';
ERROR: 3999 (42000): The hypergraph optimizer does not yet support 
'use in non-debug builds'
```

- Hypergraph 사용 테스트 쿼리
```sql
MySQL > WITH salary_rank AS (     
     SELECT e.emp_no, e.first_name, e.last_name, d.dept_no, s.salary,
     RANK() OVER (
        PARTITION BY d.dept_no ORDER BY s.salary DESC
     ) AS dept_rank     
     FROM employees e     
     JOIN dept_emp d ON e.emp_no = d.emp_no     
     JOIN salaries s ON e.emp_no = s.emp_no     
    WHERE s.to_date = '9999-01-01' AND d.to_date = '9999-01-01' 
    ) SELECT * FROM salary_rank WHERE dept_rank = 1;
```

- 테스트 결과
  
MySQL에 일반적인 옵티마이저 (traditional optimizer)와 Hypergraph 옵티마이저 사용한 결과는 사용하는 쿼리에 따라 다르게 결과가 나옵니다.

Hypergraph는 현재 개발중인 옵티마이저로 주로 OLAP 쿼리에 좋은 결과를 만들어 냅니다.

- 일반적인 옵티마이저
```
+--------+------------+-----------+---------+--------+-----------+
| emp_no | first_name | last_name | dept_no | salary | dept_rank |
+--------+------------+-----------+---------+--------+-----------+
| 466852 | Akemi      | Warwick   | d001    | 145128 |         1 |
| 413137 | Lunjin     | Swick     | d002    | 142395 |         1 |
| 421835 | Yinlin     | Flowers   | d003    | 141953 |         1 |
| 430504 | Youjian    | Cronau    | d004    | 138273 |         1 |
|  13386 | Khosrow    | Sgarro    | d005    | 144434 |         1 |
| 472905 | Shin       | Luck      | d006    | 132103 |         1 |
|  43624 | Tokuyasu   | Pesch     | d007    | 158220 |         1 |
| 425731 | Ramachenga | Soicher   | d008    | 130211 |         1 |
|  18006 | Vidya      | Hanabata  | d009    | 144866 |         1 |
+--------+------------+-----------+---------+--------+-----------+
9 rows in set (2.1155 sec)
```

- Hypergraph 옵티마이저
```
+--------+------------+-----------+---------+--------+-----------+
| emp_no | first_name | last_name | dept_no | salary | dept_rank |
+--------+------------+-----------+---------+--------+-----------+
| 466852 | Akemi      | Warwick   | d001    | 145128 |         1 |
| 413137 | Lunjin     | Swick     | d002    | 142395 |         1 |
| 421835 | Yinlin     | Flowers   | d003    | 141953 |         1 |
| 430504 | Youjian    | Cronau    | d004    | 138273 |         1 |
|  13386 | Khosrow    | Sgarro    | d005    | 144434 |         1 |
| 472905 | Shin       | Luck      | d006    | 132103 |         1 |
|  43624 | Tokuyasu   | Pesch     | d007    | 158220 |         1 |
| 425731 | Ramachenga | Soicher   | d008    | 130211 |         1 |
|  18006 | Vidya      | Hanabata  | d009    | 144866 |         1 |
+--------+------------+-----------+---------+--------+-----------+
9 rows in set (1.6108 sec)
```

- 참고 자료 : https://lefred.be/content/mysql-hypergraph-optimizer/
