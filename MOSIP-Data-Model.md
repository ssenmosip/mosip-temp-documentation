This section contains detailed information for data model design standards, guidelines and principles for global master reference, conceptual, logical and physical model design standards been followed in MOSIP project.

# Data Model Standards

Note: Each of the below points to be expanded according to the MOSIP implementation approach.
* Meaningful Naming: DB objects that are being created will have a meaningful naming.
* PK, UK, FK, Not Null constraints
* Flexible model
* Most of the data is encrypted
* No business logic, no defaults, no use of sequences, identify fields at database level
* No DB triggers, avoid DB functions, procedures. If needed, It should be ANSI compliant
* SQL used in application should be ANSI Compliant 
* The data is stored in multiple languages as configured by administrator of the system
* Referential integrity is applied on the tables belonging to same database. If the objects are referred across DB then this will be handled at the application layer.
* Only ID information is encrypted
* System related data will be stored in system default language (mostly English).

# ER Model

TBD

# Logical Data Model

TBD

# Physical Data Model

https://github.com/mosip/mosip/tree/DEV_database_sprint6/database-scripts/data_model 


