# HeatWave로 Oracle Analytics Cloud 대시보드 구축

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## 세션 소개

MySQL HeatWave는 Oracle Cloud Analytics와 같은 기존 Oracle 서비스를 사용한 개발 작업에 쉽게 사용할 수 있습니다. -> Oracle Analytics Cloud(OAC)는 단일 통합 플랫폼에서 업계에서 가장 포괄적인 클라우드 분석을 제공하며, 여기에는 셀프 서비스 시각화 및 인라인 데이터 준비부터 기업 보고, 고급 분석 및 사전 예방적 통찰력을 제공하는 자체 학습 분석이 포함됩니다.

MySQL HeatWave를 OAC와 함께 사용하면 MySQL 데이터를 탐색하고 협업 분석을 수행할 수 있습니다.

_Estimated Time: :_ 20 minutes 소요

### 목표

이 랩에서는 다음 작업을 안내해 드립니다 :

- Oracle Analytics Cloud를 생성하고 MySQL HeatWave에 연결
- airportdb에 대한 OAC 대시보드 만들기

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account
- MySQL Shell에 사용경험

## 작업 1:  Oracle Analytic Cloud 서비스 생성

1. OCI console에서, Analytics & AI-> Analytics Clouds 메뉴를 선택합니다.
 ![analytics menu](./images/analytics-menu.png " analytics menu")

2. 인스턴스 생성을 클릭합니다.
 ![create-instance-oac](./images/create-instance-oac.png "create-instance-oac ")

3. 인스턴스 생성에서 아래에 표시된 대로 필요한 정보를 입력합니다.

    Name:

    ```bash
    <copy>hwoac</copy> 
    ```

    Description:

    ```bash
        <copy>Oracle Analytics Cloud HeatWave Test</copy>
    ```

    Capacity: **OCPU** 선택하고 **1** 로 선택

    License Type: **License Included** 선택

4. **Create** button를 클릭합니다.

    ![configure oac](./images/config-oac.png "config-oac ")

5. OAC 인스턴스 생성이 완료되는 데 약 12~15분이 걸립니다.

    ![created oac](./images/created-oac.png " created-oac")

## 작업 2: Private Access Channel 구성

1. “Private Access Channel” 리소스 페이지로 가서 **Private Access Channel 구성** 버튼을 클릭합니다.

2. Private Access Channel 생성 버튼을 클릭합니다.

3. Private Access Channel 생성 페이지에서 다음을 입력하세요:

    Name:

    ```bash
         <copy>hwoacpac</copy>
    ```

    DNS Zones:
    **DNS 영역(hwvcn.oraclevcn.com)으로 Virtual Cloud Network의 도메인 이름을 확인하세요.**

    Description:

    ```bash
        <copy>Testing</copy>
    ```

    **두 번째 DNS 영역 항목 제거**

4. **Create** button 클릭합니다.

    ![configure private access for oac](./images/config-pac-oac.png " config-pac-oac")

5. 프로세스가 완료될 때까지 30분을 기다린 후 작업 3으로 계속 진행하세요.
    ![oac private access created  ](./images/created-pac-oac.png " created-pac-oac")

## 작업 3: HeatWave DB 호스트 이름 가져오기

1. 시작하기전에 Databases > DB Systems 메뉴로 이동합니다.

2. HeatWave database 선택합니다: HeatWave-DB

3. **Endpoint Link**에서 **Connections** 탭으로 이동합니다. **Internal FQDN**에서 show를 클릭하고 복사하여 메모장에 저장합니다.

    ![database endpoint](./images/hw-db-endpoint.png "hw-db-endpoint ")

4. OAC에서 사용할 호스트 이름 저장합니다.

    예제 : **hwdb.sub09012.....hwvcn.oraclevcn.com**

## 작업 4: OAC 대시보드 구축

1. 왼쪽 위 hamburger->Analytics->Analytics Clouds 이동

