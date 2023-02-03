# Spatial (optional)

## Table of contents 

- [Spatial (optional)](#spatial-optional)
  - [Table of contents](#table-of-contents)
  - [Load a map with German federal states](#load-a-map-with-german-federal-states)
  - [Viewing the State map](#viewing-the-state-map)
  - [Viewing customers on the map](#viewing-customers-on-the-map)
  - [Inserting and filling a new Table](#inserting-and-filling-a-new-table)
  - [Viewing all customers on the map](#viewing-all-customers-on-the-map)
  - [Separating customers addresses to a specific area](#separating-customers-addresses-to-a-specific-area)
  - [Cluster the customer address](#cluster-the-customer-address)
  - [Evaluation of the results](#evaluation-of-the-results)


## Load a map with German federal states

> In this section, a world map with countries as a table is loaded into the SAP HANA Cloud Database in the form of a shapefile stored locally on the computer.

1. Right-Click on Catalog and Click Import Catalog Objects. 
2. Click on Browse…, select World_Countries.tar.gz in your Windows Explorer and click on Import

## Viewing the State map

> In this section, we want to take a look at the country borders of Germany that we uploaded in the previous step using the “World_Countries” table.

1. Left-Click on Tables and World_Countries
2. Click on Open Data
3. Scroll down to Germany and double-click on the SHAPE entry
4. The map will appear:

## Viewing customers on the map

> In this section, we want to display all customers. To do this, we will execute a database query and consider the points individually.

1. Click on the SQL-console-icon:
2. Type:
```sql
SELECT *
FROM COMPANY_DEMO.CUSTOMERS;
```
3. As you can see, the addresses already exist in the table as latitude and longitude. These must be processed further to ST_POINT’s. To do this, you must execute the following SQL command with the start-button in the upper left corner:
```sql
SELECT CUSTOMER_ID, NEW ST_POINT(TO_DOUBLE(CUSTOMER_LONGITUDE), 
TO_DOUBLE (CUSTOMER_LATITUDE), 1000004326) AS Location
FROM COMPANY_DEMO.CUSTOMERS;
```
4. Double-click on a LOCATION entry. As a result, the map showing the customer location:

## Inserting and filling a new Table

> In this section, you create a new table. This should receive the created points of longitude and latitude and the customer IDs. The other information about the customer is not required.

1. Execute the following SQL command to create a new table:
```sql
CREATE TABLE COMPANY_DEMO.CUSTOMER_LOCATION
(
	CUSTOMER_ID NVARCHAR(11) not null primary key,
	CUSTOMER_LOCATION ST_Point(1000004326)
);
```

2. Execute the following SQL command to insert the values in the new table:
```sql
INSERT INTO COMPANY_DEMO.CUSTOMER_LOCATION (CUSTOMER_ID, 
CUSTOMER_LOCATION)
SELECT CUSTOMER_ID, NEW ST_POINT(TO_DOUBLE(CUSTOMER_LONGITUDE), 
TO_DOUBLE (CUSTOMER_LATITUDE), 1000004326)
FROM COMPANY_DEMO.CUSTOMERS;
```

## Viewing all customers on the map

> In this section, we will look at all customers locations as collection.

1. To display all customers locations. All points must be combined to a collection. Execute following command for this and double-click on the result:
```sql
SELECT ST_CollectAggr(Kunde.CUSTOMER_LOCATION) 
FROM COMPANY_DEMO.CUSTOMER_LOCATION AS Kunde;
```

## Separating customers addresses to a specific area

> For our use case, we only need the customers in Germany. Using the polygon from World_Countries, we can check which points are within these borders. To simplify further processing, we store these customers in a second table.

1. Execute the following command to get only the points that are in Germany:

```sql
SELECT Kunde.CUSTOMER_LOCATION, 
"SHAPE".ST_Contains(Kunde.CUSTOMER_LOCATION) AS "In Deutschland"
FROM COMPANY_DEMO.CUSTOMER_LOCATION AS Kunde, 
"COMPANY_DEMO"."World_Countries" 
WHERE "COUNTRY" = 'Germany' 
AND "SHAPE".ST_Contains(Kunde.CUSTOMER_LOCATION)=1;
```

2. Execute the following command to create a table for customers in Germany:
```sql
CREATE TABLE COMPANY_DEMO.CUSTOMER_LOCATION_Germany
(
	CUSTOMER_ID NVARCHAR(11) not null primary key,
	CUSTOMER_LOCATION ST_Point(1000004326)
);
```

3. Execute the following command to insert the customers in Germany:
```sql
INSERT INTO COMPANY_DEMO.CUSTOMER_LOCATION_Germany
 (CUSTOMER_ID, CUSTOMER_LOCATION)
SELECT Kunde.CUSTOMER_ID, Kunde.CUSTOMER_LOCATION
FROM COMPANY_DEMO.CUSTOMER_LOCATION AS Kunde, 
"COMPANY_DEMO"."World_Countries" 
WHERE "COUNTRY" = 'Germany' 
AND "SHAPE".ST_Contains(Kunde.CUSTOMER_LOCATION)=1;
```

4. Execute the following command to receive all customers in Germany as a collection and double-click on the result:
```sql
SELECT ST_CollectAggr(Kunde.CUSTOMER_LOCATION) 
FROM COMPANY_DEMO.CUSTOMER_LOCATION_Germany AS Kunde;
```

5. Execute the following command to receive all customers in Germany as a collection bordered by the German border and double-click on the result:
```sql
SELECT "SHAPE".ST_Collect(ST_CollectAggr(Kunde.CUSTOMER_LOCATION))
FROM COMPANY_DEMO.CUSTOMER_LOCATION_Germany AS Kunde, "COMPANY_DEMO"."World_Countries"
WHERE "COUNTRY" = 'Germany';
```

## Cluster the customer address

> In this section, we are clustering all customers locations in Germany.

1. To cluster, you must execute the following SQL command:
```sql
SELECT ST_ClusterID() as ID, ST_ClusterCell() as SHAPE, 
ST_ClusterCell().ST_PointOnSurface().ST_AsText() as Point, COUNT(*) AS 
COUNT
FROM COMPANY_DEMO.CUSTOMER_LOCATION_Germany
GROUP CLUSTER BY "CUSTOMER_LOCATION"
USING HEXAGON X CELLS 20
ORDER BY COUNT DESC;
```

## Evaluation of the results

> In this section, we will look at the cluster result from different views.

1. Let's look at the largest hexagon with 200 entries by double-clicking the SHAPE entry. We can see that Frankfurt has the closeness customer density:
2. It’s interesting to know where all locations are in the Hexagon. You can do this by executing the following commands and double-click on the result:
```sql
SELECT 
ST_CollectAggr(Kunde.CUSTOMER_LOCATION).ST_Collect(ST_ClusterCell())
FROM COMPANY_DEMO.CUSTOMER_LOCATION_Germany AS Kunde
GROUP CLUSTER BY "CUSTOMER_LOCATION"
USING HEXAGON X CELLS 20
HAVING COUNT(*) = 200;
```
3. What is the general distribution of the hexagons over Germany? Execute the following command:
```sql
WITH clustered_data AS (
	SELECT ST_ClusterCell() as SHAPE
	FROM COMPANY_DEMO.CUSTOMER_LOCATION_Germany 
	GROUP CLUSTER BY "CUSTOMER_LOCATION"
	USING HEXAGON X CELLS 20
	ORDER BY COUNT(*) DESC
)	
SELECT ST_CollectAggr(SHAPE)
FROM clustered_data;
```


< [Back to Overview](README.md)