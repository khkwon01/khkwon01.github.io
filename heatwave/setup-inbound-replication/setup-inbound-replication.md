# Setup MySQL HeatWave Inbound Replication

![mysql heatwave](./images/mysql-heatwave-logo.jpg "mysql heatwave")

## Introduction

Inbound replication uses a replication channel configured in MySQL HeatWave Service to copy transactions from another location to a DB system. The channel connects the source (a MySQL instance or another DB system) to the replica (a DB system), and copies data from the source to the replica.

For more details see OCI Document:
[MySQL HeatWave Inbound Replication](https://docs.oracle.com/en-us/iaas/mysql-database/doc/inbound-replication.html).

_Estimated Time:_ 20 minutes

### Objectives

In this lab, you will be guided through the following task:

- Create a Replication Channel
- Enable or Disable a Channel
- Resume a Channel
- Reset a Channel
- Edit a Channel

### Prerequisites

- An Oracle Trial or Paid Cloud Account
- Some Experience with MySQL Shell


## Task 1: Create a Read Replica

For inbound replication, a replication channel connects the source (a MySQL instance or another DB system) to the replica (a DB system), and copies data from the source to the replica.

Use the Console to create a replication channel.

Go to the link below and follow the **Creating a Replication Channel Using the Console** Instructions:

[Creating a Replication Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/creating-replication-channel.html#GUID-3C42FF94-3DEE-409C-B8A3-467890AA7FE3)

## Task 2: Enable or Disable a Channel

Enabling a replication channel that is in the Inactive state starts replication from the source if there are no errors. Disabling a replication channel stops replication and puts the channel into the Inactive state.

Use the Console to enable or disable  a replication channel.

Go to the link below and follow the **Enabling or Disabling a Channel** Instructions:

[Enabling or Disabling a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## Task 3: Resume a Channel

When an inbound replication channel is in the Needs Attention state, fix the error then resume the channel to restart replication. The Details column on the Channels page explains why a replication channel needs attention.

The Needs Attention state may also be displayed because the DB system is in INACTIVE state. In that case, replication cannot restart until the DB system is active.

Use the Console to Resume a replication channel.

Go to the link below and follow the **Resuming a Channel** Instructions:

[Resuming a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## Task 4: Reset a Channel

Resetting an inbound replication channel removes all data on the channel, except the channel configuration. It is equivalent to RESET REPLICA ALL FOR CHANNEL. When there is an unrecoverable issue, the reset operation clears the records associated with replication so that the channel can have a clean start.

The target DB system drops its position in the source binary log, clears the replication metadata repositories, deletes the relay log files, and starts a new relay log file.

Use the Console to Reset a replication channel.

Go to the link below and follow the **Resuming a Channel** Instructions:

[Resuming a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)

## Task 5: Edit a Channel

Edit an inbound replication channel if you need to change configuration items such as the channel name, description, or source connection details after you create it.

Use the Console to Edit a replication channel.

Go to the link below and follow the **Editing a Channel** Instructions:

[Editing a Channel](https://docs.oracle.com/en-us/iaas/mysql-database/doc/managing-replication-channel.html#GUID-4CD38EFA-7463-4175-8838-0EE40C0FABC9)


You may now **proceed to the next lab**

## Acknowledgements

- **Author** - Perside Foster, MySQL Principal Solution Engineering
- **Contributors** - Mandy Pang, MySQL Principal Product Manager,  Nick Mader, MySQL Global Channel Enablement & Strategy Manager, Selena Sanchez, MySQL Solution Engineering
- **Last Updated By/Date** - Perside Foster, MySQL Solution Engineering, March 2024