This section covers high-level data architecture standards of MOSIP.

* MOSIP is developed on a open source data platform. 
* Chosen data platform is free and open source. 
* Chosen data platform can be replaced with another equivalent component with help of abstraction components
* Software and technology stack doesn’t mandate any specific vendor

Below diagram provides the data architecture of MOSIP system

TBD

The description of the databases created in MOSIP are listed below

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

