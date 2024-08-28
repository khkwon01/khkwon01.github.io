---
layout: post
---

# Heatwave Rest API 사용
- 전체 구성 flow  
![image](https://github.com/user-attachments/assets/78acbd39-5e80-49bb-ba84-cc69254ab1a7)


## Connection 설정 (Menu > Developer Services > Database Tools > Connection)
![image](https://github.com/user-attachments/assets/9688fb93-c638-4f7e-b297-369496d09139)

- Create connection 버튼 클릭 통해서 이미 구성된 Heatwave 서비스에 대한 connection 생성

## Private Endpoint 설정 (Menu > Developer Services > Database Tools > Private endpoints)
![image](https://github.com/user-attachments/assets/69787734-7e51-48a3-8b1c-939b41c5ff14)

- Create private endpoint 버튼 클릭 통해서 connection에 대한 private endpoint 구성 (보통 connection 생성시 같이 구성해야 함)

## client 예제를 통해서 rest api 방식으로 heatwave 테스트
```python
# coding: utf-8

import requests
from oci.config import from_file
from oci.signer import Signer

"""
oci 환경 접속을 위한 기본 인증 정보 설정
"""

config = from_file()
auth = Signer(
tenancy=config['tenancy'],
user=config['user'],
fingerprint=config['fingerprint'],
private_key_file_location=config['key_file'],
pass_phrase=config['pass_phrase']
)

"""
아래 endpoint는 고정 URL + connection ocid + /_/sql 로 구성

고정 URL : https://sql.dbtools.<<사용하는 region, ex) ap-seoul-1>>.oci.oraclecloud.com/20201005/ords/
"""


endpoint='https://sql.dbtools.ap-seoul-1.oci.oraclecloud.com/20201005/ords/ocid1.databasetoolsconnection.oc1.ap-seoul-1.amaaaaaacicuulyahwof7szzddyoyjup4wsjp66zs2cl7v5yaapehfji6kuq/_/sql'


headers={'Content-Type': 'application/sql'}
data='show databases'

response = requests.post(endpoint, data=data, headers=headers, auth=auth)

print(response.text)
```
