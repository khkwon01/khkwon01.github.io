# Create and Test HeatWave Lakehouse

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## Introduction

MySQL HeatWave includes MySQL HeatWave Lakehouse, letting users query hundreds of terabytes of data in object storage—in a variety of file formats, such as CSV, Parquet, and Aurora/Redshift export files from other databases. Customers can query transactional data in MySQL databases, data in various formats in object storage, or a combination of both using standard MySQL commands. Querying data in object storage is as fast as querying data inside the database.

### Objectives

In this lab, you will be guided through the following tasks:

- Create Object Storage bucket
- Upload survey data
- Create PAR Link for the  survey file
- Run Autoload to infer the schema and estimate capacity
- Load survey table from Object Store into MySQL HeatWave cluster

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell

## Task 1: Download survey file to your local machine

1. Click on this link to **Download file [passenger_survey.csv](files/passenger_survey.csv)**  to your local machine

## Task 2: Create Object Storage bucket

1. Sign in to OCI using your tenant name, user name and password.
2. Once signed in select the **root** compartment
3. From the Console navigation menu, click **Storage**.
4. Under Object Storage, click Buckets

    **NOTE:** Ensure the correct Compartment is selected : Select **root**

    ![cloud storage bucket](./images/cloud-storage-bucket.png "cloud-storage-bucket")

5. Click Create Bucket. The Create Bucket pane is displayed.
6. Enter a Bucket Name **airport-survey**
7. Under Default Storage Tier, click Standard. Leave all the other fields at their default values.
8. Click Create

    ![press bucket button](./images/press-bucket-button.png "press-bucket-button")

## Task 3: Upload airport-survey data

1. In the Buckets page, click the **airport-survey** name to load images into. The bucket's details page is displayed.
2. Under Resources, click Objects to display the list of objects in the bucket.
3. Click Upload. The Upload Objects pane is displayed.
4. Select the **passenger_survey.csv** file from your local machine
    - Click open to load the passenger_survey.csv file
    - Click the Upload button
       ![bucket detail](./images/bucket-detail.png"bucket-detail.png")

    - Wait for the **Abort** to change into **close**
    - Click the **close** button

## Task 4: Create the PAR Link for the "airport-survey" files

1. To create a PAR URL
    - Go to menu **Storage —> Buckets**
     ![Bucket menu](./images/storage-bucket-menu.png "storage bucket menu")

    - Select **airport-survey**  folder.
2. Select the first file —> **passenger_survey.csv** and click the three vertical dots.
3. Click on **Create Pre-Authenticated Request**

    ![delivery-orders-1.csv 3 dots](./images/storage-create-par-orders.png "storage create par orders")

4. The **Object** option will be pre-selected.
5. Keep **Permit object reads** selected
6. Kep the other options for **Access Type** unchanged.
7. Click the **Create Pre-Authenticated Request** button.

    ![Create PAR](./images/storage-create-par-orders-page.png "storage create par orders page")

8. Click the **Copy** icon to copy the PAR URL.
    ![Copy PAR](./images/storage-create-par-orders-page-copy.png "storage create par orders page copy")

9. Save the generated PAR URL; you will need it in the next task

## Task 5: Setup MySQL HeatWave system for Lakehouse processing

1. Make sure HeatWave Lakehouse is enabled. If not then execute **Lab 4: Load Airportdb Data into HeatWave**

    ![Enabled HeatWave Lakehouse](./images/heatwave-lakehouse-enabled.png " Enabled HeatWave Lakehouse")

2. Go to Cloud shell to SSH into the Compute Instance

    (Example: **ssh -i ~/.ssh/id_rsa opc@132.145.170...**) 

    ```bash
    <copy>ssh -i ~/.ssh/id_rsa opc@<your_compute_instance_ip></copy>
    ```

3. Connect to the HeatWave Database using MySQL Shell with the following command:

    ```bash
    <copy>mysqlsh -uadmin -p -h 10.0.1... --sql </copy>
    ```

    ![MySQL Shell Connect](./images/mysql-shell-login.png " mysql shell login")

4. Change to SQL mode

    ```bash
    <copy>\sql</copy>
    ```

5. List schemas in your heatwave instance

    ```bash
    <copy>show databases;</copy>
    ```

    ![Databse Schemas](./images/list-schemas-after.png "list schemas after")

6. Change to the airportdb database

    Enter the following command at the prompt

    ```bash
    <copy>USE airportdb;</copy>
    ```

