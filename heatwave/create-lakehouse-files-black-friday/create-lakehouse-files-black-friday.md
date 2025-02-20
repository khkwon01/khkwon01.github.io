# Upload data to Object Storage for HeatWave Lakehouse - black-friday

## Introduction

A set of files have been created for you to use in this workshop. You will create an object storage bucket and upload the files to it.

### Objectives

- Download and unzip  Sample files
- Create Object Storage bucket
- Add files into  the Bucket using the saved PAR URL

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell
- Completed Lab 5

## Task 1: Download and unzip  Sample files

1. If not already connected with SSH, on Command Line, connect to the Compute instance using SSH ... be sure replace the  "private key file"  and the "new compute instance ip"

     ```bash
    <copy>ssh -i private_key_file opc@new_compute_instance_ip</copy>
     ```

2. Setup folder to house imported sample data

    a. Go to home directory

    ```bash
    <copy>cd ~ </copy>
     ```

    b. Create folder in home directory

    ```bash
    <copy>mkdir lakehouse</copy>
     ```

    c. Go into folder

    ```bash
    <copy>cd lakehouse</copy>
     ```

3. Download sample files

    ```bash
    <copy>wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/Ukv1g5qyvJK6asGvVoksGkUDIu8KaoVfmbhBzpmbRahXu7a2EmaVTJev2a-lHvUa/n/mysqlpm/b/mysql_customer_orders/o/black_friday.zip</copy>
     ```

4. Unzip black_friday.zip file which will generate 2 different files

    ```bash
    <copy>unzip black_friday.zip</copy>
     ```

5. List the files

    ```bash
    <copy>ls -l</copy>
    ```

    ![bucket file list](./images/datafiles-list.png "datafiles list")

## Task 2: Create Object Storage bucket

1. From the Console navigation menu, click **Storage**.
2. Under Object Storage, click Buckets
    ![bucket menu](./images/cloud-storage-menu.png "cloud storage menu")

    **NOTE:** Ensure the correct Compartment is selected : Select **lakehouse**

3. Click Create Bucket. The Create Bucket pane is displayed.

    ![bucket create pane](./images/cloud-storage-bucket.png "cloud storage bucket")

4. Enter the Bucket Name **lakehouse-files**
5. Under Default Storage Tier, click Standard. Leave all the other fields at their default values.

    ![Add bucket name](./images/create-lakehous-bucket.png "create bucket")

6. Create the  Pre-Authenticated Request URL for the bucket
     - a. Click on the 3 dots to the right of the **lakehouse-files** bucket  Click on ‘Create Pre-Authenticated Request’
        ![lakehouse-files 3 dots](./images/create-lakehous-bucket-par-dots.png "bucket par dots")
        ![Create PAR](./images/create-lakehous-bucket-par-load.png "bucket par load")
     - b. The ‘Bucket’ option will be pre-selected
     - c. For 'Access Type' select 'Permit object write
     - d. Click the Create "Pre-Authenticated Request' button
        ![PAR Button](./images/create-lakehous-bucket-par-load-button.png " bucket par load button")
     - e. Click the ‘Copy’ icon to copy the PAR URL
        ![Copy PAR](./images/create-lakehous-bucket-par-copy-load.png "bucket par load copy")
     - f. Save the generated PAR URL; you will need it in the next task

## Task 3: Add files into  the Bucket using the saved PAR URL

1. Go into the lakehouse folder and list all of the files

    ```bash
    <copy>cd ~/lakehouse</copy>
    ```

    ```bash
    <copy>ls -l</copy>
    ```

    ![bucket file list](./images/datafiles-list.png "datafiles list")

2. Add the black\_friday\_train.csv file to the storage bucket by modifying the following statement with the example below. You must replace the **(PAR URL)** value with the saved generated **PAR URL** from the previous Task.

    ```bash
    <copy>curl -X PUT --data-binary '@black_friday_train.csv' (PAR URL)black_friday_train.csv</copy>
     ```

     **Example**  
     curl -X PUT --data-binary '@black\_friday\_train.csv' https://objectstorage.us-ashburn-1.oraclecloud.com/p/RfXc55AGpLSu26UgqbmGxbWZwh4hPhLkVWYMg4f5pNerQx_1NghgSKJHLzE4IWxH/n/******/b/lakehouse-files/o/black_friday_train.csv

3. Add the @black\_friday\_test.csv file to the storage bucket by modifying the following statement with the example below. You must replace the **(PAR URL)** value with the saved generated **PAR URL** from the previous Task.

    ```bash
    <copy>curl -X PUT --data-binary '@black_friday_test.csv' (PAR URL)black_friday_test.csv</copy>
     ```

     **Example**  
     curl -X PUT --data-binary '@black\_friday\_test.csv' https://objectstorage.us-ashburn-1.oraclecloud.com/p/RfXc55AGpLSu26UgqbmGxbWZwh4hPhLkVWYMg4f5pNerQx_1NghgSKJHLzE4IWxH/n/******/b/lakehouse-files/o/black_friday_test.csv

4. Your **lakehouse-files** bucket should look like this:
    ![cloud storage bucket](./images/lakehouse-bucket.png "lakehouse bucket")

You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Solution Engineering

- **Contributors** - Abhinav Agarwal, Senior Principal Product Manager, Nick Mader, MySQL Global Channel Enablement & Strategy Manager
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, May 2023
