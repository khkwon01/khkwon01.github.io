# MySQL Heatwave 백업


## 세션 소개

이 Lab에서는 MySQL Heatwave DB 시스템에서 백업을 관리하는 방법을 학습합니다.

_Estimated Time:_ 15 minutes 소요


### 목표

이 Lab에서는 다음 작업을 안내해 드립니다.

- Manual Backup 생성
- DB System 백업 Plan 수정
- Manual Backup를 사용하여 new DB System으로 데이터 복구
- Point-in-Time를 사용하여 new DB System으로 데이터 복구
- 사용하지 않는 MySQL Backups 삭제

### Prerequisites (필요사항)

- An Oracle Trial or Paid Cloud Account

## 작업 1: Manual Backup 생성

1. **Navigation Menu** 클릭

    ![OCI Console Home Page](./images/homepage.png "home page")

2. **Databases** 클릭, **DB Systems** 클릭  
    ![menu databases](./images/menu-dbsystems.png "menu databases dbsystems")

    root compartment를 선택했는지 확인
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. deatils한 정보를 보기 위해 **HEATWAVE-DB** 클릭합니다.  
    ![databases list](./images/list-dbsystem.png "list of dbsystem")

4. **More Actions** menu 에서, **Create Manual Backup** 선택합니다.
    ![databases click backup](./images/click-manual-backup.png "select create manual databases")

5. 요청된 정보를 입력한 후 **Create Manual Backup**를 클릭하세요.
    * Display Name: Manual Backup
    * description를 그대로 두세요
    * Backup Type: Full Backup
    * 보존기간(Retention Period)을 그대로 두세요

    ![databases backup create](./images/create-manual-backup.png "create manual backup")

    **참고**: 백업이 완료되는 데 몇 분이 걸릴 수 있습니다.

6. **Navigation Menu** 클릭, **Databases** 클릭, **Backups** 클릭  
    ![menu databases](./images/menu-databases-backups.png "menu dbsystems backups")

    수동 백업이 성공적으로 생성되었는지 확인하세요
    ![databases backup create](./images/create-manual-backup-complete.png "create manual backup complete")



## 작업 2: DB System 백업 Plan 수정

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


## 작업 3: Manual Backup를 사용하여 new DB System으로 데이터 복구

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


## 작업 4: Point-in-Time를 사용하여 new DB System으로 데이터 복구

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

## 작업 5: 사용하지 않는 MySQL Backups 삭제

1. **Navigation Menu** 클릭

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
- **Last Updated By/Date** - kihyuk, MySQL Solution Engineering, July 2024
