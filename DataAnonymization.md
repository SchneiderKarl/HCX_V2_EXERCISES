# Data Anonymization (optional)

## Table of contents 

- [Data Anonymization (optional)](#data-anonymization-optional)
  - [Table of contents](#table-of-contents)
  - [Understand the need for anonymization](#understand-the-need-for-anonymization)
  - [Create anonymiaztion view](#create-anonymiaztion-view)
  - [Preview the anonymized data](#preview-the-anonymized-data)
  - [Use the anonymized view to gain insights](#use-the-anonymized-view-to-gain-insights)
  - [Differential Privacy](#differential-privacy)


## Understand the need for anonymization

1. Start in the Database Explorer and paste the following code into it and run it

```sql
SELECT * FROM "hcx.db.DataIntegration::RT_EMPLOYEES";
```

![img](Images/Image_DataAnonymization__16.png)

2. Leave out direct identifier. Paste the following code into it and run it

```sql
SELECT "EMPLOYEE_SALARY", "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_REGION", "EMPLOYEE_ZIPCODE", "EMPLOYEE_T-LEVEL", "EMPLOYEE_EDUCATION" FROM "hcx.db.DataIntegration::RT_EMPLOYEES";
```

![img](Images/Image_DataAnonymization__17.png)

3. sd

```sql
SELECT *
FROM "hcx.db.DataIntegration::RT_EMPLOYEES"
WHERE EMPLOYEE_START_YEAR = 2008
	AND EMPLOYEE_GENDER = 'm'
	AND EMPLOYEE_REGION = 'APJ'
	AND EMPLOYEE_ZIPCODE = 7004
	AND "EMPLOYEE_T-LEVEL" = 'T4'
	AND EMPLOYEE_EDUCATION = 'Doctorate';
```

![img](Images/Image_DataAnonymization__18.png)

4. sd

```sql
SELECT 
"EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_REGION", "EMPLOYEE_ZIPCODE", "EMPLOYEE_T-LEVEL", "EMPLOYEE_EDUCATION", count(*)
FROM "hcx.db.DataIntegration::RT_EMPLOYEES"
GROUP BY "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_REGION", "EMPLOYEE_ZIPCODE", "EMPLOYEE_T-LEVEL", "EMPLOYEE_EDUCATION"
HAVING count(*)=1;
```

![img](Images/Image_DataAnonymization__19.png)

5. To understand the need for anonymization, run the SQL query on the sample data as given below:

```sql
SELECT "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_ZIPCODE", "EMPLOYEE_SALARY", count(*) as "Count" FROM "hcx.db.DataIntegration::RT_EMPLOYEES"
GROUP BY "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_ZIPCODE", "EMPLOYEE_SALARY" ORDER by "Count" ASC;
```



As shown by the outcome, there are numerous distinct combinations of quasi-identifiers, indicated by a Count value of 1, that can result in the revelation of sensitive information, such as salary amounts, of those involved. Therefore, data anonymization is necessary in order to share this sample data securely, without endangering data privacy.

## Create anonymiaztion view

> Next, to meet the above requirement, you will create an anonymization view using the sample data..The objective of this exercise is to anonymize the salary data with SAP HANA's integrated K-Anonymity Algorithm. Afterwards you will preview the anonymized salary data and gain some insights.

1) 1) Click on **View** in the Menu Bar
   2) Then click on **Command Palette...**

![img](Images/Image_DataIntegration__01.png)

2) Type in `SAP HANA: Create HANA Database Artifact` and select this option

![img](Images/Image_DataIntegration__02.png)

3) 1) Change the path to the **DataAnonymization*** folder, by clicking the folder icon
   2) Click on **..** to navigate to a higher level

![img](Images/Image_DataAnonymization__01.png)

4) Click on **DataAnonymization** and confirm with **OK**

![img](Images/Image_DataAnonymization__02.png)

5) Create SAP HANA Database Artifact wizard:
   1) **Path**: `/home/user/projects/HCX_V2/db/src/DataAnonymization`
   2) **Namespace**: `hcx.db.DataIntegration` (should be automatically filled)
   3) **Database Version**: `HANA Cloud`
   4) **Artifact type**: `SQL View (hdbview)`
   5) **Name**: `SALARYANON`
   6) Click **Create**

![img](Images/Image_DataAnonymization__03.png)

7. Paste the code into the created file to create an anonymized view using K-ANONYMITY:

```sql
VIEW "hcx.db.DataAnonymization::SALARYANON"
AS SELECT "EMPLOYEE_ID","EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_ZIPCODE", "EMPLOYEE_SALARY" FROM "hcx.db.DataIntegration::RT_EMPLOYEES"
WITH ANONYMIZATION (ALGORITHM 'K-ANONYMITY' PARAMETERS '{"k": 8}'
COLUMN "EMPLOYEE_ID" PARAMETERS '{"is_sequence":true}'
COLUMN "EMPLOYEE_GENDER" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"embedded":[["f"],["m"]]}}'
COLUMN "EMPLOYEE_ZIPCODE" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"function":"hcx.db.DataAnonymization::ZIP_CODE_HIERARCHY", "levels":4}}'
COLUMN "EMPLOYEE_START_YEAR" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"function":"hcx.db.DataAnonymization::START_YEAR_GROUP_HIERARCHY", "levels":3}}');
```

