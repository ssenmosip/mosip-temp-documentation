# Data Architecture Principles

Below principles are followed in designing the data base of MOSIP

* All personally identifiable information like name, age, gender, address etc will be stored in an encrypted form
* The primary key for a record will be a random number and never generated based on the record data
* Select queries by Admin or any other user directly on the database is prohibited. Only application user will be able to do a select query
* Database specific features like triggers, DB functions like sequence generators etc will not be used in MOSIP. This avoids vendor lock-in

## Open Source and Vendor Neutral

To handle vendor neutrality and open source, the following consideration are followed while designing the data model and the database design.

+ No business logic is applied at database level: Database will be used only to store and retrieve data. There is no business logic applied at database level other than Primary / Unique key, Not null and foreign keys. Foreign keys are applied within the same database, if a table is referenced in another database then no FK is applied. 

+ No specific database features used: Features that are common across databases which are compliant with open source standards are applied. 

+ All DDL, DML and DQL statements will follow ANSI standards

+ Metadata approach to handle complex and flexible data structures

+ Only following datatypes are being used
    - Character varying
    - Timestamp
    - Date
    - Integer
    - Number
    - Bytea/blob
    - Boolean

## Security

TBD

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

# Data Architecture

Below diagram provides the data architecture of MOSIP system

![MOSIP Data Architecture](https://github.com/mosip/mosip/blob/DEV_database_sprint6/database-scripts/DataArchitecture/MOSIP_DataArchitecture.jpg)

Below is the list of databases in MOSIP

|Sl No|Database Name|Description|
|---------|---------|------------|
|1|mosip_kernel|Kernel database maintains common / system configurations, data related to kernel services like sync process, OTP, etc.|
|2|mosip_master|All the master data that is defined and related to an organization is stored in this database. Including User management, authentication and authorization services related data is also be stored in this db|
|3|mosip_uin|UIN database stores all the data related to an individual for which an UIN is generated|
|4|mosip_prereg|Pre-registration database to store the data that is captured as part of pre-registration process|
|5|mosip_reg|Registration client database to capture registration related data. The needed data from MOSIP system will be synched with this database.|
|6|mosip_regprc|The data related to Registration process flows and transaction will be maintained in this database. This database also maintains data that is needed to perform deduplication.|
|7|mosip_ida|ID Authorization related requests, transactions and mapping related data like virtual ids, tokens, etc. will be stored in this database|
|8|mosip_audit|Audit related logs and the data is stored in this database|

# Data Model Naming Standards

[Naming Standards](https://github.com/mosip/mosip/wiki/Data-Model-Naming-Standards)

# Data Model

[Data Model](https://github.com/mosip/mosip/wiki/MOSIP-Data-Model)
