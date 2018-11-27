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