![img](Images/Image_DataAnonymization__04.png)

3. The code contains three quasi-identifying columns. These are start year, zip code, gender and of course salary as sensitive data.
It should look like this:



4. By deploying the provided code snippet, you anonymize the View of your salary data using the integrated k-anonymity algorithm in HANA Cloud. K in the context defines the smallest possible group with the same quasi-identifiers. 
If an attribute is a quasi-identifier, it will be anonymized using the predefined hierarchies or functions.

![img](Images/Image_DataAnonymization__05.png)

## Preview the anonymized data

1. Switch to the Database Explorer and open your HDI Container. Select Views in the catalog, click on SALARYANON and open the SQL Console.  
2. Type the following statement to query the new anonymized view :

```sql
REFRESH VIEW "hcx.db.DataAnonymization::SALARYANON" ANONYMIZATION;
SELECT *  FROM "hcx.db.DataAnonymization::SALARYANON";
```

Refreshing your View is important, so that the new changes are visible.
Click on the green Play button to execute both commands.

![img](Images/Image_DataAnonymization__06.png)

3. The zip code column has been anonymized by the k-anonymity algorithm, while the remaining columns remain unchanged.

## Use the anonymized view to gain insights

1. To improve the anonymity, we can determine the number of individuals that cannot be differentiated and count the number of distinct combinations by executing the following statement:

```sql
SELECT "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_ZIPCODE", count(*) as "Count", MAX("EMPLOYEE_SALARY") FROM "hcx.db.DataAnonymization::SALARYANON"
GROUP BY "EMPLOYEE_START_YEAR", "EMPLOYEE_GENDER", "EMPLOYEE_ZIPCODE" ORDER by "Count" ASC;
```

![img](Images/Image_DataAnonymization__07.png)

As evidenced, the anonymization process has been successful as there are significantly more individuals in each group than the specified K value of 8. This indicates that additional quasi-identifiers could have been included in the anonymized view while still maintaining accurate results with a high level of privacy.

Change k:8

![img](Images/Image_DataAnonymization__14.png)

![img](Images/Image_DataAnonymization__15.png)

Change Privilige?!



## Differential Privacy

1) 1) Click on **View** in the Menu Bar
   2) Then click on **Command Palette...**

![img](Images/Image_DataIntegration__01.png)

2) Type in `SAP HANA: Create HANA Database Artifact` and select this option

![img](Images/Image_DataIntegration__02.png)

3) Create SAP HANA Database Artifact wizard:
   1) **Path**: `/home/user/projects/HCX_V2/db/src/DataAnonymization`
   2) **Namespace**: `hcx.db.DataIntegration` (should be automatically filled)
   3) **Database Version**: `HANA Cloud`
   4) **Artifact type**: `SQL View (hdbview)`
   5) **Name**: `SALARYANON_DP`
   6) Click **Create**

![img](Images/Image_DataAnonymization__08.png)

4) Paste the code into the created file to create an anonymized view using Differential Privacy:

```sql
VIEW "hcx.db.DataAnonymization::SALARYANON_DP"
AS SELECT "EMPLOYEE_ID", "EMPLOYEE_START_YEAR", "EMPLOYEE_SALARY"
FROM "hcx.db.DataIntegration::RT_EMPLOYEES"
WITH ANONYMIZATION (ALGORITHM 'DIFFERENTIAL_PRIVACY' PARAMETERS ''
COLUMN "EMPLOYEE_ID" PARAMETERS '{"is_sequence":true}'
COLUMN "EMPLOYEE_SALARY" PARAMETERS '{"is_sensitive":true, "epsilon" : 0.5, "sensitivity": 100000}');
```

![img](Images/Image_DataAnonymization__09.png)

5) sd

```sql
REFRESH VIEW "hcx.db.DataAnonymization::SALARYANON_DP" ANONYMIZATION;
SELECT * FROM "hcx.db.DataAnonymization::SALARYANON_DP";
```

![img](Images/Image_DataAnonymization__10.png)


```sql
SELECT "EMPLOYEE_START_YEAR", AVG("EMPLOYEE_SALARY") FROM "hcx.db.DataAnonymization::SALARYANON_DP" GROUP BY "EMPLOYEE_START_YEAR"ORDER BY "EMPLOYEE_START_YEAR" ASC;
SELECT "EMPLOYEE_START_YEAR", AVG("EMPLOYEE_SALARY") FROM "hcx.db.DataIntegration::RT_EMPLOYEES" GROUP BY "EMPLOYEE_START_YEAR" ORDER BY "EMPLOYEE_START_YEAR" ASC;
```

![img](Images/Image_DataAnonymization__11.png)

![img](Images/Image_DataAnonymization__12.png)

![img](Images/Image_DataAnonymization__13.png)



< [Back to Overview](README.md)


