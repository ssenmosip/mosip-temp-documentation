This section covers high-level data architecture principles of MOSIP.

* Open source and Vendor Neutral
* Adaptability
* Security
* Multi party
* Authorization
* Authentication
* Multi language support
* Performance and scalability
* High Availability
* Auditability

# Open Source and Vendor Neutral

To handle vendor neutrality and open source, the following consideration are followed while designing the data model and the database design.

+ No business logic is applied at database level: Database will be used only to store and retrieve data. There is no business logic applied at database level other than Primary / Unique key, Not null and foreign keys. Foreign keys are applied within the same database, if a table is referenced in another database then no FK is applied. 

+ No specific database features to be used: Features that are common across databases which are compliant with open source standards are applied. 

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

# Adaptability

TBD

# Security

TBD

# Multi party

TBD

# Authorization

TBD

# Authentication

TBD


# Multi-Language

MOSIP platform is being built for multiple countries, there is a need to support multiple languages. So as per the requirements, MOSIP will support 3 languages as configured by the country level administrator.
Multi language support is needed for the following datasets. 

* Master Data
* ID data of an individual
* Transaction comments
* Labels used in UI
* Messages and notifications

From database side, the data will support **UTF-8 Unicode character set** to store data entered in multiple languages. 
There will not be any in-built support to translate data at database level. Any translation or transliteration will be handled at API or UI layer.

# High Availability

TBD

# Auditability

TBD


# High Performance

To support high performance, following database design features are to be considered

* Database sharding is applied on uin dataset. By default, base sharding algorithm will be applied in MOSIP system. SI can define the sharding algorithm based on the deployment setup
* All tables will have a primary key index on the primary key field. This will help in faster retrievals and joins
* All foreign keys will have indexes defined so that it will help in faster joins
* No referential integrity is applied on tables across databases
* Partitioning: Partitioning design to be discussed as PostgreSQL has certain limitation / different way of implementation that requires specific database features to be applied. To be discussed further to finalize the implementation of this feature.
