## Table Of Content

- [1. Common Services](#1-common-services-)
- [2. Data Services](#2-data-services-)
- [3. Admin Services](#3-admin-services-)
- [4. UIN  Generation](#4-uin--generation-)
- [5. Configuration Server](#5-configuration-server-)
- [6. Audit Manager](#6-audit-manager-)
- [7. Authentication and Authorization](#7-authentication-and-authorization-)
- [8. Pre-registration](#8-pre-registration-)
- [9. Registration](#9-registration-)
- [10. Registration Processor](#10-registration-processor-)
- [11. Authentication](#11-authentication-)
- [12. Resident Services](#12-resident-services-)
- [13. Administration](#13-administration-)
- [14. Partner Management](#14-partner-management-)

## 1. Common Services: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|OTP Manager|Generates and Validates OTP as per the defined policies|[CMN_FR_1](FRS-Common-Services)|[MOS-33](//mosipid.atlassian.net/browse/MOS-33), [MOS-34](//mosipid.atlassian.net/browse/MOS-34), [MOS-35](//mosipid.atlassian.net/browse/MOS-35), [MOS-36](//mosipid.atlassian.net/browse/MOS-36), [MOS-423](//mosipid.atlassian.net/browse/MOS-423), [MOS-991](//mosipid.atlassian.net/browse/MOS-991), [MOS-1056](//mosipid.atlassian.net/browse/MOS-1056), [MOS-1985](//mosipid.atlassian.net/browse/MOS-1985), [MOS-5486](//mosipid.atlassian.net/browse/MOS-5486)|
|2.|QR Code Generator|This utility enables QR code generation for pre-registration, registration and UIN acknowledgment|[CMN_FR_2](FRS-Common-Services)|[MOS-979](//mosipid.atlassian.net/browse/MOS-979)|
|3.|Crypto Services|Key Generator|[CMN_FR_3.1](FRS-Common-Services)|[MOS-788](//mosipid.atlassian.net/browse/MOS-788), [MOS-1431](//mosipid.atlassian.net/browse/MOS-1431)|
|4.|Crypto Services|Key Management|[CMN_FR_3.2](FRS-Common-Services)|[MOS-9284](//mosipid.atlassian.net/browse/MOS-9284)|
|5.|Crypto Services|Crypto Utility|[CMN_FR_3.3](FRS-Common-Services)|[MOS-9301](//mosipid.atlassian.net/browse/MOS-9301)|
|6.|Crypto Services|Hash Utility|[CMN_FR_3.4](FRS-Common-Services)|[MOS-20](//mosipid.atlassian.net/browse/MOS-20)|
|7.|Crypto Services|HMAC Utility/Checksum Utility|[CMN_FR_3.5](FRS-Common-Services)|[MOS-481](//mosipid.atlassian.net/browse/MOS-481)|
|8.|Email Notification|Generates and sends an Email using a third party vendor|[CMN_FR_4.2](FRS-Common-Services)|[MOS-973](//mosipid.atlassian.net/browse/MOS-973)|
|9.|SMS Notification|Generates and sends an SMS using a third party vendor|[CMN_FR_4.3](FRS-Common-Services)|[MOS-961](//mosipid.atlassian.net/browse/MOS-961)|
|10.|PDF Generator|This utility enables PDF file creation of received content (e.g., acknowledge and notification templates)|[CMN_FR_4.4](FRS-Common-Services)|[MOS-960](//mosipid.atlassian.net/browse/MOS-960), [MOS-12900](//mosipid.atlassian.net/browse/MOS-12900)|
|11.|Template Merger|Merges a pre-configured template with dynamic values|[CMN_FR_4.5](FRS-Common-Services)|[MOS-786](//mosipid.atlassian.net/browse/MOS-786)|
|12.|Transliteration|Performs Transliteration from one language to another|[CMN_FR_5](FRS-Common-Services)|[MOS-975](//mosipid.atlassian.net/browse/MOS-975)|
|13.|Mobile Data Validator|Performs the pattern validation on the mobile number based on the configured length|[CMN_FR_6.1](FRS-Common-Services)|[MOS-1028](//mosipid.atlassian.net/browse/MOS-1028)|
|14.|Email Data Validator|Performs the pattern validation on Email ID based on the configured parameters|[CMN_FR_6.2](FRS-Common-Services)|[MOS-1029](//mosipid.atlassian.net/browse/MOS-1029)|
|15.|Exception Framework|Provides base exception framework|[CMN_FR_6.3](FRS-Common-Services)|[MOS-30](//mosipid.atlassian.net/browse/MOS-30)|
|16.|Utilities|Calendar Utility|[CMN_FR_6.4](FRS-Common-Services)|[MOS-20](//mosipid.atlassian.net/browse/MOS-20)|
|17.|Utilities|Date Utility|[CMN_FR_6.5](FRS-Common-Services)|[MOS-23](//mosipid.atlassian.net/browse/MOS-23), [MOS-1988](//mosipid.atlassian.net/browse/MOS-1988), [MOS-20086](//mosipid.atlassian.net/browse/MOS-20086)|
|18.|Utilities|File Utility|[CMN_FR_6.6](FRS-Common-Services)|[MOS-21](//mosipid.atlassian.net/browse/MOS-21)|
|19.|Utilities|Json Utility|[CMN_FR_6.7](FRS-Common-Services)|[MOS-28](//mosipid.atlassian.net/browse/MOS-28)|
|20.|Utilities|Math Utility|[CMN_FR_6.8](FRS-Common-Services)|[MOS-19](//mosipid.atlassian.net/browse/MOS-19)|
|21.|Utilities|String Utility|[CMN_FR_6.9](FRS-Common-Services)|[MOS-18](//mosipid.atlassian.net/browse/MOS-18)|
|22.|Utilities|UUID Utility|[CMN_FR_6.10](FRS-Common-Services)|[MOS-1986](//mosipid.atlassian.net/browse/MOS-1986)|
|23.|Utilities|Zip-Unzip Utility|[CMN_FR_6.11](FRS-Common-Services)|[MOS-987](//mosipid.atlassian.net/browse/MOS-987)|



## 2. Data Services: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|Data mapper|Facilitate data mapping between DTO (Data Transfer Object) and entity|[DAT_FR_1](FRS-Data-Services)|[MOS-957](//mosipid.atlassian.net/browse/MOS-957)|
|2.|Data Access Manager|Provides an implementation for DAM (Data Access Manager) interface|[DAT_FR_2](FRS-Data-Services)|[MOS-987](//mosipid.atlassian.net/browse/MOS-31), [MOS-987](//mosipid.atlassian.net/browse/MOS-32), [MOS-14007](//mosipid.atlassian.net/browse/MOS-14007)|
|3.|Sync Handler|Enables Registration Client to sync Master data, List of Users, User-Role Mapping and Configurations|[DAT_FR_3](FRS-Data-Services)|[MOS-994](//mosipid.atlassian.net/browse/MOS-994),[MOS-997](//mosipid.atlassian.net/browse/MOS-997),[MOS-996](//mosipid.atlassian.net/browse/MOS-996),[MOS-12079](//mosipid.atlassian.net/browse/MOS-12079),[MOS-12944](//mosipid.atlassian.net/browse/MOS-12944),[MOS-12945](//mosipid.atlassian.net/browse/MOS-12945),[MOS-12946](//mosipid.atlassian.net/browse/MOS-12946),[MOS-12902](//mosipid.atlassian.net/browse/MOS-12902),[MOS-12889](//mosipid.atlassian.net/browse/MOS-12889),[MOS-13945](//mosipid.atlassian.net/browse/MOS-13945),[MOS-12902](//mosipid.atlassian.net/browse/MOS-12902),[MOS-13976](//mosipid.atlassian.net/browse/MOS-987),[MOS-15408](//mosipid.atlassian.net/browse/MOS-987), [MOS-19169](//mosipid.atlassian.net/browse/MOS-19169), [MOS-15408](//mosipid.atlassian.net/browse/MOS-15408), [MOS-13945](//mosipid.atlassian.net/browse/MOS-13945), [MOS-16083](//mosipid.atlassian.net/browse/MOS-16083), [MOS-17328](//mosipid.atlassian.net/browse/MOS-17328)|
|4.|Machine ID Generator|Generates Machine ID|[DAT_FR_4.1](FRS-Data-Services)|[MOS-9711](//mosipid.atlassian.net/browse/MOS-9711)|
|5.|Registration Center ID Generator|Generates Registration Center ID|[DAT_FR_4.2](FRS-Data-Services)|[MOS-1102](//mosipid.atlassian.net/browse/MOS-1102)|
|6.|RID Generator|Generates Registration ID|[DAT_FR_4.3](FRS-Data-Services)|[MOS-431](//mosipid.atlassian.net/browse/MOS-431),[MOS-5191](//mosipid.atlassian.net/browse/MOS-5191),[MOS-13171](//mosipid.atlassian.net/browse/MOS-13171),[MOS-12082](//mosipid.atlassian.net/browse/MOS-12082),[MOS-18217](//mosipid.atlassian.net/browse/MOS-18217)|
|7.|MISP ID Generator|Generates MISP ID|[DAT_FR_4.4](FRS-Data-Services)|[MOS-987](//mosipid.atlassian.net/browse/MOS-987)|
|8.|PRID Generator|Generates PRID|[DAT_FR_4.5](FRS-Data-Services)|[MOS-12095](//mosipid.atlassian.net/browse/MOS-12095), [MOS-735](//mosipid.atlassian.net/browse/MOS-735)|
|9.|VID Generator|Generates VID |[DAT_FR_4.6](FRS-Data-Services)|[MOS-1070](//mosipid.atlassian.net/browse/MOS-1070)|
|10.|Token ID Generator|Generates Token ID|[DAT_FR_4.7](FRS-Data-Services)|[MOS-21930](//mosipid.atlassian.net/browse/MOS-21930),[MOS-12898](//mosipid.atlassian.net/browse/MOS-12898),[MOS-8321](//mosipid.atlassian.net/browse/MOS-8321),[MOS-21930](//mosipid.atlassian.net/browse/MOS-21930)|
|11.|Partner ID Generator|Generates Partner ID|[DAT_FR_4.8](FRS-Data-Services)|[MOS-987](//mosipid.atlassian.net/browse/MOS-987)|
|12.|MISP License Key Generator|Generates MISP License Key|[DAT_FR_4.9](FRS-Data-Services)|[MOS-16828](//mosipid.atlassian.net/browse/MOS-16828)|
|13.|UIN Validator|Validates UIN|[DAT_FR_4.10](FRS-Data-Services)|[MOS-595](//mosipid.atlassian.net/browse/MOS-595),[MOS-9743](//mosipid.atlassian.net/browse/MOS-9743)|
|14.|PRID Validator|Validates PRID|[DAT_FR_4.11](FRS-Data-Services)|[MOS-1007](//mosipid.atlassian.net/browse/MOS-1007)|
|15.|VID Validator|Validates VID|[DAT_FR_4.12](FRS-Data-Services)|[MOS-714](//mosipid.atlassian.net/browse/MOS-714)|
|16.|RID Validator|Validates RID|[DAT_FR_4.13](FRS-Data-Services)|[MOS-1591](//mosipid.atlassian.net/browse/MOS-1591),[MOS-10415](//mosipid.atlassian.net/browse/MOS-10415),[MOS-12093](//mosipid.atlassian.net/browse/MOS-12093),[MOS-13172](//mosipid.atlassian.net/browse/MOS-13172)|

## 3. Admin Services: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|36.|Master Data Management|Registration Center Type - Create/Update/Delete|[ADM_FR_2.1](FRS-Admin-Services)|[MOS-539](//mosipid.atlassian.net/browse/MOS-539), [MOS-10558](//mosipid.atlassian.net/browse/MOS-10558), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|37.|Master Data Management|Registration Center - Create/Read/Update/Delete|[ADM_FR_2.2](FRS-Admin-Services)|[MOS-8220](//mosipid.atlassian.net/browse/MOS-8220), [MOS-8221](//mosipid.atlassian.net/browse/MOS-8221), [MOS-8236](//mosipid.atlassian.net/browse/MOS-8236), [MOS-8244](//mosipid.atlassian.net/browse/MOS-8244), [MOS-9529](//mosipid.atlassian.net/browse/MOS-9529), [MOS-9722](//mosipid.atlassian.net/browse/MOS-9722), [MOS-10560](//mosipid.atlassian.net/browse/MOS-10560), [MOS-11924](//mosipid.atlassian.net/browse/MOS-11924), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-17318](//mosipid.atlassian.net/browse/MOS-17318)|
|38.|Master Data Management|List of Machine Types - Create|[ADM_FR_2.3](FRS-Admin-Services)|[MOS-547](//mosipid.atlassian.net/browse/MOS-547), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|39.|Master Data Management|List of Machine Specifications - Create/Update/Delete|[ADM_FR_2.4](FRS-Admin-Services)|[MOS-551](//mosipid.atlassian.net/browse/MOS-551), [MOS-10565](//mosipid.atlassian.net/browse/MOS-10565), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|40.|Master Data Management|List of Machines - Create/Read/Update/Delete|[ADM_FR_2.5](FRS-Admin-Services)|[MOS-8222](//mosipid.atlassian.net/browse/MOS-8222), [MOS-8229](//mosipid.atlassian.net/browse/MOS-8229), [MOS-9723](//mosipid.atlassian.net/browse/MOS-9723), [MOS-10566](//mosipid.atlassian.net/browse/MOS-10566), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|41.|Master Data Management|Mappings of Registration Center, Machine and User Mappings - Create/Read/Delete|[ADM_FR_2.6](FRS-Admin-Services)|[MOS-8232](//mosipid.atlassian.net/browse/MOS-8232), [MOS-10306](//mosipid.atlassian.net/browse/MOS-10306), [MOS-10589](//mosipid.atlassian.net/browse/MOS-10589), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|42.|Master Data Management|Create/Read/Update/Delete - Location Hierarchy|[ADM_FR_1.1](FRS-Admin-Services)|[MOS-8233](//mosipid.atlassian.net/browse/MOS-8233), [MOS-8234](//mosipid.atlassian.net/browse/MOS-8234), [MOS-550](//mosipid.atlassian.net/browse/MOS-550), [MOS-12155](//mosipid.atlassian.net/browse/MOS-12155), [MOS-13943](//mosipid.atlassian.net/browse/MOS-13943), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-10591](//mosipid.atlassian.net/browse/MOS-10591)|
|43.|Master Data Management|List of Holidays - Create/Read/Update/Delete|[ADM_FR_1.2](FRS-Admin-Services)|[MOS-8235](//mosipid.atlassian.net/browse/MOS-8235), [MOS-549](//mosipid.atlassian.net/browse/MOS-549), [MOS-8565](//mosipid.atlassian.net/browse/MOS-8565), [MOS-10593](//mosipid.atlassian.net/browse/MOS-10593), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|44.|Master Data Management|Biometric Authentication Type - Create/Read|[ADM_FR_1.3](FRS-Admin-Services)|[MOS-8245](//mosipid.atlassian.net/browse/MOS-8245), [MOS-9622](//mosipid.atlassian.net/browse/MOS-9622), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|45.|Master Data Management|Biometric Attirbute Type - Create/Read|[ADM_FR_1.4](FRS-Admin-Services)|[MOS-8246](//mosipid.atlassian.net/browse/MOS-8246), [MOS-9623](//mosipid.atlassian.net/browse/MOS-9623), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|46.|Master Data Management|Gender - Create/Read/Update/Delete|[ADM_FR_1.5](FRS-Admin-Services)|[MOS-8266](//mosipid.atlassian.net/browse/MOS-8266), [MOS-9624](//mosipid.atlassian.net/browse/MOS-9624), [MOS-988](//mosipid.atlassian.net/browse/MOS-988), [MOS-13944](//mosipid.atlassian.net/browse/MOS-13944), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|47.|Master Data Management|Document Category - Create/Read/Update/Delete|[ADM_FR_1.6](FRS-Admin-Services)|[MOS-8269](//mosipid.atlassian.net/browse/MOS-8269), [MOS-9683](//mosipid.atlassian.net/browse/MOS-9683), [MOS-10567](//mosipid.atlassian.net/browse/MOS-10567), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|48.|Master Data Management|Document Type - Create/Update/Delete|[ADM_FR_1.7](FRS-Admin-Services)|[MOS-9684](//mosipid.atlassian.net/browse/MOS-9684), [MOS-10569](//mosipid.atlassian.net/browse/MOS-10569), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|49.|Master Data Management|Applicant Type-Document Category-Document Type Mapping - Read|[ADM_FR_1.8](FRS-Admin-Services)|[MOS-12060](//mosipid.atlassian.net/browse/MOS-12060), [MOS-13962](//mosipid.atlassian.net/browse/MOS-13962), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-12068](//mosipid.atlassian.net/browse/MOS-12068), [MOS-13591](//mosipid.atlassian.net/browse/MOS-13591), [MOS-22085](//mosipid.atlassian.net/browse/MOS-22085)|
|50.|Master Data Management|List of Devices - Create/Read/Update/Delete|[ADM_FR_2.7](FRS-Admin-Services)|[MOS-8263](//mosipid.atlassian.net/browse/MOS-8263), [MOS-9695](//mosipid.atlassian.net/browse/MOS-9695), [MOS-12057](//mosipid.atlassian.net/browse/MOS-12057), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-10563](//mosipid.atlassian.net/browse/MOS-10563)|
|51.|Master Data Management|List of Device Specifications - Create/Read/Update/Delete|[ADM_FR_2.8](FRS-Admin-Services)|[MOS-8264](//mosipid.atlassian.net/browse/MOS-8264), [MOS-9788](//mosipid.atlassian.net/browse/MOS-9788), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-10562](//mosipid.atlassian.net/browse/MOS-10562)|
|52.|Master Data Management|List of Device Types - Create/Update/Delete|[ADM_FR_2.9](FRS-Admin-Services)|[MOS-9787](//mosipid.atlassian.net/browse/MOS-9787), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|53.|Master Data Management|List of Languages - Create/Read/Update/Delete|[ADM_FR_1.9](FRS-Admin-Services)|[MOS-8265](//mosipid.atlassian.net/browse/MOS-8265), [MOS-1075](//mosipid.atlassian.net/browse/MOS-1075), [MOS-10554](//mosipid.atlassian.net/browse/MOS-10554), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|54.|Master Data Management|List of Titles - Create/Read/Update/Delete|[ADM_FR_1.10](FRS-Admin-Services)|[MOS-8267](//mosipid.atlassian.net/browse/MOS-8267), [MOS-9696](//mosipid.atlassian.net/browse/MOS-9696), [MOS-992](//mosipid.atlassian.net/browse/MOS-992), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|55.|Master Data Management|Template File Format - Create/Update/Delete|[ADM_FR_1.11](FRS-Admin-Services)|[MOS-9687](//mosipid.atlassian.net/browse/MOS-9687), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076), [MOS-10573](//mosipid.atlassian.net/browse/MOS-10573)|
|56.|Master Data Management|List of Template Types - Create|[ADM_FR_1.12](FRS-Admin-Services)|[MOS-586](//mosipid.atlassian.net/browse/MOS-586), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|57.|Master Data Management|List of Templates - Create/Read/Update/Delete|[ADM_FR_1.13](FRS-Admin-Services)|[MOS-8271](//mosipid.atlassian.net/browse/MOS-8271), [MOS-995](//mosipid.atlassian.net/browse/MOS-995), [MOS-10590](//mosipid.atlassian.net/browse/MOS-10590), [MOS-15461](//mosipid.atlassian.net/browse/MOS-15461), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|58.|Master Data Management|List of Blacklisted Words - Create/Read/Update/Delete|[ADM_FR_1.14](FRS-Admin-Services)|[MOS-8268](//mosipid.atlassian.net/browse/MOS-8268), [MOS-9697](//mosipid.atlassian.net/browse/MOS-9697), [MOS-1054](//mosipid.atlassian.net/browse/MOS-1054), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|59.|Master Data Management|List of Reason Categories - Create|[ADM_FR_1.15](FRS-Admin-Services)|[MOS-9689](//mosipid.atlassian.net/browse/MOS-9689), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|60.|Master Data Management|List of Rejection Reasons - Create/Read|A[DM_FR_1.16](FRS-Admin-Services)|[MOS-8551](//mosipid.atlassian.net/browse/MOS-8551), [MOS-9690](//mosipid.atlassian.net/browse/MOS-9690),[MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|61.|Master Data Management|List of Applications - Create/Read|[ADM_FR_1.17](FRS-Admin-Services)|[MOS-8888](//mosipid.atlassian.net/browse/MOS-8888), [MOS-9688](//mosipid.atlassian.net/browse/MOS-9688), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|62.|Master Data Management|List of ID Types - Create/Read|[ADM_FR_1.18](FRS-Admin-Services)|[MOS-8247](//mosipid.atlassian.net/browse/MOS-8247), [MOS-9691](//mosipid.atlassian.net/browse/MOS-9691),[MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|63.|Master Data Management|Mappings of Registration Center and Machine - Create/Read/Delete|[ADM_FR_2.10](FRS-Admin-Services)|[MOS-9728](//mosipid.atlassian.net/browse/MOS-9728), [MOS-9712](//mosipid.atlassian.net/browse/MOS-9712), [MOS-1053](//mosipid.atlassian.net/browse/MOS-1053), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|64.|Master Data Management|Mappings of Registration Center and Device - Create/Read/Delete|[ADM_FR_2.11](FRS-Admin-Services)|[MOS-9729](//mosipid.atlassian.net/browse/MOS-9729), [MOS-9712](//mosipid.atlassian.net/browse/MOS-9712), [MOS-10561](//mosipid.atlassian.net/browse/MOS-10561), [MOS-12058](//mosipid.atlassian.net/browse/MOS-12058), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|65.|Master Data Management|Mappings of Registration Center, Machine and Device - Create/Read/Delete|[ADM_FR_2.12](FRS-Admin-Services)|[MOS-9730](//mosipid.atlassian.net/browse/MOS-9730), [MOS-9712](//mosipid.atlassian.net/browse/MOS-9712), [MOS-10564](//mosipid.atlassian.net/browse/MOS-10564), [MOS-12076](//mosipid.atlassian.net/browse/MOS-12076)|
|66.|Master Data Management|Individual Type Management - Read|[ADM_FR_1.19](FRS-Admin-Services)|[MOS-13950](//mosipid.atlassian.net/browse/MOS-13950)|


## 4. UIN  Generation: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|UIN Generator|Generates UIN|[UIG_FR_1](Audit Manager)|[MOS-425](//mosipid.atlassian.net/browse/MOS-425),[MOS-9738](//mosipid.atlassian.net/browse/MOS-9738), [MOS-22036](//mosipid.atlassian.net/browse/MOS-22036), [MOS-18828](//mosipid.atlassian.net/browse/MOS-18828),[MOS-15406](//mosipid.atlassian.net/browse/MOS-15406)|

## 5. Configuration Server: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|||||

## 6. Audit Manager: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|Audit Manager|Provides service across MOSIP to store Audit logs|[AMG_FR_1](Audit Manager)|[MOS-8](//mosipid.atlassian.net/browse/MOS-8),[MOS-441](//mosipid.atlassian.net/browse/MOS-441), [MOS-829](//mosipid.atlassian.net/browse/MOS-829), [MOS-12903](//mosipid.atlassian.net/browse/MOS-12903)|

## 7. Authentication and Authorization: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|Authentication and Authorization|Provides authenticaiton and Authorization across MOSIP|[AUT_FR_1](Authentication and Authorization(WIP)|[MOS-1000](//mosipid.atlassian.net/browse/MOS-1000)|

## 8. Pre-registration: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|pre-registration-ui|Login/Creating a User Account|PRE_FR_1|[MOS-17](//mosipid.atlassian.net/browse/MOS-17), [MOS-26](//mosipid.atlassian.net/browse/MOS-26), [MOS-980](//mosipid.atlassian.net/browse/MOS-980), [MOS-13173](//mosipid.atlassian.net/browse/MOS-13173)|
|2.|pre-registration-ui|Login/Creating a User Account|PRE_FR_1.1|[MOS-26](//mosipid.atlassian.net/browse/MOS-26)|
|3.|pre-registration-ui|Login/Creating a User Account|PRE_FR_1.2|[MOS-17](//mosipid.atlassian.net/browse/MOS-17)|
|4.|pre-registration-ui|Logout/Session Timeout|PRE_FR_1.4|[MOS-205](//mosipid.atlassian.net/browse/MOS-205), [MOS-10485](//mosipid.atlassian.net/browse/MOS-10485), [MOS-17869](//mosipid.atlassian.net/browse/MOS-17869)|
|5.|pre-registration-ui|Creating an Application|PRE_FR_2|[MOS-792](//mosipid.atlassian.net/browse/MOS-792), [MOS-793](//mosipid.atlassian.net/browse/MOS-793), [MOS-14511](//mosipid.atlassian.net/browse/MOS-14511)|
|6.|pre-registration-demographic-service, pre-registration-document-service|Creating an Application|PRE_FR_2|[MOS-623](//mosipid.atlassian.net/browse/MOS-623), [MOS-625](//mosipid.atlassian.net/browse/MOS-625)|
|7.|pre-registration-ui|Provide Consent|PRE_FR_2.2|[MOS-13682](//mosipid.atlassian.net/browse/MOS-13682)|
|8.|pre-registration-ui|Provide Consent|PRE_FR_2.3|[MOS-623](//mosipid.atlassian.net/browse/MOS-623), [MOS-625](//mosipid.atlassian.net/browse/MOS-625)|
|9.|pre-registration-ui|Provide Data in Preferred Language|PRE_FR_2.4|[MOS-666](//mosipid.atlassian.net/browse/MOS-666), [MOS-13144](//mosipid.atlassian.net/browse/MOS-13144),[MOS-13965](//mosipid.atlassian.net/browse/MOS-13965)|
|10.|pre-registration-translitration-service|Provide Data in Preferred Language|PRE_FR_2.4|[MOS-667](//mosipid.atlassian.net/browse/MOS-667)|
|11.|pre-registration-ui|Viewing "My Applications"|PRE_FR_2.5|[MOS-794](//mosipid.atlassian.net/browse/MOS-794)|
|12.||Viewing "My Applications"|PRE_FR_2.5|[MOS-626](//mosipid.atlassian.net/browse/MOS-626)|
|13.|pre-registration-ui|Modify Application Data|PRE_FR_2.6|[MOS-797](//mosipid.atlassian.net/browse/MOS-797)|
|14.|pre-registration-demographic-service, pre-registration-document-service|Modify Application Data|PRE_FR_2.6|[MOS-628](//mosipid.atlassian.net/browse/MOS-628)|
|15.|pre-registration-ui|Discard Application|PRE_FR_2.7|[MOS-806](//mosipid.atlassian.net/browse/MOS-806)|
|16.||Discard Application|PRE_FR_2.7|[MOS-805](//mosipid.atlassian.net/browse/MOS-805))|
|17.|pre-registration-document-service|Attaching Documents for Reference|PRE_FR_3|[MOS-623](//mosipid.atlassian.net/browse/MOS-623), [MOS-625](//mosipid.atlassian.net/browse/MOS-625)|
|18.|pre-registration-ui|Choosing a Registration Center for Appointment|PRE_FR_4.1|[MOS-814](//mosipid.atlassian.net/browse/MOS-814)|
|19.|pre-registration-ui|Choosing Appointment Slots|PRE_FR_4.3|[MOS-817](//mosipid.atlassian.net/browse/MOS-817)|
|20.|pre-registration-booking-service|Choosing Appointment Slots|PRE_FR_4.3|[MOS-664](//mosipid.atlassian.net/browse/MOS-664)|
|21.|pre-registration-ui|Cancel Appointment|PRE_FR_4.4|[MOS-818](//mosipid.atlassian.net/browse/MOS-818)|
|22.|pre-registration-booking-service|Cancel Appointment|PRE_FR_4.4|[MOS-665](//mosipid.atlassian.net/browse/MOS-665)|
|23.|pre-registration-ui|Re-book Appointment|PRE_FR_4.5|[MOS-978](//mosipid.atlassian.net/browse/MOS-978)|
|24.|pre-registration-booking-service|Re-book Appointment|PRE_FR_4.5|[MOS-978](//mosipid.atlassian.net/browse/MOS-978)|
|25.|pre-registration-ui|Appointment Acknowledgement (PRID)|PRE_FR_5|[MOS-812](//mosipid.atlassian.net/browse/MOS-812), [MOS-13142](//mosipid.atlassian.net/browse/MOS-13142), [MOS-13143](//mosipid.atlassian.net/browse/MOS-13143)|
|26.|pre-registration-ui|Get Appointment for the Day|PRE_FR_4.2|[MOS-816](//mosipid.atlassian.net/browse/MOS-816)|
|27.|pre-registration-booking-service|Get Appointment for the Day|PRE_FR_4.2|[MOS-663](//mosipid.atlassian.net/browse/MOS-663)|
|28.|pre-registration-datasync-service|Retrieve Application Data by PRID|PRE_FR_6.1|[MOS-668](//mosipid.atlassian.net/browse/MOS-668), [MOS-1999](//mosipid.atlassian.net/browse/MOS-1999)|
|29.||List of Configurable Parameters and Processes|PRE_FR_7|[MOS-10291](//mosipid.atlassian.net/browse/MOS-10291), [MOS-14510](//mosipid.atlassian.net/browse/MOS-14510)|


## 9. Registration: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|RC Setup & Update| Master Data Sync | REG_FR_2.1| [MOS-16941](//mosipid.atlassian.net/browse/MOS-16941), [MOS-22389](//mosipid.atlassian.net/browse/MOS-22389)|
|2.|New Registration| Master Data Sync | REG_FR_2.1| [MOS-16791](//mosipid.atlassian.net/browse/MOS-16791), [MOS-16537](//mosipid.atlassian.net/browse/MOS-16537), [MOS-16537](//mosipid.atlassian.net/browse/MOS-16537), [MOS-16778](//mosipid.atlassian.net/browse/MOS-16778), [MOS-13657](//mosipid.atlassian.net/browse/MOS-13657), [MOS-13655](//mosipid.atlassian.net/browse/MOS-13655), [MOS-13557](//mosipid.atlassian.net/browse/MOS-13557), [MOS-13661](//mosipid.atlassian.net/browse/MOS-13661) |
|3.|UIN update| Master Data Sync | REG_FR_2.1| [MOS-13660](//mosipid.atlassian.net/browse/MOS-13660), [MOS-12984](//mosipid.atlassian.net/browse/MOS-12984) |
|4.|Authentication| Master Data Sync | REG_FR_2.1| [MOS-13659](//mosipid.atlassian.net/browse/MOS-13659)|
|5.|Sync| Master Data Sync | REG_FR_2.1| [MOS-11644](//mosipid.atlassian.net/browse/MOS-11644), [MOS-18331](//mosipid.atlassian.net/browse/MOS-18331), [MOS-13994](//mosipid.atlassian.net/browse/MOS-13994), [MOS-11582](//mosipid.atlassian.net/browse/MOS-11582), [MOS-1279](//mosipid.atlassian.net/browse/MOS-1279), [MOS-1243](//mosipid.atlassian.net/browse/MOS-1243), [MOS-1235](//mosipid.atlassian.net/browse/MOS-1235), [MOS-1227](//mosipid.atlassian.net/browse/MOS-1227) |
|6.|EoD process|End of day process | REG_FR_4.8| [MOS-11767](//mosipid.atlassian.net/browse/MOS-11767), [MOS-9108](//mosipid.atlassian.net/browse/MOS-9108), [MOS-9090](//mosipid.atlassian.net/browse/MOS-9090), [MOS-9036](//mosipid.atlassian.net/browse/MOS-9036), [MOS-8624](//mosipid.atlassian.net/browse/MOS-8624), [MOS-558](//mosipid.atlassian.net/browse/MOS-558), [MOS-556](//mosipid.atlassian.net/browse/MOS-556), [MOS-22010](//mosipid.atlassian.net/browse/MOS-22010), [MOS-22009](//mosipid.atlassian.net/browse/MOS-22009), [MOS-22008](//mosipid.atlassian.net/browse/MOS-22008), [MOS-22007](//mosipid.atlassian.net/browse/MOS-22007), [MOS-22006](//mosipid.atlassian.net/browse/MOS-22006), [MOS-21928](//mosipid.atlassian.net/browse/MOS-21928)|
|7.|New Registration| Appointments (PRIDs) | REG_FR_2.1| [MOS-13556](//mosipid.atlassian.net/browse/MOS-13556), [MOS-1204](//mosipid.atlassian.net/browse/MOS-1204) |
|8.|Sync| Pre-registration Data Download | REG_FR_2.5| [MOS-1367](//mosipid.atlassian.net/browse/MOS-1367), [MOS-1277](//mosipid.atlassian.net/browse/MOS-1277), [MOS-1223](//mosipid.atlassian.net/browse/MOS-1223), [MOS-1200](//mosipid.atlassian.net/browse/MOS-1200)|
|9.|New Registration| Pre-registration Data Download  | REG_FR_2.5| [MOS-13556](//mosipid.atlassian.net/browse/MOS-13556), [MOS-1204](//mosipid.atlassian.net/browse/MOS-1204) |
|10.|Sync| Pre-registration Data Download  | REG_FR_2.5| [MOS-11582](//mosipid.atlassian.net/browse/MOS-11582), [MOS-1277](//mosipid.atlassian.net/browse/MOS-1277), [MOS-1223](//mosipid.atlassian.net/browse/MOS-1223), [MOS-1200](//mosipid.atlassian.net/browse/MOS-1200),[MOS-1367](//mosipid.atlassian.net/browse/MOS-1367) |
|11.|Sync| New Registration | REG_FR_4.1| [MOS-13983](//mosipid.atlassian.net/browse/MOS-13983) | 
|12.|Packet Exporter| Registration Packet Upload | REG_FR_7.1| [MOS-13561](//mosipid.atlassian.net/browse/MOS-13561),[MOS-1328](//mosipid.atlassian.net/browse/MOS-1328),[MOS-559](//mosipid.atlassian.net/browse/MOS-559),[MOS-12961](//mosipid.atlassian.net/browse/MOS-12961), [MOS-22013](//mosipid.atlassian.net/browse/MOS-22013), [MOS-22012](//mosipid.atlassian.net/browse/MOS-22012), [MOS-21929](//mosipid.atlassian.net/browse/MOS-21929)| 
|13.|EOD Process| Offline upload (Packet Exporter)  (Packet Exporter) | REG_FR_7.2| [MOS-16712](//mosipid.atlassian.net/browse/MOS-16712) | 
|14.|New Registration| Offline upload (Packet Exporter) | REG_FR_7.2| [MOS-9072](//mosipid.atlassian.net/browse/MOS-9072)| 
|15.|Packet Exporter| Offline upload (Packet Exporter)  | REG_FR_7.2| [MOS-1328](//mosipid.atlassian.net/browse/MOS-1328), [MOS-1305](//mosipid.atlassian.net/browse/MOS-1305),[MOS-559](//mosipid.atlassian.net/browse/MOS-559) | 
|16.|Sync| Offline upload (Packet Exporter)  | REG_FR_7.2| [MOS-63](//mosipid.atlassian.net/browse/MOS-63) | 
|17.|Lost UIN| Lost UIN | REG_FR_4.3| [MOS-18989](//mosipid.atlassian.net/browse/MOS-18989),[MOS-18117](//mosipid.atlassian.net/browse/MOS-18117) | 
|18.|New Registration| New Registration | REG_FR_4.1| [MOS-18100](//mosipid.atlassian.net/browse/MOS-18100),[MOS-17663](//mosipid.atlassian.net/browse/MOS-17663), [MOS-21861](//mosipid.atlassian.net/browse/MOS-21861),[MOS-21860](//mosipid.atlassian.net/browse/MOS-21860), [MOS-16544](//mosipid.atlassian.net/browse/MOS-16544),[MOS-16109](//mosipid.atlassian.net/browse/MOS-16109), [MOS-15918](//mosipid.atlassian.net/browse/MOS-15918),[MOS-15324](//mosipid.atlassian.net/browse/MOS-15324), [MOS-14566](//mosipid.atlassian.net/browse/MOS-14566),[MOS-21863](//mosipid.atlassian.net/browse/MOS-21863), [MOS-14565](//mosipid.atlassian.net/browse/MOS-14565),[MOS-14046](//mosipid.atlassian.net/browse/MOS-14046),[MOS-13661](//mosipid.atlassian.net/browse/MOS-13661), [MOS-12999](//mosipid.atlassian.net/browse/MOS-12999),[MOS-12193](//mosipid.atlassian.net/browse/MOS-12193), [MOS-12186](//mosipid.atlassian.net/browse/MOS-12186),[MOS-12176](//mosipid.atlassian.net/browse/MOS-12176), [MOS-335](//mosipid.atlassian.net/browse/MOS-335),[MOS-294](//mosipid.atlassian.net/browse/MOS-294), [MOS-236](//mosipid.atlassian.net/browse/MOS-236),[MOS-1015](//mosipid.atlassian.net/browse/MOS-1015), [MOS-1016](//mosipid.atlassian.net/browse/MOS-1016),[MOS-1017](//mosipid.atlassian.net/browse/MOS-1017), [MOS-1177](//mosipid.atlassian.net/browse/MOS-1177),[MOS-11678](//mosipid.atlassian.net/browse/MOS-11678), [MOS-1382](//mosipid.atlassian.net/browse/MOS-1382), [MOS-1342](//mosipid.atlassian.net/browse/MOS-1342), [MOS-1331](//mosipid.atlassian.net/browse/MOS-1331), [MOS-5482](//mosipid.atlassian.net/browse/MOS-5482), [MOS-1325](//mosipid.atlassian.net/browse/MOS-1325), [MOS-1291](//mosipid.atlassian.net/browse/MOS-1291), [MOS-1291](//mosipid.atlassian.net/browse/MOS-1291), [MOS-1290](//mosipid.atlassian.net/browse/MOS-1290), [MOS-1302](//mosipid.atlassian.net/browse/MOS-1302), [MOS-1205](//mosipid.atlassian.net/browse/MOS-1205), [MOS-1214](//mosipid.atlassian.net/browse/MOS-1214), [MOS-1221](//mosipid.atlassian.net/browse/MOS-1221), [MOS-1252](//mosipid.atlassian.net/browse/MOS-1252), [MOS-1285](//mosipid.atlassian.net/browse/MOS-1285), [MOS-21873](//mosipid.atlassian.net/browse/MOS-21873), [MOS-1287](//mosipid.atlassian.net/browse/MOS-1287), [MOS-21924](//mosipid.atlassian.net/browse/MOS-21924), [MOS-21923](//mosipid.atlassian.net/browse/MOS-21923), [MOS-21922](//mosipid.atlassian.net/browse/MOS-21922), [MOS-21921](//mosipid.atlassian.net/browse/MOS-21921) |
|19.|UIN update| UIN Updates | REG_FR_3.5| [MOS-19014](//mosipid.atlassian.net/browse/MOS-19014),[MOS-18319](//mosipid.atlassian.net/browse/MOS-18319), [MOS-15998](//mosipid.atlassian.net/browse/MOS-15998),[MOS-14999](//mosipid.atlassian.net/browse/MOS-14999), [MOS-13660](//mosipid.atlassian.net/browse/MOS-13660),[MOS-13560](//mosipid.atlassian.net/browse/MOS-13560), [MOS-13524](//mosipid.atlassian.net/browse/MOS-13524),[MOS-12984](//mosipid.atlassian.net/browse/MOS-12984), [MOS-1299](//mosipid.atlassian.net/browse/MOS-1299),[MOS-1178](//mosipid.atlassian.net/browse/MOS-1178) |
|20.|Acknowledgement| Acknowledgement and Notifications | REG_FR_4.4| [MOS-13559](//mosipid.atlassian.net/browse/MOS-13559), [MOS-1278](//mosipid.atlassian.net/browse/MOS-1278), [MOS-1273](//mosipid.atlassian.net/browse/MOS-1273),[MOS-338](//mosipid.atlassian.net/browse/MOS-338), [MOS-21926](//mosipid.atlassian.net/browse/MOS-21926), [MOS-21927](//mosipid.atlassian.net/browse/MOS-21927)| 
|21.|New Registration| Acknowledgement and Notifications | REG_FR_4.4| [MOS-12167](//mosipid.atlassian.net/browse/MOS-12167), [MOS-1315](//mosipid.atlassian.net/browse/MOS-1315), [MOS-1316](//mosipid.atlassian.net/browse/MOS-1316) |
|22.|Notification| Acknowledgement and Notifications | REG_FR_4.4| [MOS-1303](//mosipid.atlassian.net/browse/MOS-1303), [MOS-1195](//mosipid.atlassian.net/browse/MOS-1195), [MOS-12989](//mosipid.atlassian.net/browse/MOS-12989) |
|23.|New Registration| Biometric Exceptions  | REG_FR_4.6| [MOS-19011](//mosipid.atlassian.net/browse/MOS-19011), [MOS-15999](//mosipid.atlassian.net/browse/MOS-15999), [MOS-16109](//mosipid.atlassian.net/browse/MOS-16109), [MOS-1292](//mosipid.atlassian.net/browse/MOS-1292), [MOS-21920](//mosipid.atlassian.net/browse/MOS-21920), [MOS-21897](//mosipid.atlassian.net/browse/MOS-21897), [MOS-21888](//mosipid.atlassian.net/browse/MOS-21888)|
|24.|Authentication| Biometric Exceptions  | REG_FR_4.6| [MOS-13659](//mosipid.atlassian.net/browse/MOS-13659) |
|25.|Finger Print Capture| Biometric Exceptions  | REG_FR_4.6| [MOS-1184](//mosipid.atlassian.net/browse/MOS-1184) |
|26.|Authentication| Operator and Supervisor Approval | REG_FR_4.7| [MOS-13523](//mosipid.atlassian.net/browse/MOS-13523), [MOS-1310](//mosipid.atlassian.net/browse/MOS-1310), [MOS-1307](//mosipid.atlassian.net/browse/MOS-1307), [MOS-1320](//mosipid.atlassian.net/browse/MOS-1320)  |
|27.|User Onboarding| User On-boarding | REG_FR_1.1| [MOS-19001](//mosipid.atlassian.net/browse/MOS-19001), [MOS-1330](//mosipid.atlassian.net/browse/MOS-1330), [MOS-1206](//mosipid.atlassian.net/browse/MOS-1206), [MOS-1012](//mosipid.atlassian.net/browse/MOS-1012), [MOS-1011](//mosipid.atlassian.net/browse/MOS-1011), [MOS-1010](//mosipid.atlassian.net/browse/MOS-1010), [MOS-1009](//mosipid.atlassian.net/browse/MOS-1009), [MOS-1008](//mosipid.atlassian.net/browse/MOS-1008),  [MOS-1006](//mosipid.atlassian.net/browse/MOS-1006), [MOS-22161](//mosipid.atlassian.net/browse/MOS-22161), [MOS-22005](//mosipid.atlassian.net/browse/MOS-22005), [MOS-22001](//mosipid.atlassian.net/browse/MOS-22001), [MOS-22000](//mosipid.atlassian.net/browse/MOS-22000), [MOS-21999](//mosipid.atlassian.net/browse/MOS-21999), [MOS-21998](//mosipid.atlassian.net/browse/MOS-21998)|
|28.|Authentication| Login/Authentication  | REG_FR_1.2| [MOS-18483](//mosipid.atlassian.net/browse/MOS-18483), [MOS-16809](//mosipid.atlassian.net/browse/MOS-16809), [MOS-15833](//mosipid.atlassian.net/browse/MOS-15833) |
|29.|New Registration| User On-boarding | REG_FR_1.1| [MOS-16829](//mosipid.atlassian.net/browse/MOS-16829) |
|30.|Login| User On-boarding | REG_FR_1.1| [MOS-16040](//mosipid.atlassian.net/browse/MOS-16040), [MOS-12199](//mosipid.atlassian.net/browse/MOS-12199), [MOS-12185](//mosipid.atlassian.net/browse/MOS-12185), [MOS-12135](//mosipid.atlassian.net/browse/MOS-12135), [MOS-12118](//mosipid.atlassian.net/browse/MOS-12118), [MOS-8368](//mosipid.atlassian.net/browse/MOS-8368), [MOS-1186](//mosipid.atlassian.net/browse/MOS-1186), [MOS-553](//mosipid.atlassian.net/browse/MOS-553) |
|31.|RC Setup & Update | User On-boarding | REG_FR_1.1| [MOS-14225](//mosipid.atlassian.net/browse/MOS-14225), [MOS-13179](//mosipid.atlassian.net/browse/MOS-13179), [MOS-9054](//mosipid.atlassian.net/browse/MOS-9054) |
|32.|Authorization | User On-boarding | REG_FR_1.1| [MOS-1111](//mosipid.atlassian.net/browse/MOS-1111) |
|33.|Logout| Logout | REG_FR_1.3| [MOS-563](//mosipid.atlassian.net/browse/MOS-563) |
|34.|New Registration| Login/Authentication | REG_FR_1.2| [MOS-16798](//mosipid.atlassian.net/browse/MOS-16798) |
|35.|Login| Login/Authentication  | REG_FR_1.2| [MOS-12135](//mosipid.atlassian.net/browse/MOS-12135), [MOS-553](//mosipid.atlassian.net/browse/MOS-553), [MOS-12118](//mosipid.atlassian.net/browse/MOS-12118), [MOS-8368](//mosipid.atlassian.net/browse/MOS-8368) |
|36.|Authentication| Login/Authentication| REG_FR_1.2| [MOS-1334](//mosipid.atlassian.net/browse/MOS-1334), [MOS-1301](//mosipid.atlassian.net/browse/MOS-1301), [MOS-1175](//mosipid.atlassian.net/browse/MOS-1175) |
|37.|Packet exporter| Login/Authentication  | REG_FR_1.2| [MOS-1317](//mosipid.atlassian.net/browse/MOS-1317) |
|38.|Security Scan| Key Management  | REG_FR_9.1| [MOS-18150](//mosipid.atlassian.net/browse/MOS-18150) |
|39.|New Registration| Key Management  | REG_FR_9.1| [MOS-15112](//mosipid.atlassian.net/browse/MOS-15112) |
|40.|Sync| Key Management  | REG_FR_9.1| [MOS-13665](//mosipid.atlassian.net/browse/MOS-13665),[MOS-11696](//mosipid.atlassian.net/browse/MOS-11696), [MOS-1244](//mosipid.atlassian.net/browse/MOS-1244), [MOS-22148](//mosipid.atlassian.net/browse/MOS-22148)|
|41.|RC Setup & Update| Business validations | REG_FR_5.11| [MOS-19006](//mosipid.atlassian.net/browse/MOS-19006) |
|43.|EOD Process| End of day process | REG_FR_4.8| [MOS-12867](//mosipid.atlassian.net/browse/MOS-12867), [MOS-12874](//mosipid.atlassian.net/browse/MOS-12874) |
|44.|Packet Creation | New Registration | REG_FR_4.1| [MOS-12112](//mosipid.atlassian.net/browse/MOS-12112) |
|45.|Login| Login/Authentication  | REG_FR_1.2| [MOS-11661](//mosipid.atlassian.net/browse/MOS-11661) |
|47.|New registration| New Registration | REG_FR_4.1| [MOS-10406](//mosipid.atlassian.net/browse/MOS-10406), [MOS-13624](//mosipid.atlassian.net/browse/MOS-13624), [MOS-12187](//mosipid.atlassian.net/browse/MOS-12187), [MOS-12167](//mosipid.atlassian.net/browse/MOS-12167), [MOS-11750](//mosipid.atlassian.net/browse/MOS-11750), [MOS-11732](//mosipid.atlassian.net/browse/MOS-11732), [MOS-11678](//mosipid.atlassian.net/browse/MOS-11678), [MOS-10408](//mosipid.atlassian.net/browse/MOS-10408), [MOS-1015](//mosipid.atlassian.net/browse/MOS-1015), [MOS-1018](//mosipid.atlassian.net/browse/MOS-1018), [MOS-554](//mosipid.atlassian.net/browse/MOS-554), [MOS-236](//mosipid.atlassian.net/browse/MOS-236) |
|48.|Device onboarding|  Master data Sync | REG_FR_2.1| [MOS-11597](//mosipid.atlassian.net/browse/MOS-11597) |
|49.|New registration|  Pre-registration Data download| REG_FR_2.5| [MOS-16784](//mosipid.atlassian.net/browse/MOS-16784) |
|50.|New registration|  New Registration | REG_FR_4.1| [MOS-11597](//mosipid.atlassian.net/browse/MOS-11597) |
|51.|Sync|  Registration Data | REG_FR_5.14| [MOS-16544](//mosipid.atlassian.net/browse/MOS-16544), [MOS-8641](//mosipid.atlassian.net/browse/MOS-8641), [MOS-8942](//mosipid.atlassian.net/browse/MOS-8942), [MOS-8572](//mosipid.atlassian.net/browse/MOS-8572), [MOS-1381](//mosipid.atlassian.net/browse/MOS-1381), [MOS-1014](//mosipid.atlassian.net/browse/MOS-1014), [MOS-1013](//mosipid.atlassian.net/browse/MOS-1013)  |
|52.|EoD process| Analytics and Audit Logs  | REG_FR_8| [MOS-16712](//mosipid.atlassian.net/browse/MOS-16712) |
|53.|Security Scan| Analytics and Audit Logs  | REG_FR_8| [MOS-15832](//mosipid.atlassian.net/browse/MOS-15832) |
|54.|Sync|  Analytics and Audit Logs  | REG_FR_8| [MOS-13184](//mosipid.atlassian.net/browse/MOS-13184), [MOS-11597](//mosipid.atlassian.net/browse/MOS-11597) |
|55.|Packet Creation| Analytics and Audit Logs  | REG_FR_8| [MOS-8761](//mosipid.atlassian.net/browse/MOS-8761) |
|56.|New Registration| Peripherals Check   | REG_FR_3.1| [MOS-11612](//mosipid.atlassian.net/browse/MOS-11612), [MOS-10407](//mosipid.atlassian.net/browse/MOS-10407), [MOS-1219](//mosipid.atlassian.net/browse/MOS-1219), |
|57.|RC Setup & Update| Software Version Upgrade   | REG_FR_10| [MOS-13527](//mosipid.atlassian.net/browse/MOS-13527), [MOS-67](//mosipid.atlassian.net/browse/MOS-67)  |
|58.|New Registration| Data retention policies  | REG_FR_11.1| [MOS-12167](//mosipid.atlassian.net/browse/MOS-12167)  |
|59.|Sync| Data retention policies | REG_FR_11.1| [MOS-12083](//mosipid.atlassian.net/browse/MOS-12083), [MOS-8942](//mosipid.atlassian.net/browse/MOS-8942), [MOS-8641](//mosipid.atlassian.net/browse/MOS-8641), [MOS-8572](//mosipid.atlassian.net/browse/MOS-8572), [MOS-1381](//mosipid.atlassian.net/browse/MOS-1381), [MOS-1338](//mosipid.atlassian.net/browse/MOS-1338), [MOS-18089](//mosipid.atlassian.net/browse/MOS-18089) |
|60.|Data Clean-Up|  Machine Retirement    | REG_FR_11.2| [MOS-13698](//mosipid.atlassian.net/browse/MOS-13698)  |
|61.|New Registration|  Machine retirement | REG_FR_11.2| [MOS-10555](//mosipid.atlassian.net/browse/MOS-10555) , [MOS-1300](//mosipid.atlassian.net/browse/MOS-1300) |
|62.|New Registration| Transliteration | REG_FR_6.2| [MOS-15107](//mosipid.atlassian.net/browse/MOS-15107), [MOS-21863](//mosipid.atlassian.net/browse/MOS-21863) |
|63.|Transliteration |  Transliteration | REG_FR_6.2| [MOS-1293](//mosipid.atlassian.net/browse/MOS-1293), [MOS-1288](//mosipid.atlassian.net/browse/MOS-1288)  |
|64.|New registration|  Transliteration  | REG_FR_6.2| [MOS-21863](//mosipid.atlassian.net/browse/MOS-21863), [MOS-10410](//mosipid.atlassian.net/browse/MOS-10410)  |
|65.|Translation |  Translation | REG_FR_6.1| [MOS-1202](//mosipid.atlassian.net/browse/MOS-1202)  |
|66.|New Registration | New Registration  | REG_FR_4.1| [MOS-15107](//mosipid.atlassian.net/browse/MOS-15107)  |
|67.|Disk space checker |  Disk space check | REG_FR_3.2| [MOS-336](//mosipid.atlassian.net/browse/MOS-336)  |
|68.|New Registration |  Peripherals Check | REG_FR_3.1| [MOS-8694](//mosipid.atlassian.net/browse/MOS-8694)  |
|69.|Security Scan |   Virus Scan/ Security Scan | REG_FR_3.3| [MOS-13526](//mosipid.atlassian.net/browse/MOS-13526)  |
|71.|VDM |  Biometric Capture (SDK Integration, Extract and Match) | REG_FR_5.4| [MOS-16121](//mosipid.atlassian.net/browse/MOS-16121), [MOS-13075](//mosipid.atlassian.net/browse/MOS-13075), [MOS-22410](//mosipid.atlassian.net/browse/MOS-22410), [MOS-23070](//mosipid.atlassian.net/browse/MOS-23070)|
|72.|Device Onboarding|  Biometric Capture (SDK Integration, Extract and Match) | REG_FR_4.5| [MOS-1309](//mosipid.atlassian.net/browse/MOS-1309),    [MOS-1275](//mosipid.atlassian.net/browse/MOS-1275), [MOS-1226](//mosipid.atlassian.net/browse/MOS-1226), [MOS-1224](//mosipid.atlassian.net/browse/MOS-1224) |
|73.|New Registration | Biometric Capture (SDK Integration, Extract and Match) | REG_FR_4.5| [MOS-10409](//mosipid.atlassian.net/browse/MOS-10409), [MOS-1325](//mosipid.atlassian.net/browse/MOS-1325), [MOS-1331](//mosipid.atlassian.net/browse/MOS-1331), [MOS-16024](//mosipid.atlassian.net/browse/MOS-16024), [MOS-16008](//mosipid.atlassian.net/browse/MOS-16008), [MOS-16016](//mosipid.atlassian.net/browse/MOS-16016), [MOS-1302](//mosipid.atlassian.net/browse/MOS-1302), [MOS-1291](//mosipid.atlassian.net/browse/MOS-1291), [MOS-1287](//mosipid.atlassian.net/browse/MOS-1287), [MOS-1285](//mosipid.atlassian.net/browse/MOS-1285), [MOS-1342](//mosipid.atlassian.net/browse/MOS-1342), [MOS-13522](//mosipid.atlassian.net/browse/MOS-13522), [MOS-1205](//mosipid.atlassian.net/browse/MOS-1205), [MOS-1177](//mosipid.atlassian.net/browse/MOS-1177) |
|74.|Face capture|  Biometric Capture (SDK Integration, Extract and Match) | REG_FR_4.5| [MOS-1252](//mosipid.atlassian.net/browse/MOS-1252) |
|75.|Device Onboarding| Biometric Capture (SDK Integration, Extract and Match) | REG_FR_4.5| [MOS-1226](//mosipid.atlassian.net/browse/MOS-1226),    [MOS-1224](//mosipid.atlassian.net/browse/MOS-1224) |
|76.|Security|  Database | REG_FR_5.5| [MOS-8726](//mosipid.atlassian.net/browse/MOS-8726) |
|77.|RC Setup & Update|  Database  | REG_FR_5.5| [MOS-8710](//mosipid.atlassian.net/browse/MOS-8710) |
|78.|RC Setup & Update|  File system | REG_FR_5.6| [MOS-16120](//mosipid.atlassian.net/browse/MOS-16120), [MOS-13174](//mosipid.atlassian.net/browse/MOS-13174), [MOS-12088](//mosipid.atlassian.net/browse/MOS-12088), [MOS-13527](//mosipid.atlassian.net/browse/MOS-13527), [MOS-8710](//mosipid.atlassian.net/browse/MOS-8710), [MOS-14](//mosipid.atlassian.net/browse/MOS-14), [MOS-61](//mosipid.atlassian.net/browse/MOS-61) |
|79.|Packet creation| File system    | REG_FR_5.6| [MOS-11628](//mosipid.atlassian.net/browse/MOS-11628) |
|80.|Acknowledgement|  Encryption and Decryption   | REG_FR_5.8| [MOS-15835](//mosipid.atlassian.net/browse/MOS-15835) |
|81.|Sync|  Encryption and Decryption    | REG_FR_5.8| [MOS-11696](//mosipid.atlassian.net/browse/MOS-11696),[MOS-21461](//mosipid.atlassian.net/browse/MOS-21461), [MOS-1343](//mosipid.atlassian.net/browse/MOS-1343)  |
|82.|Security|  Encryption and Decryption   | REG_FR_5.8| [MOS-8726](//mosipid.atlassian.net/browse/MOS-8726) |
|83.|Packet creation|  Encryption and Decryption  | REG_FR_5.8| [MOS-65](//mosipid.atlassian.net/browse/MOS-65), [MOS-21573](//mosipid.atlassian.net/browse/MOS-21573), [MOS-8658](//mosipid.atlassian.net/browse/MOS-8658), [MOS-561](//mosipid.atlassian.net/browse/MOS-561) |
|84.|RC Setup & Update| Storage Policies  | REG_FR_5.9| [MOS-11784](//mosipid.atlassian.net/browse/MOS-11784) |
|85.|Packet Creation|  Storage Policies  | REG_FR_5.9| [MOS-65](//mosipid.atlassian.net/browse/MOS-65) |
|86.|UIN Update|  Registration Client UI  | REG_FR_6| [MOS-14999](//mosipid.atlassian.net/browse/MOS-14999) |
|87.|New Registration|  Registration Client UI  | REG_FR_6| [MOS-13080](//mosipid.atlassian.net/browse/MOS-13080), [MOS-11678](//mosipid.atlassian.net/browse/MOS-11678), [MOS-21873](//mosipid.atlassian.net/browse/MOS-21873),[MOS-8742](//mosipid.atlassian.net/browse/MOS-8742), [MOS-11713](//mosipid.atlassian.net/browse/MOS-11713), [MOS-21870](//mosipid.atlassian.net/browse/MOS-21870),  [MOS-21860](//mosipid.atlassian.net/browse/MOS-21860), [MOS-15324](//mosipid.atlassian.net/browse/MOS-15324), [MOS-22011](//mosipid.atlassian.net/browse/MOS-22011), [MOS-21923](//mosipid.atlassian.net/browse/MOS-21923), [MOS-21922](//mosipid.atlassian.net/browse/MOS-21922), [MOS-21921](//mosipid.atlassian.net/browse/MOS-21921), [MOS-21920](//mosipid.atlassian.net/browse/MOS-21920), [MOS-21897](//mosipid.atlassian.net/browse/MOS-21897), [MOS-21888](//mosipid.atlassian.net/browse/MOS-21888), [MOS-21887](//mosipid.atlassian.net/browse/MOS-21887), [MOS-21873](//mosipid.atlassian.net/browse/MOS-21873)|
|88.|Authentication| Login/Authentication| REG_FR_4.2| [MOS-21523](//mosipid.atlassian.net/browse/MOS-21523)|
|89.|Acknowledgement|Registration Client UI|REG_FR_6|[MOS-21926](//mosipid.atlassian.net/browse/MOS-21926)|
|90.|EoD Process|Registration Client UI|REG_FR_6|[MOS-22010](//mosipid.atlassian.net/browse/MOS-22010), [MOS-22008](//mosipid.atlassian.net/browse/MOS-22008), [MOS-22007](//mosipid.atlassian.net/browse/MOS-22007), [MOS-22006](//mosipid.atlassian.net/browse/MOS-22006), [MOS-21928](//mosipid.atlassian.net/browse/MOS-21928)|
|91.|Login|Login/Authentication|REG_FR_4.2|[MOS-21996](//mosipid.atlassian.net/browse/MOS-21996), [MOS-21997](//mosipid.atlassian.net/browse/MOS-21997)|
|92.|Packet Creation|Registration Data|REG_FR_5.14|[MOS-22381](//mosipid.atlassian.net/browse/MOS-22381)|
|93.|Packet Exporter|Registration Client UI|REG_FR_6|[MOS-22013](//mosipid.atlassian.net/browse/MOS-22013), [MOS-22012](//mosipid.atlassian.net/browse/MOS-22012)|
|94.|Security|Key Management|REG_FR_5.10|[MOS-22405](//mosipid.atlassian.net/browse/MOS-22405)|
|95.|Security|Master Data|REG_FR_5.12|[MOS-22397](//mosipid.atlassian.net/browse/MOS-22397)|
|96.|Security|Login/Authentication|REG_FR_4.2|[MOS-22397](//mosipid.atlassian.net/browse/MOS-22397)|
|97.|User Onboarding|Registration Client UI|REG_FR_6|[MOS-22005](//mosipid.atlassian.net/browse/MOS-22005), [MOS-22001](//mosipid.atlassian.net/browse/MOS-22001), [MOS-21999](//mosipid.atlassian.net/browse/MOS-21999)|
|98.|Device Onboarding|Peripherals check|REG_FR_5.27|[MOS-15996](//mosipid.atlassian.net/browse/MOS-15996) |


## 10. Registration Processor: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1. | | New UIN Issuance| RPR_FR_1.1| [NA](//mosipid.atlassian.net/browse/NA)
|2. | uin-update-stage| UIN Update| RPR_FR_1.2| [MOS-13211](//mosipid.atlassian.net/browse/MOS-13211), [MOS-13210](//mosipid.atlassian.net/browse/MOS-13210), [MOS-12924](//mosipid.atlassian.net/browse/MOS-12924)
|3. | uin-update-stage| De-activate UIN – Manual/Automated| RPR_FR_1.3| [MOS-1086](//mosipid.atlassian.net/browse/MOS-1086), [MOS-1085](//mosipid.atlassian.net/browse/MOS-1085)
|4. | uin-update-stage| Re-activate UIN| RPR_FR_1.4| [MOS-1087](//mosipid.atlassian.net/browse/MOS-1087)
|5. | registration-processor-camel-bridge| Orchestration| RPR_FR_2.1| [MOS-10727](//mosipid.atlassian.net/browse/MOS-10727), [MOS-12568](//mosipid.atlassian.net/browse/MOS-12568), [MOS-17609](//mosipid.atlassian.net/browse/MOS-17609), [MOS-15017](//mosipid.atlassian.net/browse/MOS-15017)
|6. | reprocess-stage| Retry Processing (In case of exceptions/failures)| RPR_FR_2.2| [MOS-8225](//mosipid.atlassian.net/browse/MOS-8225)
|7. | reprocess-stage| Resume Workflow| RPR_FR_2.3| [MOS-13197](//mosipid.atlassian.net/browse/MOS-13197)
|8. | | Integration (System capability)| RPR_FR_2.4| 
|9. | | Workflow Customization (Ability to plug-in/exclude stages)| RPR_FR_2.5| 
|10. | | Multiple Workflows (Specific to lifecycle – E.G.: New vs. Update, Activation vs. Deactivation, Applicant Type specific workflow)| RPR_FR_2.6| 
|11. | | Scalability and Throughput| RPR_FR_2.7| 
|12. | packet-receiver-stage| Sanity Check| RPR_FR_3.1| [MOS-44](//mosipid.atlassian.net/browse/MOS-44), [MOS-45](//mosipid.atlassian.net/browse/MOS-45), [MOS-46](//mosipid.atlassian.net/browse/MOS-46), [MOS-1031](//mosipid.atlassian.net/browse/MOS-1031), [MOS-21712 (CheckSum Validation)](//https://mosipid.atlassian.net/browse/MOS-21712), [MOS-21715 (Virus Scan)](//mosipid.atlassian.net/browse/MOS-21715)
|13. | virus-scanner-stage| Virus Scan| RPR_FR_3.2| [MOS-21715 (DMZ Virus Scan)](//mosipid.atlassian.net/browse/MOS-21715), [MOS-21716 (Secure Virus Scan)](//mosipid.atlassian.net/browse/MOS-21716)
|14. | | Source Authentication| RPR_FR_3.3| 
|15. | osi-validator-stage| Machine-User-Center Mapping Check| RPR_FR_3.4| [MOS-240 (Machine Validation)](//mosipid.atlassian.net/browse/MOS-240), [MOS-12831 (Device Validation)](//mosipid.atlassian.net/browse/MOS-12831)
|16. | osi-validator-stage| GPS Capture Check| RPR_FR_3.5| [MOS-240 (Machine Validation - Has GPS)](//mosipid.atlassian.net/browse/MOS-240)
|17. | osi-validator-stage| Operator & Supervisor Validation| RPR_FR_3.6| [MOS-1088](//mosipid.atlassian.net/browse/MOS-1088), [MOS-9129](//mosipid.atlassian.net/browse/MOS-9129), [MOS-246](//mosipid.atlassian.net/browse/MOS-246), [MOS-245](//mosipid.atlassian.net/browse/MOS-245), [MOS-241](//mosipid.atlassian.net/browse/MOS-241), [MOS-14589](//mosipid.atlassian.net/browse/MOS-14589), [MOS-242](//mosipid.atlassian.net/browse/MOS-242), [MOS-17805](//mosipid.atlassian.net/browse/MOS-17805)
|18. | quality-matchness-checker-stage| Data Quality Check: Photo, Age, Gender Data Check| RPR_FR_3.7| [MOS-1082](//mosipid.atlassian.net/browse/MOS-1082)
|19. | quality-matchness-checker-stage| Biometrics Quality Check| RPR_FR_3.8| [MOS-1093](//mosipid.atlassian.net/browse/MOS-1093), [MOS-1091](//mosipid.atlassian.net/browse/MOS-1091), [MOS-1084](//mosipid.atlassian.net/browse/MOS-1084), [MOS-17610](//mosipid.atlassian.net/browse/MOS-17610), [MOS-8460](//mosipid.atlassian.net/browse/MOS-8460)
|20. | quality-matchness-checker-stage| Doc. Validation - OCR| RPR_FR_3.9| [MOS-1081](//mosipid.atlassian.net/browse/MOS-1081)
|21. | quality-matchness-checker-stage| File & Document Validation| RPR_FR_3.10| [MOS-226](//mosipid.atlassian.net/browse/MOS-226), [MOS-48](//mosipid.atlassian.net/browse/MOS-48), [MOS-13138](//mosipid.atlassian.net/browse/MOS-13138)
|22. | osi-validator-stage| Introducer Validation| RPR_FR_3.11| [MOS-1088](//mosipid.atlassian.net/browse/MOS-1088), [MOS-9129](//mosipid.atlassian.net/browse/MOS-9129), [MOS-246](//mosipid.atlassian.net/browse/MOS-246), [MOS-245](//mosipid.atlassian.net/browse/MOS-245), [MOS-17805](//mosipid.atlassian.net/browse/MOS-17805)
|23. | demo-dedupe-stage, bio-dedupe-stage, packet-bio-dedupe-service| Deduplication – Demographic, Biometrics| RPR_FR_3.12| [MOS-1094](//mosipid.atlassian.net/browse/MOS-1094), [MOS-1079](//mosipid.atlassian.net/browse/MOS-1079), [MOS-1064](//mosipid.atlassian.net/browse/MOS-1064), [MOS-1096](//mosipid.atlassian.net/browse/MOS-1096), [MOS-1095](//mosipid.atlassian.net/browse/MOS-1095), [MOS-9343](//mosipid.atlassian.net/browse/MOS-9343), [MOS-9342](//mosipid.atlassian.net/browse/MOS-9342), [MOS-9341](//mosipid.atlassian.net/browse/MOS-9341), [MOS-11897](//mosipid.atlassian.net/browse/MOS-11897)
|24. | | Data Verification (Pluggable by SI – Not part of MOSIP)| RPR_FR_3.13| 
|25. | | Data Enrichment (Incl. receipt of Update Packet from ext. system and process thereafter, in terms of MOSIP’s capability)| RPR_FR_3.14| 
|26. | | Manual Verification for ext. system data update (Pluggable by SI)| RPR_FR_3.15| 
|27. | manual-verification-stage| Manual Adjudication (Pluggable by SI)| RPR_FR_3.16| [MOS-1078](//mosipid.atlassian.net/browse/MOS-1078), [MOS-1077](//mosipid.atlassian.net/browse/MOS-1077), [MOS-1076](//mosipid.atlassian.net/browse/MOS-1076), [MOS-16105](//mosipid.atlassian.net/browse/MOS-16105)
|28. | registration-processor-abis| ABIS Integration (Incl. ABIS Middleware)| RPR_FR_3.17| [MOS-1097](//mosipid.atlassian.net/browse/MOS-1097), [MOS-13141](//mosipid.atlassian.net/browse/MOS-13141), [MOS-13140](//mosipid.atlassian.net/browse/MOS-13140)
|29. | uin-generator-stage| Identity Generation (Refer to UIN Generation service) – Incl. UIN Generation and UIN association| RPR_FR_3.18| [MOS-1065](//mosipid.atlassian.net/browse/MOS-1065), [MOS-19000](//mosipid.atlassian.net/browse/MOS-19000)
|30. | uin-generator-stage| Store/Update ID Repository (Refer to ID-Auth)| RPR_FR_3.19| [MOS-1067](//mosipid.atlassian.net/browse/MOS-1067), [MOS-1089](//mosipid.atlassian.net/browse/MOS-1089)
|31. | | Capture Audit Trails/Analytics Data| RPR_FR_3.20| [MOS-719](//mosipid.atlassian.net/browse/MOS-719), [MOS-9597](//mosipid.atlassian.net/browse/MOS-9597), [MOS-8367](//mosipid.atlassian.net/browse/MOS-8367), [MOS-13198](//mosipid.atlassian.net/browse/MOS-13198)
|32. | message-sender-stage| Notification (Pluggable by SI)| RPR_FR_3.21| [MOS-10783](//mosipid.atlassian.net/browse/MOS-10783), [MOS-1069](//mosipid.atlassian.net/browse/MOS-1069), [MOS-1068](//mosipid.atlassian.net/browse/MOS-1068), [MOS-12007](//mosipid.atlassian.net/browse/MOS-12007), [MOS-11962](//mosipid.atlassian.net/browse/MOS-11962), [MOS-13967](//mosipid.atlassian.net/browse/MOS-13967), [MOS-14595](//mosipid.atlassian.net/browse/MOS-14595), [MOS-1066](//mosipid.atlassian.net/browse/MOS-1066)
|33. | printing-stage| Print & Post (Pluggable by SI)| RPR_FR_3.22| [MOS-14596](//mosipid.atlassian.net/browse/MOS-14596), [MOS-14582](//mosipid.atlassian.net/browse/MOS-14582), [MOS-16107](//mosipid.atlassian.net/browse/MOS-16107), [MOS-15021](//mosipid.atlassian.net/browse/MOS-15021), [MOS-1071](//mosipid.atlassian.net/browse/MOS-1071)
|34. | | Data Seeding to External Functional ID System (Pluggable by SI)| RPR_FR_3.23| 


## 11. Authentication: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|Biometric Authenticator|Biometric Authentication |IDA_FR_1.1|[MOS-1155](//mosipid.atlassian.net/browse/MOS-1155), [MOS-1145](//mosipid.atlassian.net/browse/MOS-1145), [MOS-18108](//mosipid.atlassian.net/browse/MOS-18108), [MOS-12073](//mosipid.atlassian.net/browse/MOS-12073), [MOS-12072](//mosipid.atlassian.net/browse/MOS-12072), [MOS-10831](//mosipid.atlassian.net/browse/MOS-10831), [MOS-10308](//mosipid.atlassian.net/browse/MOS-10308), [MOS-1150](//mosipid.atlassian.net/browse/MOS-1150), [MOS-1149](//mosipid.atlassian.net/browse/MOS-1149), [MOS-1146](//mosipid.atlassian.net/browse/MOS-1146), [MOS-1411](//mosipid.atlassian.net/browse/MOS-1411), [MOS-1154](//mosipid.atlassian.net/browse/MOS-1154), [MOS-1133](//mosipid.atlassian.net/browse/MOS-1133), [MOS-1417](//mosipid.atlassian.net/browse/MOS-1417)|
|2.|Demographic Authenticator|Demographic Authentication |IDA_FR_1.2|[MOS-13162](//mosipid.atlassian.net/browse/MOS-13162), [MOS-1114](//mosipid.atlassian.net/browse/MOS-1114), [MOS-584](//mosipid.atlassian.net/browse/MOS-584), [MOS-231](//mosipid.atlassian.net/browse/MOS-231), [MOS-230](//mosipid.atlassian.net/browse/MOS-230), [MOS-223](//mosipid.atlassian.net/browse/MOS-223), [MOS-212](//mosipid.atlassian.net/browse/MOS-212), [MOS-208](//mosipid.atlassian.net/browse/MOS-208), [MOS-207](//mosipid.atlassian.net/browse/MOS-207), [MOS-233](//mosipid.atlassian.net/browse/MOS-233), [MOS-232](//mosipid.atlassian.net/browse/MOS-232), [MOS-8437](//mosipid.atlassian.net/browse/MOS-8437), [MOS-8369](//mosipid.atlassian.net/browse/MOS-8369), [MOS-21585](//mosipid.atlassian.net/browse/MOS-21585)|
|3.|OTP Authenticator|OTP Authentication |IDA_FR_1.3|[MOS-17444](//mosipid.atlassian.net/browse/MOS-17444), [MOS-224](//mosipid.atlassian.net/browse/MOS-224), [MOS-42](//mosipid.atlassian.net/browse/MOS-42), [MOS-41](//mosipid.atlassian.net/browse/MOS-41), [MOS-27](//mosipid.atlassian.net/browse/MOS-27), [MOS-1415](//mosipid.atlassian.net/browse/MOS-1415), [MOS-8420](//mosipid.atlassian.net/browse/MOS-8420), [MOS-1418](//mosipid.atlassian.net/browse/MOS-1418) |
|4.|Static Pin Authenticator|Static PIN Authentication-Descoped |IDA_FR_1.4|[MOS-13674](//mosipid.atlassian.net/browse/MOS-13674), [MOS-1142](//mosipid.atlassian.net/browse/MOS-1142), [MOS-1422](//mosipid.atlassian.net/browse/MOS-1422), [MOS-1414](//mosipid.atlassian.net/browse/MOS-1414), [MOS-1140](//mosipid.atlassian.net/browse/MOS-1140)|
|5.|Multi-factor Authenticator|Multi-factor Authentication |IDA_FR_2|[MOS-13664](//mosipid.atlassian.net/browse/MOS-13664), [MOS-1117](//mosipid.atlassian.net/browse/MOS-1117), [MOS-13](//mosipid.atlassian.net/browse/MOS-13), [MOS-11](//mosipid.atlassian.net/browse/MOS-11), [MOS-17407](//mosipid.atlassian.net/browse/MOS-17407), [MOS-1124](//mosipid.atlassian.net/browse/MOS-1124), [MOS-8403](//mosipid.atlassian.net/browse/MOS-8403), [MOS-1148](//mosipid.atlassian.net/browse/MOS-1148), [MOS-1134](//mosipid.atlassian.net/browse/MOS-1134), [MOS-1423](//mosipid.atlassian.net/browse/MOS-1423), [MOS-12231](//mosipid.atlassian.net/browse/MOS-12231), [MOS-13299](//mosipid.atlassian.net/browse/MOS-13299), [MOS-8386](//mosipid.atlassian.net/browse/MOS-8386), [MOS-1420](//mosipid.atlassian.net/browse/MOS-1420), [MOS-1153](//mosipid.atlassian.net/browse/MOS-1153), [MOS-18214](//mosipid.atlassian.net/browse/MOS-18214), [MOS-22933](//mosipid.atlassian.net/browse/MOS-22933),[MOS-22932](//mosipid.atlassian.net/browse/MOS-22932), [MOS-22931](//mosipid.atlassian.net/browse/MOS-22931), [MOS-22930](//mosipid.atlassian.net/browse/MOS-22930), [MOS-22929](//mosipid.atlassian.net/browse/MOS-22929), [MOS-21583](//mosipid.atlassian.net/browse/MOS-21583), [MOS-21326](//mosipid.atlassian.net/browse/MOS-21326), [MOS-21327](//mosipid.atlassian.net/browse/MOS-21327), [MOS-18215](//mosipid.atlassian.net/browse/MOS-18215), [MOS-21757](//mosipid.atlassian.net/browse/MOS-21757)NFRS [MOS-1156](//mosipid.atlassian.net/browse/MOS-1156), [MOS-1144](//mosipid.atlassian.net/browse/MOS-1144), [MOS-1143](//mosipid.atlassian.net/browse/MOS-1143), [MOS-1141](//mosipid.atlassian.net/browse/MOS-1141), [MOS-1139](//mosipid.atlassian.net/browse/MOS-1139), [MOS-1136](//mosipid.atlassian.net/browse/MOS-1136), [MOS-1132](//mosipid.atlassian.net/browse/MOS-1132), [MOS-1131](//mosipid.atlassian.net/browse/MOS-1131), [MOS-1128](//mosipid.atlassian.net/browse/MOS-1128), [MOS-1126](//mosipid.atlassian.net/browse/MOS-1126), [MOS-1125](//mosipid.atlassian.net/browse/MOS-1125), [MOS-1121](//mosipid.atlassian.net/browse/MOS-1121), [MOS-1118](//mosipid.atlassian.net/browse/MOS-1118), [MOS-1116](//mosipid.atlassian.net/browse/MOS-1116), [MOS-1421](//mosipid.atlassian.net/browse/MOS-1421)|
|6.|To be Planned-V2|QR Code based Authentication |IDA_FR_3.1||
|7.|eKYC Authenticator|eKYC Authentication |IDA_FR_4.1|[MOS-13161](//mosipid.atlassian.net/browse/MOS-13161), [MOS-1119](//mosipid.atlassian.net/browse/MOS-1119), [MOS-10165](//mosipid.atlassian.net/browse/MOS-10165), [MOS-12241](//mosipid.atlassian.net/browse/MOS-12241), [MOS-13963](//mosipid.atlassian.net/browse/MOS-13963), [MOS-21038](//mosipid.atlassian.net/browse/MOS-21038) |
|8.|MPA Authenticator|MISP License Authentication |IDA_FR_5.1|[MOS-1098](//mosipid.atlassian.net/browse/MOS-1098), [MOS-13157](//mosipid.atlassian.net/browse/MOS-13157), [MOS-1099](//mosipid.atlassian.net/browse/MOS-1099)|
|9.|MPA Authenticator|Partner Policy Authentication |IDA_FR_5.2|[MOS-1129](//mosipid.atlassian.net/browse/MOS-1129), [MOS-1123](//mosipid.atlassian.net/browse/MOS-1123), [MOS-13157](//mosipid.atlassian.net/browse/MOS-13157), [MOS-13156](//mosipid.atlassian.net/browse/MOS-13156), [MOS-1099](//mosipid.atlassian.net/browse/MOS-1099) |
|10.|To be planned|Registered Devices and Open Devices |IDA_FR_6.1||

## 12. Resident Services: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|||||

## 13. Administration: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|||||

## 14. Partner Management: [**[↑]**](#table-of-content)

|**S.No.**| **Component Name**| **Feature**|**Feature ID**|**JIRA ID(s)**|
|:------:|-----|---|---|---|
|1.|||||