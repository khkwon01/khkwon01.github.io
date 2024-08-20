MySQL Shell를 사용하여 MySQL diagnostic 정보를 수집하는 방법을 가이드합니다.

(참고로, Heatwave에서는 동작하지 않음)

## 1. 요구 조건
- slow_query_log : ON
- log_output : TABLE

## 2. 수집 방법

mysql shell에서 아래 명령어을 수행하면 아래 기술한 디렉토리에 mysql-diagnostics-<timestamp info>.zip 파일이 생성됨

- util.debug.collectDiagnostics("/users/my_user/diag/", {slowQueries: true, })

