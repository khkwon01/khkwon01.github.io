## 1. Github Action 전체 Flow
![image](https://github.com/user-attachments/assets/1f454113-be9c-472b-99cd-73c6ad5cd176)

- 문서 : https://docs.github.com/en/actions
  
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

4) Schedule Event
on:
  scheduled:
    - cron: '30 5,15 * * *'

5) Specific Manual Event
on: [workflow-dispatch, repository-dispatch]

6) Common Activity
on: issue_comment
```

## 3. Github Action Component
- steps : GitHub Actions로 작업할 때 처리하는 기본 실행 단위입니다.
  ```
  steps:
  - uses: actions/checkout@v4
  - name: setup Go version
    uses: actions/setup-go@v4
    with:
      go-version: '1.20.0'
  - run: go run helloworld.go
  ```
- Runners : 워크플로에 대한 코드가 실행되는 물리적 또는 가상 컴퓨터 또는 컨테이너입니다.
  ```
  runs-on: ubuntu-latest
  ```
- Jobs : steps 집계하고 이를 실행할 Runners를 정의합니다.
  ```
  jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: setup Go version'
        uses: actions/setup-go@v2
        with:
          go-version: '1.14.0'
      - run: go run helloworld.go
  ```
- workflow : pipeline와 유사한 역할을 합니다.
  ```
  name: Go

  on: [push]

  jobs:
    build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        go-version: [ '1.19', '1.20', '1.21.x' ]

    steps:
      - uses: actions/checkout@v4
      - name: Setup Go ${{ matrix.go-version }}
        uses: actions/setup-go@v5
        with:
          go-version: ${{ matrix.go-version }}
      # You can test your matrix by printing the current Go version
      - name: hello
        run: go run helloworld.go
    ```
