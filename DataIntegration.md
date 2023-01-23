# Data Integration Exercise (Mandatory)

## Table of contents

- [Data Integration Exercise (Mandatory)](#data-integration-exercise-mandatory)
  - [Table of contents](#table-of-contents)
  - [Exercise](#exercise)

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