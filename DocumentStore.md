# Document Store (optional)

## Table of contents 

- [Document Store (optional)](#document-store-optional)
  - [Table of contents](#table-of-contents)
  - [Prereq folder](#prereq-folder)
  - [Exercise](#exercise)
  - [Create Collection](#create-collection)
  - [Rename preconfigured files](#rename-preconfigured-files)
  - [DBX: JSON Collections -\>](#dbx-json-collections--)
  - [Select \*, where "name" = 'Peter Peterson';, nested: "address"."city" = 'Melbourne';](#select--where-name--peter-peterson-nested-addresscity--melbourne)
  - [Insert new Item](#insert-new-item)
  - [Update, Delelete](#update-delelete)
  - [Aggregation](#aggregation)
  - [Nested einführen, select, update, agg](#nested-einführen-select-update-agg)
  - [Join with Relational Data for more information](#join-with-relational-data-for-more-information)
  - [Create View to persist with Relational Data](#create-view-to-persist-with-relational-data)


## Prereq folder
- .csv with linebreaks and json input data or Import data?

## Exercise

- Create Collection
- Create tabledata
- Open DBX
- Select * from (Json result)
- select * from where (Json result)
- select Projection and aggregation
- Insert entry
- Update same entry
- Delete same entry
- Combine with Relational data
- renaming columns
- schemaless and schema
- (Arrays)

## Create Collection
1. Strg Shift P **Create Database Object**
2. Path: `/home/user/projects/HCX_V2/db/src/DocumentStore`
Namespace: `hcx.db.DocumentStore`
Database version: `HANA Cloud`
Artifact type: `Document Store Collection (hdbcollection)`
Artifact name: `REVIEWS`

3. Should look like this:
```sql
COLLECTION "hcx.db.DocumentStore::REVIEWS"
```
4. Deploy

## Rename preconfigured files 

> oder nur hdbtabledata definieren
New File Name: REVIEWS

```json
{
    "format_version": 1,
    "imports": [
        {
            "column_mappings": {
                "hcx.db.DocumentStore::REVIEWS": 1
            },
            "is_collection_table": true,
            "source_data": {
                "data_type": "CSV",
                "dialect": "HANA-JSON",
                "file_name": "hcx.db.DocumentStore::REVIEWS.csv",
                "has_header": false
            },
            "target_table": "hcx.db.DocumentStore::REVIEWS"
        }
    ]
}
```

## DBX: JSON Collections -> 

Rigth-click Reviews -> Generate SELECT Statement and Run

## Select *, where "name" = 'Peter Peterson';, nested: "address"."city" = 'Melbourne';
Select specified columns, damit kein JSON String zurück gegeben wird.


## Insert new Item

```sql
INSERT INTO "hcx.db.DocumentStore::REVIEWS" VALUES ('{"reviewerID": "A1F6404F1VG29J"}')
```

## Update, Delelete

## Aggregation 

## Nested einführen, select, update, agg

## Join with Relational Data for more information

## Create View to persist with Relational Data



< [Back to Overview](README.md)