2. Analytics 홈페이지를 클릭하여 OAC 콘솔에 액세스하기 위해 프로비저닝(provisioned)한 OAC 인스턴스를 선택합니다.

    ![analytics go home page](./images/analytics-go-home-page.png "analytics-go-home-page ")

3. 대시보드를 구축하기 위해 HeatWave에 연결을 만듭니다.

    ![analytics home page](./images/analytics-home-page.png " analytics-home-page")

4. mysql을 검색하고 데이터베이스로 mysql을 선택하세요.

    예제 : **HEATWAVE-HW.sub0….heatwavevcn.oraclevcn.com**

    ![add mysql connection](./images/add-connection-mysql.png "add-connection-mysql ")

5. 연결 세부 정보를 지정하세요.

    - 4번 작업의 FQDN으로 HEATWAVE-DB의 호스트 이름을 지정하세요.
    - 반드시 MySQL 관리자 사용자 이름과 비밀번호를 사용하세요.

    ![config myql connection](./images/config-add-connection-mysql.png "config-add-connection-mysql ")

6. 이전에 생성한 MySQL 연결을 선택하세요.

7. 왼쪽 패널에서 "수동 쿼리(Manual Query)"를 두 번 클릭하고 하단에서 "수동 쿼리(Manual Query)" 탭을 클릭합니다.

    ![manual query](./images/manual-query-select.png "manual-query-select ")

8. 다음 SQL 쿼리(스위스, 이탈리아 및 프랑스 승객의 회사별 평균 연령 찾기)를 명세서 텍스트 상자에 추가하고 오른쪽의 데이터 액세스에서 "라이브"를 선택한 다음 상단에서 확인을 클릭합니다.

    ```bash  
    <copy> SELECT
        airline.airlinename,
        AVG(datediff(departure,birthdate)/365.25) as avg_age,
        count(*) as nbpeople
    FROM
        booking, flight, airline, passengerdetails
    WHERE
        booking.flight_id=flight.flight_id AND
        airline.airline_id=flight.airline_id AND
        booking.passenger_id=passengerdetails.passenger_id AND
        country IN ("SWITZERLAND", "FRANCE", "ITALY")
    GROUP BY
        airline.airlinename
    ORDER BY
        airline.airlinename, avg_age
    LIMIT 10;</copy>
    ```

9. Dataset 화면
    ![set oac dataset](./images/new-data-set-oac.png "new-data-set-oac ")

10. 저장 버튼을 클릭하고 DataSet 이름을 Passengers로 설정한 다음 통합 문서 만들기 버튼을 클릭합니다.
    ![create oac workbook](./images/create-workbook-oac.png "create-workbook-oac")

11. 새 페이지에서 데이터 세트 아이콘을 클릭하고 항공사(airline) 및 nbrpeople을 선택합니다.
    ![select columns](./images/passenger-column.png "passenger-column")

12. 마우스 오른쪽 버튼을 클릭하고 "최상의 시각화 만들기"를 선택하세요.
    ![auto visualization](./images/best-visualization-oac.png "best-visualization-oac")

13. 하단의 + 기호를 클릭하여 Canvas 2를 추가하고 항공사와 avg_age를 선택하세요.
    
14. 마우스 오른쪽 버튼을 클릭하고 "시각화 선택(Pick Visualization)"을 선택한 다음 원형 차트를 선택하세요.
    ![manual visualization](./images/pick-visualization-oac.png "pick-visualization-oac ")

15. 통합 문서를 "승객 통합 문서 (passenger Workbook)"로 저장하고 OAC 응용 프로그램을 닫습니다.

16. 다음 쿼리를 사용하여 OAC에 차트를 추가합니다.

    ```bash
    <copy>SELECT satisfaction,customer_type, travel_type, AVG(departure_delay) departure_delay,count(*) as nb_psgr
    FROM airportdb.passenger_survey
    group by customer_type,travel_type,satisfaction;</copy>
    ```

    ![delay satisfaction workbook](./images/delay-satisfaction.png "delay satisfaction")

이제 **다음 Lab으로 진행**할 수 있습니다.

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, Dec 2024