7. To see a list of the tables available in the airportdb schema

    Enter the following command at the prompt

    ```bash
    <copy>show tables;</copy>
    ```

    You are now ready to use Autoload to load a table from the object store into MySQL HeatWave

## Task 6: Run Autoload to infer the schema and estimate capacity required for the DELIVERY table in the Object Store

1. The survey information is in the passenger_survey.csv file in object store for which we have created a PAR URL in the earlier task. We will load the file for the passenger_survey table into MySQL HeatWave. Enter the following commands one by one and hit Enter.

2. This sets the schema we will load table data into. Don’t worry if this schema has not been created. Autopilot will generate the commands for you to create this schema if it doesn’t exist.

    ```bash
    <copy>SET @db_list = '["airportdb"]';</copy>
    ```

3. This sets the parameters for the table name we want to load data into and other information about the source file in the object store. Substitute the **(PAR URL)** below with the one you generated in the previous task:

    ```bash
    <copy>SET @dl_tables = '[{
    "db_name": "airportdb",
    "tables": [{
    "table_name": "passenger_survey",
    "dialect": {
        "format": "csv",
        "field_delimiter": ",",
        "record_delimiter": "\\n",
        "has_header": true,
        "is_strict_mode": false},
        "file": [{"par": "(PAR URL)"}]}]  }]';</copy>
    ```

    - It should look like the following example (Be sure to include the PAR Link inside at of quotes("")):

        ![Load script set table](./images/load-script-set-table.png "Load script set table")

    - Run the set table script now.

4. This command populates all the options needed by Autoload:

    ```bash
    <copy>SET @options = JSON_OBJECT('mode', 'dryrun',  'policy', 'disable_unsupported_columns',  'external_tables', CAST(@dl_tables AS JSON));</copy>
    ```

5. Run this Autoload command:

    ```bash
    <copy>CALL sys.heatwave_load(@db_list, @options);</copy>
    ```

6. Once Autoload completes running, its output has several pieces of information:
    - a. Whether the table exists in the schema you have identified.
    - b. Auto schema inference determines the number of columns in the table.
    - c. Auto schema sampling samples a small number of rows from the table and determines the number of rows in the table and the size of the table.
    - d. Auto provisioning determines how much memory would be needed to load this table into HeatWave and how much time loading this data take.

7. Autoload also generated a statement lke the one below. Execute this statement now.

    ```bash
    <copy>SELECT log->>"$.sql" AS "Load Script" FROM sys.heatwave_autopilot_report WHERE type = "sql" ORDER BY id;</copy>
    ```

    ![Dryrun script](./images/load-script-dryrun.png "load script dryrun")

8. The execution result conatins the SQL statements needed to create the table and then load this table data from the Object Store into HeatWave.

    ![create passenger survey script](./images/create-passenger-survey-script.png "create passenger survey script")

9. Copy the **CREATE TABLE** command from the results. It should look like the following example

    ![create passenger survey script copy](./images/create-passenger-survey-script-copy.png "create passenger survey script copy")  

10. Execute the modified **CREATE TABLE** command to create the passenger_survey table.

11. The create command and result should look lie this

    ![Delivery Table create](./images/create-survey-table.png "create delivery table")

## Task 7: Load complete passenger_survey table from Object Store into MySQL HeatWave

1. Run this command to see the created table structure .

    ```bash
    <copy>desc passenger_survey;</copy>
    ```

    ![Passenger Survey Table](./images/passenger-survey-table.png "Passenger Survey Table")

2. Now load the data from the Object Store into the passenger_survey table.

    ```bash
    <copy> ALTER TABLE `airportdb`.`passenger_survey` SECONDARY_LOAD; </copy>
    ```

3. Once Autoload completes, check the number of rows loaded into the table.

    ```bash
    <copy>select count(*) from passenger_survey;</copy>
    ```

4. View a sample of the data in the table.

    ```bash
    <copy>select * from passenger_survey limit 5;</copy>
    ```

    a. Join the passenger_survey table with another table in the schema

    ```bash
    <copy> select p.* , ps.* from passenger p 
    join passenger_survey ps on p.passenger_id = ps.ID
    where p.passenger_id = 28; </copy>
    ```

5. Your output for steps 2 thru 5 should look like this:

    ![Passenger Survey Output](./images/passenger-survey-output.png "Passenger Survey Output")

6. Your passenger_survey table is now ready to be used in queries with other tables.

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, March 2024
