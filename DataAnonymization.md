# Data Anonymization (optional)

## Table of contents 

- [Data Anonymization (optional)](#data-anonymization-optional)
  - [Table of contents](#table-of-contents)
  - [Open Database Explorer Tables-\>Employees](#open-database-explorer-tables-employees)
  - [Genereate Select Statement](#genereate-select-statement)
  - [Create anonymiaztion view](#create-anonymiaztion-view)
  - [Preview the anonymized data](#preview-the-anonymized-data)
  - [Optimize the anonymization and gain more Insights](#optimize-the-anonymization-and-gain-more-insights)
  - [Differential Privacy](#differential-privacy)


## Open Database Explorer Tables->Employees

## Genereate Select Statement

To understand the need for anonymization, run the SQL query on the sample data as given below:

```sql
SELECT "start_year", "gender", "zipcode", "salary", count(*) as "Count" FROM "ANON_SAMPLE"
GROUP BY "start_year", "gender", "zipcode", "salary" ORDER by "Count" ASC;
```
As shown by the outcome, there are numerous distinct combinations of quasi-identifiers, indicated by a Count value of 1, that can result in the revelation of sensitive information, such as salary amounts, of those involved. Therefore, data anonymization is necessary in order to share this sample data securely, without endangering data privacy.

## Create anonymiaztion view

> Next, to meet the above requirement, you will create an anonymization view using the sample data..The objective of this exercise is to anonymize the salary data with SAP HANA's integrated K-Anonymity Algorithm. Afterwards you will preview the anonymized salary data and gain some insights.

1. Create a new View. As artifact type, choose SQL View (hdbview) and as artifact name, write SALARYANON. Then click on Create.
2. Paste the code into the created file to create an anonymized view using K-ANONYMITY:
    ```sql
    VIEW "SALARYANON" ("id", "start_year", "gender", "zipcode", "salary")
    AS SELECT "id", "start_year", "gender", "zipcode", "salary" FROM "ANON_SAMPLE"
    WITH ANONYMIZATION (ALGORITHM 'K-ANONYMITY' PARAMETERS '{"k": 8}'
    COLUMN "id" PARAMETERS '{"is_sequence":true}'
    COLUMN "gender" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"embedded":[["f"],["m"]]}}'
    COLUMN "zipcode" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"embedded":[["5004","50xx"],["5005","50xx"],["5006","50xx"],["5104","51xx"],["5105","51xx"],["5106","51xx"],["5204","52xx"],["5205","52xx"],["5206","52xx"],["6006","60xx"],["6007","60xx"],["6008","60xx"],["6106","61xx"],["6107","61xx"],["6108","61xx"],["6206","62xx"],["6207","62xx"],["6208","62xx"],["7002","70xx"],["7003","70xx"],["7004","70xx"],["7102","71xx"],["7103","71xx"],["7104","71xx"],["7202","72xx"],["7203","72xx"],["7204","72xx"]]}}'
    COLUMN "start_year" PARAMETERS '{"is_quasi_identifier":true,"hierarchy":{"embedded":[["1987","1986-1990","1986-1995"],["1988","1986-1990","1986-1995"],["1989","1986-1990","1986-1995"],["1990","1986-1990","1986-1995"],["1991","1991-1995","1986-1995"],["1992","1991-1995","1986-1995"],["1993","1991-1995","1986-1995"],["1994","1991-1995","1986-1995"],["1995","1991-1995","1986-1995"],["1996","1996-2000","1996-2005"],["1997","1996-2000","1996-2005"],["1998","1996-2000","1996-2005"],["1999","1996-2000","1996-2005"],["2000","1996-2000","1996-2005"],["2001","2001-2005","1996-2005"],["2002","2001-2005","1996-2005"],["2003","2001-2005","1996-2005"],["2004","2001-2005","1996-2005"],["2005","2001-2005","1996-2005"],["2006","2006-2010",">2006"],["2007","2006-2010",">2006"],["2008","2006-2010",">2006"],["2009","2006-2010",">2006"],["2010","2006-2010",">2006"],["2011","2011-2015",">2006"],["2012","2011-2015",">2006"],["2013","2011-2015",">2006"],["2014","2011-2015",">2006"],["2015","2011-2015",">2006"],["2016","2016-2020",">2006"],["2017","2016-2020",">2006"]]}}');
    ```
3. The code contains three quasi-identifying columns. These are start year, zip code, gender and of course salary as sensitive data.
It should look like this:
4. By executing the provided code snippet, you anonymize the View of your salary data using the integrated k-anonymity algorithm in HANA Cloud. K in the context defines the smallest possible group with the same quasi-identifiers. 
If an attribute is a quasi-identifier, it will be anonymized using the predefined hierarchies or functions.

## Preview the anonymized data

1. Switch to the Database Explorer and open your HDI Container. Select Views in the catalog, click on SALARYANON and open the SQL Console.  
2. Type the following statement to query the new anonymized view :

```sql
REFRESH VIEW "SALARYANON" ANONYMIZATION;
SELECT * FROM SALARYANON;
```

Refreshing your View is important, so that the new changes are visible.
Click on the green Play button to execute both commands.

3. The start year column has been anonymized by the k-anonymity algorithm, while the remaining columns remain unchanged.

## Optimize the anonymization and gain more Insights

1. To improve the anonymity, we can determine the number of individuals that cannot be differentiated and count the number of distinct combinations by executing the following statement:
   ```sql
   REFRESH VIEW "SALARYANON" ANONYMIZATION;
    SELECT "start_year", "gender", "zipcode", count(*) AS "Count", MAX("salary") FROM "SALARYANON" GROUP BY "start_year", "gender", "zipcode" ORDER BY "Count" ASC;
   ```

As evidenced, the anonymization process has been successful as there are significantly more individuals in each group than the specified K value of 8. This indicates that additional quasi-identifiers could have been included in the anonymized view while still maintaining accurate results with a high level of privacy.

## Differential Privacy

< [Back to Overview](README.md)


