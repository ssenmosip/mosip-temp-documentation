**1. Kernel:**

|**S.No.**| **Component Name**| **Feature**|**JIRA ID**|
|:------:|-----|---|---|
|1.|Crypto Services|Provides services to Encrypt/Decrypt Data|[MOS-38](https://mosipid.atlassian.net/browse/MOS-38), [MOS-40](https://mosipid.atlassian.net/browse/MOS-40), [MOS-787](https://mosipid.atlassian.net/browse/MOS-787), [MOS-989](https://mosipid.atlassian.net/browse/MOS-989), [MOS-9284](https://mosipid.atlassian.net/browse/MOS-9284)|
|2.|Key Management|Provides Public/PrivateKeys throughout MOSIP for Encryption/Decryption|[MOS-789](https://mosipid.atlassian.net/browse/MOS-789), [MOS-1910](https://mosipid.atlassian.net/browse/MOS-1910), [MOS-9301](https://mosipid.atlassian.net/browse/MOS-9301), [MOS-13359](https://mosipid.atlassian.net/browse/MOS-13359)|
|3.|UIN Generation|Generates UIN|[MOS-425](https://mosipid.atlassian.net/browse/MOS-425), [MOS-9738](https://mosipid.atlassian.net/browse/MOS-9738) |
|4.|Audit Manager|Provides service across MOSIP to store Audit logs|[MOS-8](https://mosipid.atlassian.net/browse/MOS-8), [MOS-441](https://mosipid.atlassian.net/browse/MOS-441), [MOS-829](https://mosipid.atlassian.net/browse/MOS-829), [MOS-12903](https://mosipid.atlassian.net/browse/MOS-12903)|
|5.|OTP Manager|Generates and Validates OTP as per the defined policies|[MOS-33](https://mosipid.atlassian.net/browse/MOS-33), [MOS-34](https://mosipid.atlassian.net/browse/MOS-34), [MOS-35](https://mosipid.atlassian.net/browse/MOS-35), [MOS-36](https://mosipid.atlassian.net/browse/MOS-36), [MOS-423](https://mosipid.atlassian.net/browse/MOS-423), [MOS-991](https://mosipid.atlassian.net/browse/MOS-991), [MOS-1056](https://mosipid.atlassian.net/browse/MOS-1056), [MOS-1985](https://mosipid.atlassian.net/browse/MOS-1985), [MOS-5486](https://mosipid.atlassian.net/browse/MOS-5486)|
|6.|OTP Notification Service|Generates an OTP and sends Notification to a recipient|[MOS-8230](https://mosipid.atlassian.net/browse/MOS-8230)|
|7.|Email Notification|Generates and sends an Email using a third party vendor|[MOS-973](https://mosipid.atlassian.net/browse/MOS-973)|
|8.|SMS Notification|Generates and sends an SMS using a third party vendor|[MOS-961](https://mosipid.atlassian.net/browse/MOS-961)|
|9.|Key Generator|Generates Key pair for Encryption and Decryption|[MOS-788](https://mosipid.atlassian.net/browse/MOS-788), [MOS-1431](https://mosipid.atlassian.net/browse/MOS-1431)|
|10.|Data Mapper|Facilitate data mapping between DTO (Data Transfer Object) and entity|[MOS-957](https://mosipid.atlassian.net/browse/MOS-957)|
|11.|PDF Generator|This utility enables PDF file creation of received content (e.g., acknowledge and notification templates)|[MOS-960](https://mosipid.atlassian.net/browse/MOS-960), [MOS-12900](https://mosipid.atlassian.net/browse/MOS-12900)|
|12.|Template Merger|Merges a pre-configured template with dynamic values|[MOS-786](https://mosipid.atlassian.net/browse/MOS-786)|
|13.|QR Code Generator|This utility enables QR code generation for pre-registration, registration and UIN acknowledgment|[MOS-979](https://mosipid.atlassian.net/browse/MOS-979)|
|14.|Data Access Manager|Provides an implementation for DAM (Data Access Manager) interface|[MOS-31](https://mosipid.atlassian.net/browse/MOS-31), [MOS-32](https://mosipid.atlassian.net/browse/MOS-32), [MOS-14007](https://mosipid.atlassian.net/browse/MOS-14007)|
|15.|Log Manager|Enable Generation and storage of logs in a configured location|[MOS-10](https://mosipid.atlassian.net/browse/MOS-10), [MOS-39](https://mosipid.atlassian.net/browse/MOS-39), [MOS-1104](https://mosipid.atlassian.net/browse/MOS-1104), [MOS-13742](https://mosipid.atlassian.net/browse/MOS-13742)|
|16.|Static PIN Validator|Performs a pattern validation on Static PIN Validator|[MOS-12897](https://mosipid.atlassian.net/browse/MOS-12897)|
|17.|Transliteration|Performs Transliteration from one language to another|[MOS-975](https://mosipid.atlassian.net/browse/MOS-975)|
|18.|Mobile Data Validator|Performs the pattern validation on the mobile number based on the configured length|[MOS-1028](https://mosipid.atlassian.net/browse/MOS-1028)|
|19.|Email Data Validator|Performs the pattern validation on Email ID based on the configured parameters|[MOS-1029](https://mosipid.atlassian.net/browse/MOS-1029)|
|20.|UIN Validator|Performs a pattern validation on UIN|[MOS-595](https://mosipid.atlassian.net/browse/MOS-595), [MOS-9743](https://mosipid.atlassian.net/browse/MOS-9743)|
|21.|PRID Validator|Performs a pattern validation on Pre-Registration ID (PRID)|[MOS-1007](https://mosipid.atlassian.net/browse/MOS-1007), [MOS-12093](https://mosipid.atlassian.net/browse/MOS-12093)|
|22.|VID Validator|Performs a pattern validation on Virtual ID (VID)|[MOS-714](https://mosipid.atlassian.net/browse/MOS-714)|
|23.|RID Validator|Performs a pattern validation on Registration ID (RID)|[MOS-1591](https://mosipid.atlassian.net/browse/MOS-1591), [MOS-10415](https://mosipid.atlassian.net/browse/MOS-10415), [MOS-12093](https://mosipid.atlassian.net/browse/MOS-12093), [MOS-13172](https://mosipid.atlassian.net/browse/MOS-13172)|
|24.|TSP ID Validator|Performs a pattern validation on TSP ID|[MOS-1057](https://mosipid.atlassian.net/browse/MOS-1057)|
|25|MOSIP Utilities|Exception Framework, Calendar Utility, Checksum Utility, Crypto Utility, Date Utility, File Utility, Hash Utility, HMAC Utility, Json Utility, Math Utility, String Utility, UUID Utility|[MOS-9](https://mosipid.atlassian.net/browse/MOS-9), [MOS-18](https://mosipid.atlassian.net/browse/MOS-18), [MOS-19](https://mosipid.atlassian.net/browse/MOS-19), [MOS-20](https://mosipid.atlassian.net/browse/MOS-20), MOS-21, MOS-22, MOS-23, MOS-28, MOS-29, MOS-987, MOS-1986, MOS-1988, MOS-9284, MOS-65(MOS-481)|
|26.|Sync Handler|Enables Registration Client to sync Master data, List of Users, User-Role Mapping and Configurations|MOS-994, MOS-997, MOS-996, MOS-12079, MOS-12944, MOS-12945, MOS-12946, MOS-12902, MOS-12889, MOS-13945, MOS-13976, MOS-15408, MOS-16083, MOS-16110|
|27.|License Key Manager|Enables a User to Generate and Map License Keys to TSP and enables TSP to fetch permissions for a particular License Key|MOS-13094,MOS-14005|
|28.|Authorization|Enable MOSIP to Authorize requests|MOS-15402|
|29.|RID Generator|Generates Registration ID (RID)|MOS-431, MOS-5191, MOS-12082, MOS-13171|
|30.|Machine ID Generator|Generates Machine ID|MOS-9711|
|31.|Registration Center ID Generator|Generates Registration Center ID|MOS-1102|
|32.|TSP ID Generator|Generates TSP ID|MOS-1058,MOS-10220|
|33.|PRID Generator|Generates Pre-Registration ID (PRID)|MOS-735, MOS-1070, MOS-15404|
|34.|VID Generator|Generates Virtual ID (VID)|MOS-734, MOS-1070, MOS-15404|
|35.|Token ID Generator|Generates Token ID|MOS-1103, MOS-8321, MOS-12898, MOS-15404|
|36.|Master Data Management|Registration Center Type - Create/Update/Delete|MOS-539, MOS-10558,MOS-12076|
|37.|Master Data Management|Registration Center - Create/Read/Update/Delete|MOS-8220, MOS-8221, MOS-8236, MOS-8244, MOS-9529, MOS-9722, MOS-10560, MOS-11924,MOS-12076|
|38.|Master Data Management|List of Machine Types - Create|MOS-547,MOS-12076|
|39.|Master Data Management|List of Machine Specifications - Create/Update/Delete|MOS-551, MOS-10565,MOS-12076|
|40.|Master Data Management|List of Machines - Create/Read/Update/Delete|MOS-8222, MOS-8229, MOS-9723, MOS-10566,MOS-12076|
|41.|Master Data Management|Mappings of Registration Center, Machine and User Mappings - Create/Read/Delete|MOS-8232, MOS-10306, MOS-10589,MOS-12076|
|42.|Master Data Management|Create/Read/Update/Delete - Location Hierarchy|MOS-8233, MOS-8234, MOS-550, MOS-12155, MOS-13943,MOS-12076|
|43.|Master Data Management|List of Holidays - Create/Read/Update/Delete|MOS-8235, MOS-549, MOS-8565, MOS-10591,MOS-12076|
|44.|Master Data Management|Biometric Authentication Type - Create/Read|MOS-8245, MOS-9622,MOS-12076|
|45.|Master Data Management|Biometric Attirbute Type - Create/Read|MOS-8246, MOS-9623,MOS-12076|
|46.|Master Data Management|Gender - Create/Read/Update/Delete|MOS-8266, MOS-9624, MOS-988, MOS-13944,MOS-12076|
|47.|Master Data Management|Document Category - Create/Read/Update/Delete|MOS-8269, MOS-9683, MOS-10567,MOS-12076|
|48.|Master Data Management|Document Type - Create/Update/Delete|MOS-9684, MOS-10569,MOS-12076|
|49.|Master Data Management|Applicant Type-Document Category-Document Type Mapping - Read|MOS-12060, MOS-13962, MOS-12076, MOS-12068, MOS-13591|
|50.|Master Data Management|List of Devices - Create/Read/Update/Delete|MOS-8263, MOS-9695, MOS-12057,MOS-12076, MOS-10563|
|51.|Master Data Management|List of Device Specifications - Create/Read/Update/Delete|MOS-8264, MOS-9788, MOS-12076, MOS-10562|
|52.|Master Data Management|List of Device Types - Create/Update/Delete|MOS-9787, MOS-10563,MOS-12076|
|53.|Master Data Management|List of Languages - Create/Read/Update/Delete|MOS-8265, MOS-1075, MOS-10554,MOS-12076|
|54.|Master Data Management|List of Titles - Create/Read/Update/Delete|MOS-8267, MOS-9696, MOS-992,MOS-12076|
|55.|Master Data Management|Template File Format - Create/Update/Delete|MOS-9687,MOS-12076, MOS-10573|
|56.|Master Data Management|List of Template Types - Create|MOS-586,MOS-12076|
|57.|Master Data Management|List of Templates - Create/Read/Update/Delete|MOS-8271, MOS-995, MOS-10590, MOS-15461,MOS-12076|
|58.|Master Data Management|List of Blacklisted Words - Create/Read/Update/Delete|MOS-8268, MOS-9697, MOS-1054,MOS-12076|
|59.|Master Data Management|List of Reason Categories - Create|MOS-9689,MOS-12076|
|60.|Master Data Management|List of Rejection Reasons - Create/Read|MOS-8551, MOS-9690,MOS-12076|
|61.|Master Data Management|List of Applications - Create/Read|MOS-8888, MOS-9688,MOS-12076|
|62.|Master Data Management|List of ID Types - Create/Read|MOS-8247, MOS-9691,MOS-12076|
|63.|Master Data Management|Mappings of Registration Center and Machine - Create/Read/Delete|MOS-9728, MOS-9712, MOS-1053,MOS-12076|
|64.|Master Data Management|Mappings of Registration Center and Device - Create/Read/Delete|MOS-9729, MOS-9712, MOS-10561, MOS-12058,MOS-12076|
|65.|Master Data Management|Mappings of Registration Center, Machine and Device - Create/Read/Delete|MOS-9730, MOS-9712, MOS-10564,MOS-12076|
|66.|Master Data Management|Individual Type Management - Read|MOS-13950|


**2. Pre-registration:**

|**S.No.**| **Component Name**| **Feature**|**JIRA ID**|
|:------:|-----|---|---|
|1.|Pre-Registration Application Manager|Provide Demographic Data and Upload Documents (Includes: Create\Modify\Delete)|MOS-13344,MOS-13682, MOS-14511, MOS-623, MOS-626, MOS-628, MOS-792, MOS-793, MOS-794, MOS-797, MOS-805, MOS-806|
|2.|Login|Login to the Pre-registration application with Mobile or E-Mail and OTP|MOS-13173, MOS-980, MOS-17, MOS-26|
|3.|Logout|Logout of the Pre-registration application|MOS-10485, MOS-205|
|4.|Acknowledgement|Generate acknowledgement for successful pre-registration|MOS-13143, MOS-812|
|5.|RC Identifier|Search for available registration centers to book appoint|MOS-814|
|6.|Availability Checker|Get availability of slots for the chosen registration center|MOS-663, MOS-816|
|7.|Appointment Booking|Book\re-book the appointment in the chosen registration-center for registration|MOS-664, MOS-665, MOS-817, MOS-818, MOS-977, MOS-978|
|8.|Translation|Translation of the labels/static content as per the pre-configured default language for a Country|MOS-666|
|9.|Transliteration|Transliteration of the values entered as per the default language chosen by the individual|MOS-667|
|10.|PRID Generator|Generate/Assign a unique Pre-registration ID per applicant|MOS-1072|
|11.|Pre-Registration Data Sync|Synchronize the Pre-registration data with the Registration-Client|MOS-1999| 
|12.|Pre-Registration Data Sync|Synchronize Status of PRIDs with Registration Processor|MOS-668|

**3. Registration Client:** - WIP

|**S.No.**| **Component Name**| **Feature**|**JIRA ID**|
|:------:|-----|---|---|
|1.|RC Setup & Update|Install/Update and launch the Registration-client software|MOS-13527, MOS-67, MOS-61, MOS-14|
|2.|Sync| | |
|3.|Login| | |
|4.|Authentication| | |
|5.|Authorization| | |
|6.|Device Onboarding| | |
|7.|User Registration| | |
|8.|Logout| | |
|9.|New Registration| | |
|10.|Translation| | |
|11.|Transliteration| | |
|12.|EoD Process| | |
|13.|Disk Space Checker| | |
|14.|Acknowledgement| | |
|15.|Packet Creation| | |
|16.|Data Clean Up| | |
|17.|Notification| | |
|18.|Packet Exporter| | |
|19.|Security Scan| | |
|20.|UIN Update| | |
|21.|Registration Reports| | |
|22.|Security| | |
|23.|VDM| | |

**4. Registration Processor:** 

|**S.No.**| **Component Name**| **Feature**|**JIRA ID**|
|:------:|-----|---|---|
|1.|packet-receiver-stage|It receives the packet sent from the registration client and performs various sanity checks on the packet|MOS-1030, MOS-1031, MOS-11567, MOS-11855, MOS-249, MOS-43, MOS-44, MOS-45, MOS-46, MOS-49|
|2.|Demo de-dupe Stage|Demographic de-duplication of name,gender and DOB|MOS-1064, MOS-1079, MOS-13137|
|3.|Biometric Dedupe Dummy ABIS|A dummy ABIS which provides failure and successful scenarios using Dummy Tags|MOS-11897|
|4.|Mannual Verification|This is a pluggable stage where a manual verifier can verify the demographic and biometric data of an individual manually|MOS-1076, MOS-1077, MOS-1078, MOS-1080, MOS-1081, MOS-1082|
|5.|UIN Generator Stage|Generates & allocates UIN. Stores the individual's biometric & demographic data in the identity repository. Notifies the resident that UIN is generated trough the configured channels (SMS,Email etc.)|MOS-1065|
|6.|Print Queue Stage|Enable the availability of UIN data & UIN card for printing and postal services|MOS-1071|
|7.|UIN update stage|Updates the data(demographic \biometric) of the resident, Updation of UIN status to de-activate and Re-activate|MOS-1085, MOS-1086, MOS-1087, MOS-1089, MOS-12924, MOS-13210, MOS-13211|
|8.|External system integration|This stage interacts with various external systems|MOS-1032, MOS-13149, MOS-13150, MOS-13151, MOS-13595|
|9.|Non-functional requirements for Processor|Retry Stage|MOS-13197, MOS-8225|
|10.|Non-functional requirements for Processor|Registration processor camel bridge|MOS-10727, MOS-12568|

**5. ID-Authentication:** 

|**S.No.**| **Component Name**| **Feature**|**JIRA ID**|
|:------:|-----|---|---|
|1.|TSP Authentication |Validates if the authenticating agency(s) are authenticated sources to initiate the individual's authentication request|MOS-12231, MOS-10938, MOS-10914, MOS-1421, MOS-1099, MOS-1098, MOS-13157, MOS-13156|
|2.|TSP Authorization|Determines if the authenticating agency(s) are authorized entities to initiate the individual's authentication request|MOS-8369, MOS-1156, MOS-1129, MOS-1123|
|3.|Biometric Authentication|Verifies the authenticity of an individual using biometric attributes provided in the authentication request|MOS-10831,MOS-10378, MOS-10308, MOS-10046, MOS-1411, MOS-1154, MOS-1150, MOS-1133, MOS-12073, MOS-1155, MOS-1145, MOS-12072, MOS-10963, MOS-10131, MOS-10114, MOS-1417, MOS-1149, MOS-1146|
|4.|Demographic Authentication|Verifies the authenticity of an individual using demographic attributes provided in the authentication request|MOS-11900, MOS-10182, MOS-8854, MOS-8437, MOS-1412, MOS-1114, MOS-584, MOS-233, MOS-232, MOS-231, MOS-230, MOS-223, MOS-212, MOS-208, MOS-207, MOS-13162|
|5.|OTP Authentication|Enables an individual to receive OTP. Verifies the authenticity of an individual using OTP provided in the authentication request|MOS-27, MOS-41, MOS-42, MOS-224, MOS-1415, MOS-587, MOS-1902, MOS-8420, MOS-8820|
|6.|Static PIN Authentication|Enables storage of static pin set by an individual using Resident Services APIs. Verifies the authenticity of an individual using static pin provided in the authentication request|MOS-13674, MOS-1422, MOS-1414, MOS-1142, MOS-1140|
|7.|E-KYC Authentication Services|Provides E-KYC details of an individual to the authenticating agency post successful authentication of the individual|MOS-13963, MOS-12241, MOS-10165, MOS-9396, MOS-9224, MOS-9207, MOS-9190, MOS-9173, MOS-9156, MOS-1425, MOS-1119, MOS-13963, MOS-12241, MOS-10165, MOS-9396, MOS-9224, MOS-9207, MOS-9190, MOS-9173, MOS-9156, MOS-1425, MOS-1119|
|8.|Multi-factor Authenticator|Verifies the authenticity of an individual using multiple attributes provided in the authentication request|MOS-13326, OS-13299, MOS-12228, MOS-12225, MOS-10890, MOS-10705, MOS-10475, MOS-10097, MOS-10080, MOS-10063, MOS-10012, MOS-9333, MOS-9128, MOS-8871, MOS-8837, MOS-8819, MOS-8403, MOS-8386, MOS-5481, MOS-1423, MOS-1420, MOS-1153, MOS-1144, MOS-1143, MOS-1141, MOS-1139, MOS-1136, MOS-1132, MOS-1131, MOS-1128, MOS-1126, MOS-1125, MOS-1124, MOS-1121, MOS-15211, MOS-15131, MOS-15194, MOS-15288, MOS-15245, MOS-1118, MOS-1116, MOS-1148, MOS-1134, MOS-1117, MOS-13, MOS-11|
