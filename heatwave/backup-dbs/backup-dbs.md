# Backup MySQL DB System


## Introduction

In this lab, you will learn to manage backups in a MySQL DB System.

_Estimated Time:_ 15 minutes


### Objectives

In this lab, you will be guided through the following tasks:

- Create a Manual Backup 
- Edit the Backup Plan of a DB System
- Restore to a new DB System from a Manual Backup
- Restore to a new DB System from a Point-in-Time
- Delete unused MySQL Backups

### Prerequisites

- An Oracle Trial or Paid Cloud Account

## Task 1: Create a Manual Backup

1. Click **Navigation Menu**

    ![OCI Console Home Page](./images/homepage.png "home page")

2. Click  **Databases**, then **DB Systems**  
    ![menu databases](./images/menu-dbsystems.png "menu databases dbsystems")

    Make sure you are using the root compartment
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. Click on **HEATWAVE-DB** to view the deatils.  
    ![databases list](./images/list-dbsystem.png "list of dbsystem")

4. From the **More Actions** menu, select **Create Manual Backup** 
    ![databases click backup](./images/click-manual-backup.png "select create manual databases")

5. Fill in the information requested and then click on **Create Manual Backup**
    * Display Name: Manual Backup
    * Leave the description as is
    * Backup Type: Full Backup
    * Leave the Retention Period as is

    ![databases backup create](./images/create-manual-backup.png "create manual backup")

    **Note**: It may take a few minutes for the backup to complete

6. Click **Navigation Menu**, click  **Databases**, then **Backups**  
    ![menu databases](./images/menu-databases-backups.png "menu dbsystems backups")

    Confirm that Manual backup has been created successfully
    ![databases backup create](./images/create-manual-backup-complete.png "create manual backup complete")



## Task 2: Edit a Backup Plan

1. Click **Navigation Menu** 

    ![OCI Console Home Page](./images/homepage.png "home page")

2. Click  **Databases**, then **DB Systems**  
    ![menu databases](./images/menu-dbsystems.png "menu databases dbsystems")

     Make sure you are using the root compartment
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. Click on **HEATWAVE-DB** to view the deatils.  
    ![databases list](./images/list-dbsystem.png "list of dbsystem")

4. From the **More Actions** menu, select **Edit Backup Plan** 
    ![databases click backup](./images/click-edit-backup.png "select edit backup")

5. Enable **Automatic Backups** and fill the requested information
    * Backup Retention Period: 1
    * Window Start Time: 07:00 UTC
    * Enable Point in Time Recovery

    ![databases edit backup](./images/edit-backup-plan.png "edit backup plan") 

6. Click **Show backup windows per region**. A list of all backup windows per region will appear. If you don't define a backup window, Oracle will select one for you based on your region
    ![databases edit backup window](./images/edit-backup-plan-window.png "edit backup pla window")

7. Click **Save Changes** 


## Task 3: Restore a Backup to a New DB System

1. From the **More Actions** menu on your **HEATWAVE-DB** database, select **Restore to a new DB System** 
    ![databases click restore](./images/click-restore-backup.png "select restore backup")

2. Select **Restore from a backup**, then click the **Select backup** button to open the **Browse all backup** page 

    ![databases restore](./images/restore-from-backup.png "restore from backup")

3. Click the **Manual** button and select the check box next to the **Manual Backup** you created before. Then Click **Select Backup** 
    ![databases restore](./images/restore-backup-config.png "restore from manual backup config")

4. Ensure the root compartment is selected and enter the name of the new DB System, and Select **Standalone** option
    ```bash
    <copy>NEWDB</copy>
    ```
    ![databases restore](./images/restore-from-manual-backup.png "restore from manual backup")

5. Under Configure Networking section, ensure the HEATWAVE-VCN and its private subnet are selected 
    ![databases restore](./images/restore-backup-create-db.png "restore backup create-db")

