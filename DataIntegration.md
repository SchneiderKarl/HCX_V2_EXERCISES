# Data Integration Exercise (Mandatory)

## Table of contents

- [Data Integration Exercise (Mandatory)](#data-integration-exercise-mandatory)
  - [Table of contents](#table-of-contents)
  - [Create Virtual Table (or Strg+Shift+P)](#create-virtual-table-or-strgshiftp)
  - [Deploy to SAP HANA Cloud runtime](#deploy-to-sap-hana-cloud-runtime)
  - [Open HDI Container in SAP HANA Database Explorer](#open-hdi-container-in-sap-hana-database-explorer)
  - [Add shared Replica?](#add-shared-replica)
  - [Back in BAS Create Replication Task](#back-in-bas-create-replication-task)
  - [Deploy](#deploy)
  - [DBX](#dbx)
  - [Add realtime Replication use Table with Virtual Table from before](#add-realtime-replication-use-table-with-virtual-table-from-before)
  - [Exercise](#exercise)

## Create Virtual Table (or Strg+Shift+P)

1) 1) Click on **View** in the Menu Bar
   2) Then click on **Command Palette...**


2) Type in `SAP HANA: Create HANA Database Artifact`

3) Create SAP HANA Database Artifact wizard:
   1) **Path**: `/home/user/porjects/HCX_V2/db/src/DataIntegration`
   2) **Namespace**: leave it `hcx.db.DataIntegration`
   3) **Database Version**: `HANA Cloud`
   4) **Artifact type**: `Virtual Table (hdbvirtualtable)`
   5) **Name**: `VT_XXXXX`
4) Right-click on the created file and select **Open With...** and change the default editor to **Virtual Table Editor**.
5) Virtual Table Editor wizard:
   1) **Virtual table name**: `` leave it
   2) **Remoute source name**: ``
   3) **Database name**: ``
   4) **Schema name**: ``
   5) **Object name**: ``

## Deploy to SAP HANA Cloud runtime

## Open HDI Container in SAP HANA Database Explorer

## Add shared Replica?

## Back in BAS Create Replication Task

## Deploy

## DBX

## Add realtime Replication use Table with Virtual Table from before








## Exercise
- Virtual Table with Virtual Table Editor, switch on to default
- open DBX Access Data
- Access Time, Insert etc, dann wieder Delete (or Read-Only)
- Federation (Virtualization) vs Replication
- Create Replication Table
- Initial (Batch) Load
- Time (Load/Unload)
- Inital+Realtime+Structure
- Insert into their Virtual Table and select of entry
- Replicate Data with Replica (Remote Table Replication RTR) vs Fabric Virtual Table (Replica)
- Replication Task vs Flowgraph

Look at Barmer Script


- First Remote Source SAP HANA, onPrem, HANA Service or HANA Cloud
- Second Source S4/HANA (Cloud) System
- Third Amazon Athena or Google BigQuery, or MS ? or Oracle 
- Fourth (SAP HANA Data Lake RE, DL Files)
- Fifth (Object Storage S3 Bucket, Azure Blob, Google Cloud Storage)


1. Tabelle SAP HANA Service/Cloud
   - Orders
     - ID
     - Date
     - Time
     - Quantity
     - Price
     - Product
     - Status

2. Tabelle S4/HANA (Cloud)
   - Products
     - ID
     - Name
     - ...
3. Customers with Address or Spatial Columns  
4. Employees with Salary
      - k-Anon
      - Differential Privacy