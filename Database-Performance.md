# Database Server 

The database is designed in a way that each module can be deployed on same or separate database servers. Even the UIN data is designed to store the data into different database server using sharding methodology. The sharding logic will be implemented at the API level. 

# Table Partitioning Strategy

Table partitioning is part of an advanced database design for better SQL performance.   Generally partitioning strategy is advisable and need to be followed when the data set is very high over millions of rows.  It is dividing the table using set of columns as key

It logically divides the table using a column or columns of data as an index which demarcates the beginning and ending of a segment of data into individual partitions. These act like tables within a table and will improve querying performance. The key is to select the correct data to use as the partition index field and to include that as an element in the SQL where or having clause.

The way partitions are defined in PostgreSQL is different when compared to other commercial databases.  The partitions use techniques like inheritance, constraints and db triggers or rules. This will make things complex so we might not use partition in MOSIP.  **– To be discussed further with the architecture team**

In MOSIP, we have the following types of tables where we will have huge datasets, they are listed below

* Transaction

Transaction tables are huge and will have lots of data. Most of the queries will be on open or in process transactions. So, the main transaction table can contain only open transaction and all closed transactions can be moved to a separate table.

* Audit

Only 6 month of audit data can be maintained in audit table and rest of the data can be moved to audit history table.

* UIN

UIN data will be sharded and stored in different databases, which will provide horizontal scalability.

# Indexing Strategy

All the tables will have a primary key and a primary index created. Also, the foreign keys that are created will also have an index. Apart from that, based on the need necessary indexes would be created.
**<To be elaborated further based on the data read strategy>**