6. Ensure that the **MySQL.HeatWave.VM.Standard** shape is selected. 

    ![databases restore](./images/restore-backup-create-db-shape.png "restore backup create db shape")

    If not, click on **Change Shape** and look for and select the **MySQL.HeatWave.VM.Standard** shape.

7. Leave **Data Storage Size** as it is.

8. On Configure Backups, disable 'Enable Automatic Backup'

    ![databases restore](./images/restore-edit-backup-plan.png "restore edit backup plan") 

9. Click on **Show Advanced Options** and go to the **Connections** tab, assign **NEWDB** as the new hostname. 

    Then click **Restore**

    ![databases restore](./images/restore-backup-create.png "restore from backup create")

    **Note**: It may take a few minures for the DB system to be created. When the DB System satate changes to Active, the DB System is ready to use.




## Task 4: Restore a Backup to a New DB System at a Point in Time

1. 1. Click **Navigation Menu**

    ![OCI Console Home Page](./images/homepage.png "home page")

2. Click  **Databases**, then **DB Systems**  
    ![menu databases](./images/menu-dbsystems.png "menu databases dbsystems")

    Make sure you are using the root compartment
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. Click on **HEATWAVE-DB** to view the deatils.  
    ![databases list](./images/list-dbsystem.png "list of dbsystem")

4. From the **More Actions** menu on your **HEATWAVE-DB** database, select **Restore to a new DB System** 
    ![databases click restore](./images/click-restore-backup.png "select restore backup")

5. Next, select **Restore from DB System at a point in time** option, and click on the **latest available point-in-time**

    ![databases restore](./images/restore-backup-pitr-config.png "restore from pitr backup config")


6. Ensure the root compartment is selected and enter the name of the new DB System, and Select **Standalone** option
    ```bash
    <copy>NEWDB2</copy>
    ```
    ![databases restore](./images/restore-from-pitr-backup.png "restore from pitr backup")

7. Under Configure Networking section, ensure the HEATWAVE-VCN and its private subnet are selected 
    ![databases restore](./images/restore-backup-create-db.png "restore backup create-db")

8. Ensure that the **MySQL.HeatWave.VM.Standard** shape is selected. 

    ![databases restore](./images/restore-backup-create-db-shape.png "restore backup create db shape")

    If not, click on **Change Shape** and look for and select the **MySQL.HeatWave.VM.Standard** shape.

9. Leave **Data Storage Size** as it is.

10. On Configure Backups, disable **'Enable Automatic Backup'**

    ![databases restore](./images/restore-edit-backup-plan.png "restore edit backup plan") 

11. Click on **Show Advanced Options** and go to the **Connections tab**, assign **NEWDB** as the new hostname. 

    Then click **Restore**
    ![databases restore](./images/restore-backup-create.png "restore from backup create")

    **Note**: It may take a few minures for the DB system to be created. When the DB System satate changes to Active, the DB System is ready to use.

## Task 5: Delete a Backup

1. Click **Navigation Menu**

    ![OCI Console Home Page](./images/homepage.png "home page")

2. Click  **Databases**, then **Backups**  
    ![menu databases](./images/menu-databases-backups.png "menu dbsystems backups")

    Make sure you are using the root compartment
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. Click the **Actions** button next to the Manual Backup you created previously, and select **Delete** from the drop-down menu
    ![delete backup](./images/delete-backup.png "click delete backup")

4. A pop-up window will appear asking you to confirm that you want to delete the backup, click **Delete Backup**
    ![delete backup](./images/confirm-delete-backup.png "confirm delete backup")

5. When the backup is deleted, its state will change to **Deleted** and it cannot be restored. 
    ![delete backup](./images/delete-backup-completed.png "delete backup completed")

    > **Note**: 
    - It may take a few minutes for the backup to be deleted.
    - Disable PITR (as it’s not compatible with Lakehouse) or disable backups completely to avoid issues later.
 
You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Selena Sanchez, MySQL Solution Engineering 
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - Selena Sanchez, MySQL Solution Engineering, March 2024