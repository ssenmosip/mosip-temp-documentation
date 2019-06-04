This section contains information on data model design standards, guidelines and principles for global master reference data, conceptual, logical and physical model design standards followed in MOSIP project.

# Data Model Standards

Note: Each of the below points to be expanded according to the MOSIP implementation approach.
* Meaningful Naming: DB objects that are being created will have a meaningful naming.
* PK, UK, FK, Not Null constraints
* Flexible model
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

Below is the list of databases in MOSIP

|Sl No|Database Name|Description|Data Model|Data Dictionary|
|---------|---------|------------|----------|-----------|
|1|mosip_kernel|Kernel database maintains common / system configurations, data related to kernel services like sync process, OTP, etc.|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_kernel.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_kernel.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_kernel_dd.xlsx)</div>|
|2|mosip_master|All the master data that is defined and related to an organization is stored in this database. Including User management, authentication and authorization services related data is also be stored in this db|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_master.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_master.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_master_dd.xlsx)</div>|
|3|mosip_idrepo|ID repository database stores all the data related to an individual for which an UIN is generated|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idrepo.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idrepo.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idrepo_dd.xlsx)</div>|
|4|mosip_prereg|Pre-registration database to store the data that is captured as part of pre-registration process|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_prereg.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_prereg.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_prereg_dd.xlsx)</div>|
|5|mosip_reg|Registration client database to capture registration related data. The needed data from MOSIP system will be synched with this database.|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_reg.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_reg.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_reg_dd.xlsx)</div>|
|6|mosip_regprc|The data related to Registration process flows and transaction will be maintained in this database. This database also maintains data that is needed to perform deduplication.|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_regprc.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_regprc.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_regprc_dd.xlsx)</div>|
|7|mosip_ida|ID Authentication related requests, transactions and mapping related data like virtual ids, tokens, etc. will be stored in this database|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_ida.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_ida.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_ida_dd.xlsx)</div>|
|8|mosip_audit|Audit related logs and the data is stored in this database|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_audit.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_audit.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_audit_dd.xlsx)</div>|
|9|mosip_iam|The user management related data of MOSIP application is stored in various storages, the database related users are stored in this database|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_iam.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_iam.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_iam_dd.xlsx)</div>|
|10|mosip_idmap|Database to store and manage all the data related to mapping between various IDs, like vid with UIN of an individual|<div>[DBM File](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idmap.dbm)</div> <div>[Image File ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idmap.png)</div>|<div>[Data Model (Image) ](https://github.com/mosip/mosip/blob/master/scripts/database/data_model/mosip_idmap_dd.xlsx)</div>|

<div>https://github.com/mosip/mosip/tree/DEV_database_sprint6/database-scripts/data_model</div> 


