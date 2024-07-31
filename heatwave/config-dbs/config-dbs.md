# Configure MySQL HeatWave DB System


## Introduction

In this lab, you will learn to manage configurations in a MySQL DB System.

_Estimated Time:_ 15 minutes


### Objectives

In this lab, you will be guided through the following tasks:

- Create a MySQL Configuration 
- Copy a MySQL Configuration, change variables and compare them
- Update the MySQL Configuration of a DB system
- Delete unused MySQL Confiigurations

### Prerequisites

- An Oracle Trial or Paid Cloud Account

## Task 1: Create a MySQL Configuration

1. Click **Navigation Menu**

    ![OCI Console Home Page](./images/homepage.png "home page")

2. Click  **Databases**, then **Configurations**  
    ![menu databases](./images/menu-databases-configurations.png "menu databases configurations")

    Make sure you are using the root compartment
    ![use root compartment](./images/select-compartment.png "use root comparment")

3. Select the Click **Create Configuration**
    ![create configuration](./images/create-configuration-list.png " click create configuration")

    Enter a name for your configuration: 

    ```bash
    <copy>MyConfig</copy>
    ```
  
    ![create configuration](./images/create-configuration-name.png "configuration compartment")

    
4. Click the **Change Shape** button 
    ![create configuration](./images/create-configuration-shape-change.png "change configuration shape")
    
5. Select the **OCPU** tab and look for and select the **MySQL.HeatWave.VM.Standard** shape. Then click **Select Shape**
    ![create configuration](./images/create-configuration-shape-select.png "select configuration shape")

6. Scroll down, the Variables Information page is displayed. In the **User Variables (Read/Write)** sectiion add the following variables and values:

    * Set **max_connections** to 200
    * Set **sort\_buffer\_size** to 500000
    * Set **time\_zone** to +01:00

    ![create configuration](./images/create-configuration-add-variables.png "configuration add variables")

    **Note:** You can click the **+Another Variable** to add more rows for configuring more variables

7. Click **Create** to create the configuration. The configuration Details page is displayed. 
    ![configuration details](./images/configuration-details.png "new configuration details")

8. Scroll down to see the variables that you have configured
    ![configuration variable details](./images/configuration-variables.png "new configuration variables details")



## Task 2: Copy a MySQL Configuration

1. On the MyConfig Details page, click **Copy Configuration** to make copy of the MyConfig configuration. 
    ![configuration details](./images/configuration-copy.png "click copy configuration")

2. The configuration copy page is displayed, enter a name for the configuration:

    ```bash
    <copy>MyConfig2</copy>
    ```

    ![copy configuration](./images/copy-configuration-name.png " copy configuration name")

3. Scroll Down and click the **Initialization Variiables** tab, and enable the **Ignore case in table and schema names** option

    ![copy configuration](./images/copy-configuration-change-initialization.png "copy configuration add initiialization variable")

4. Click **Create** to create the MyConfig2 configuration

5. Go back to the configurations list page
    ![configuration list](./images/list-configuration.png "list of configurations")

6. Click the context menu of MyConfig and click **Copy Configuration**
    ![copy configuration](./images/copy-configuration-from-dropdown.png "copy configuration dropdown menu")

7. The configuration copy page is displayed, enter a name for the configuration:

    ```bash
    <copy>MyConfig3</copy>
    ```
    ![copy configuration](./images/copy3-configuration-name.png "copy configuration name")

8. Scroll down to the **User variables (read/write)** tab and perform the following changes:
    * Change the value of **max_connections** to 300
    * Change the value **time_zone** to +02:00. 
    * Click **+Another Variable** to add another row.

    ![copy configuration](./images/copy-configuration-change-variables.png "copy configuration change variables")

    *  Add the **autocomit** variable and set its value to **OFF** 

    ![copy configuration](./images/copy-configuration-add-variable.png "copy configuration add variable")

