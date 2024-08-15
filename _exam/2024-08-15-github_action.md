## 1. Github Action 전체 Flow
![image](https://github.com/user-attachments/assets/1f454113-be9c-472b-99cd-73c6ad5cd176)

## 2. Github Action Event
```
1) Single Event
on: push

2) Multiple Event
on: [push, pull_request]

3) Type별 Event
on:
  push:
    branches:
      - main 
      - 'rel/v*'
    tags:
      - v1.*
      - beta  
    paths:
      - '**.ts'  
```
