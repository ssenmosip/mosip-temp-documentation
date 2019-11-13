# Data Architecture Principles

* Personal identifiable information of an individual like name, age, gender, address etc and other sensitive information must be signed and stored in an encrypted form
* Documents and images must not be stored in a database table. They must be stored in a file system and referenced in DB.
* No business logic applied at database level, only Primary / Unique key, Not null and foreign keys are applied. Foreign keys are applied within the same database, if a table is referenced in another database then no FK is applied
* Database specific features like triggers, DB functions like sequence generators etc must not be used in MOSIP. This avoids vendor lock-in
* Keys (surrogate keys), wherever used, must be a random number and not be generated based on the record data. This improves privacy
* Direct queries on the database by a human must not be made. Database administrators must ensure this control during database configuration setup
* All DDL and DML statements must follow ANSI standards
* Database is setup in UTF-8*** file format to support multiple languages
* Only following datatypes are used
    - Character varying
    - Timestamp
    - Date
    - Integer
    - Number
    - Bytea/blob
    - Boolean

# Logical view of MOSIP data system

![MOSIP Data Architecture](_images/arch_diagrams/MOSIP_DataArchitecture.jpg)

## Security

In MOSIP, the following roles are defined to perform various activities and have control over the DB objects that are defined

* **sysadmin:** sysadmin user/role is a super administrator role, who will have all the privileges to perform any task within the database. Currently all the objects are being owned by this user / role.
	
* **dbadmin:** dbadmin user / role is created to handle all the database administration activities db monitoring, performance tuning, backups, restore, replication setup, etc.
	
* **appadmin:** appadmin user / role is used to perform all the DDL (Data Definition Language) tasks. All the db objects that are created in these databases will be owned by appadmin user.
	
* **Application User:** Each application will have a user / role created to perform DML (Data Manipulation Language) tasks like CRUD operations (select, insert, update, delete). The user prereguser, is created to connect from the application to perform all the DML activities. Similarly, we will have masteruser, prereguser, reguser, idauser, idrepouser, idmapuser, kerneluser, audituser, regprcuser to perform DML tasks for master, pre-registration, registration, ida, ID repository, ID Map, kernel, audit and registration processor modules respectively.

**Note:** From the above set of roles only application user / role is specific to a application / module. The other user / roles are common which needs to be  created per postresql db instance / server.

Apart from the above, MOSIP will provide control over accessing data by various users based on the user access defined at zone level. This will implemented at application layer. 

## Multi-Language

MOSIP platform is being built for multiple countries, there is a need to support multiple languages. So as per the requirements, MOSIP will support 3 languages as configured by the country level administrator.
Multi language support is needed for the following datasets. 

* Master Data
* ID data of an individual
* Transaction comments
* Labels used in UI
* Messages and notifications

From database side, the data will support **UTF-8 Unicode character set** to store data entered in multiple languages. 
There will not be any in-built support to translate data at database level. Any translation or transliteration will be handled at API or UI layer.

## High Availability

TBD

## Auditability

TBD


## High Performance

To support high performance, following database design features are to be considered

* Database sharding is applied on uin dataset. By default, base sharding algorithm will be applied in MOSIP system. SI can define the sharding algorithm based on the deployment setup
* All tables will have a primary key index on the primary key field. This will help in faster retrievals and joins
* All foreign keys will have indexes defined so that it will help in faster joins
* No referential integrity is applied on tables across databases
* Partitioning: Partitioning design to be discussed as PostgreSQL has certain limitation / different way of implementation that requires specific database features to be applied. To be discussed further to finalize the implementation of this feature.

The performance related strategies are detailed in [Database Performance](Database-Performance). This needs to be further discussed and elaborated as per need.

# Data Model Naming Standards

[Naming Standards](Data-Model-Naming-Standards)

# Data Model

[Data Model](MOSIP-Data-Model)