9. Click **Create** to create MyConfig3 



## Task 3: Comparing two MySQL Configuration

1. Go back to the configurations list page 
    ![configuration list](./images/list-configuration3.png "list of confiigurations")
    
2. Select the **MyConfig2** and **MyConfig 3** confiigurations from the configurations list by selecting the check boxes. 
    Then click the **Actions** button and select **Compare** from the drop-down menu

    ![compare confgurations](./images/compare-configurations.png "click compare configurations")

3. The Compare configurations dialog box is shown. It shows the differences by **default**. 

    ![compare confgurations](./images/compare-configurations-default.png "compare confgurations default")

    * If you want to view all information of both configurations, click the **Show all** configuration Information button. 
    
    ![compare confgurations](./images/compare-configurations-show-all.png "compare confgurations all")

4. Click **Close**. 

## Task 4: Update the Configuration of a DB System

1. Click **Navigation Menu**, click  **Databases**, then **DB Systems**  
    ![menu databases](./images/menu-dbsystems.png "menu databases dbsystem")

2. Click on **EATWAVE-DB** to view the deatils.  
    ![databases list](./images/list-dbsystem.png "list of dbsystem")

3. Click the **Edit** button to edit the DB System
    ![edit database](./images/edit-dbsystem.png "click edit database")

4. The edit DB system page is shown. Scroll down to the Configuration section, click the **Change Configuration** button to choose a different configuration.
    ![edit database](./images/dbsystem-change-configuration.png "change database configuration")

5. The browse configuration dialog is displayed. Note that it only lists all configurations **that match the shape of the DB System**
    
    Click the Custom button to hide the default configurations 

    ![edit database](./images/dbsystem-change-configuration-custom.png "edit database cnfiguration custom tab")

6. Select **MyConfig2** configuration. 
    * An error message is displayed, this is because the initilization variable cannot be changed once the DB System has been deployed. 

    ![edit database](./images/dbsystem-change-configuration-error.png "edit database error")
    
7. Select the **MyConfig3** configuration and click **Select a Configuration**. 
    ![edit database](./images/dbsystem-change-configuration-final.png "change database configuration")

8. Click **Save Changes** in the Edit DB System page. HEATWAVE-DB changes to an updating state, after changing the configuration, the database needs to be restarted for the changes to take effect. 
    ![edit database](./images/dbsystem-change-configuration-save-changes.png "edit database save changes")

9. After it has restared, the database will change to **ACTIVE** state and the configuration shows MyConfig3. 
    ![database details](./images/dbsystem-active.png "active database")


## Task 5: Delete MySQL Configuration

1. Click **Navigation Menu**, then **Configurations**  
    ![configuration list](./images/menu-databases-configurations.png "list of confiigurations")

    Make sure you are in the root compartment
    ![Select Root compartment](./images/select-compartment.png "use root comparment")

3. Select the **MyConfig3, MyConfig2 and MyConfig** configurations by selecting the respective check boxes, click the actions button and select the **Delete** from the drop down menu
    ![delete configuration](./images/delete-configurations.png "click delete configuration")

4. Click **Delete configurations** too confirm
    ![delete configuration](./images/delete-configurations-confirm.png "delete configuration")

5. An error occurs and the deletion of the MyConfig3 configuration fails. Click **Show Details** to view the reason. 

    ![delete configuration](./images/delete-configurations-error.png "delete configuration error")
    
    As shown on the details, the MyConfig3 configuration cannot be deleted because it is currently being used by a DB system.
    Click close on the details page. 

6. On the configuration list page, you will notice that MyConfig2 and MyConfig configurations have been deleted.
    ![configuration list](./images/list-configurations.png "list of configurations")


You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Selena Sanchez, MySQL Solution Engineering 
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Perside Foster, MySQL Principal Solution Engineering
- **Last Updated By/Date** - Selena Sanchez, MySQL Solution Engineering, March 2024