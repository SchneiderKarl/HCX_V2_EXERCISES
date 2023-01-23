# Data Tiering (optional)

## Table of contents 

- [Data Tiering (optional)](#data-tiering-optional)
  - [Table of contents](#table-of-contents)
  - [Exercise](#exercise)

## Exercise
- Use table created in Data Integration (with Date compoenent, eg Transaction Date and Status closed,open,new,in Progress)
- DBX
- First Partition the table with Dynamic Aging and filter if Status closed
  - This year+all not closed Hot
  - Last 2-3 year+closed Warm
  - Last 4-10 year+closed in RDL
  - older than 10 years+closed in DLF
  - check open metadata/data
- CALL SYSHDL_HCX.REMOTE_EXECUTE(CREATE Table like)
- insert/delete from HC Table CALL REMOTEEXECUTE
- Virtual Table in .hdbvirtualtable
  - Scheduled job to export to data lake 
- insert into virtual table with newer date to create new partition
- Create View that is combining all if needed with Table for input of the years so not all is fetched (maybe in default from Data Integration which gets updated if needed)
- 

[hello](link|bas) hello [bas]

{link|bas}

{links|bas}: hello

[links|bas]:hello

[bas]:basLink

> Q4 planned integration of HDI and Data Lake