# Migrate Data Into MySQL HeatWave

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## Introduction

Use the export and import methods to transfer data from a MySQL instance to MySQL HeatWave Service.

For more details see OCI Document:
- [MySQL HeatWave Exporting and Importing](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/exporting-and-importing.html).

- https://plforacle.github.io/mysql-mgrate-apex/workshops/freetier/index.html


_Estimated Time:_ 20 minutes

### Objectives

In this lab, you will be guided through the following task:

- Create a DB system with data import
- Import data into a DB system
- Export data from MySQL servers and DB systems
- Migrate data with replication

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell


## Task 1: Create a DB system with data import

Use the data import feature to import data from an Object Storage bucket to a standalone DB system.

You can import to a standalone DB system in the same region as the Object Storage bucket only. Also, you can import a dump while it is still being exported to an Object Storage bucket.

To import data to a high availability DB system, first import data to a standalone DB system and then enable high availability.

Go to the link below and follow the **Importing Using the Data Import Feature** Instructions:

[Importing Using the Data Import Feature](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/importing-using-data-import-feature.html)

## Task 2: Import data into a DB system

Use MySQL Shell in the Oracle Cloud Infrastructure compute instance to import data to a MySQL HeatWave Service DB system.

Go to the link below and follow the **Importing Using MySQL Shell** Instructions:

[Importing Using MySQL Shell](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/importing-using-mysql-shell.html)

## Task 3: Export data from MySQL servers and DB systems

Export a MySQL instance to an Object Storage bucket using dump utilities of MySQL Shell. You can then use the data import feature to import data from the Object Storage bucket to a DB system present in the same region.

Go to the link below and follow the **Importing Using the Data Import Feature** Instructions:

[Exporting a MySQL Instance](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/exporting-mysql-instance.html)

## Task 4: Migrate data with replication

Use the Console and MySQL Shell to migrate a MySQL instance to MySQL HeatWave Service. The MySQL instance can be running on-premises, in other cloud vendors as managed or unmanaged services, or a MySQL HeatWave Service instance.

Go to the link below and follow the **Migrating a MySQL Instance to MySQL HeatWave Service** Instructions:

[Migrating a MySQL Instance to MySQL HeatWave Service](https://docs.public.oneportal.content.oci.oraclecloud.com/en-us/iaas/mysql-database/doc/migrating-mysql-instance-mysql-heatwave-service.html)



You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, March 2024