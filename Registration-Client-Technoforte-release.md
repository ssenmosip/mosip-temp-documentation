**Date: 06 Jun 2019** 

**MOSIP**

|**S.No.**| **Deliverable Name**| **Supporting Information**|**Comments**|
|:------:|-----|---|---|
|1.|MOSIP - High Level Design Document|[Click to View](Deliverables---Attachments)|Refer attachment 1 in the linked page - Attachment Name: MOSIP_HLD_v2 - Delivered on 05Feb'19|
|2.|MOSIP - Platform Guide|[MOSIP Platform Documentation](Platform-Documentation)|Refer Section 10.1 in the linked page|
|3.|MOSIP - Getting Started Document|[MOSIP Getting Started Document](https://github.com/mosip/mosip/wiki/Getting-Started)|


**Date: 06 Jun 2019**

**Module: Registration**

|**S.No.**|**Module**|**Deliverable Name**| **Supporting Information**|**Comments**|
|:------:|-----|---|---|---|
|1.|Registration|Installation Guide| [Click to View](https://github.com/mosip/mosip/wiki/Registration-Client-Setup)
|2.|Registration|Component-Feature-JIRA ID Mapping|[Click to View](https://github.com/mosip/mosip/wiki/Component-Feature-ID-JIRA-ID-Mapping#9-registration-)|
|3.|Registration|High Level Design Document|[MOSIP Platform Documentation](https://github.com/mosip/mosip/wiki/Platform-Documentation#32-registration-services-)|Refer Section 3.2 in the linked page|
|4.|Registration|Code Drop|[Tag: 0.12.6](/mosip/mosip/releases/tag/0.12.6)||
|5.|Registration|Known Defects and Pending Items|[Click to View](Deliverables---Attachments)|Refer Section 6 in the linked page|

**Date: 06 Jun 2019**

**Module: Registration**

|**S.No.**|**Module**|**Deliverable Name**| **Supporting Information**|**Comments**|
|:------:|-----|---|---|---|
|1.|Registration|Tested Code|[Tag: 0.12.6](/mosip/mosip/releases/tag/0.12.6)|Exit Criteria: Sonar report with all quality gates cleared ([Sonar Report](//104.215.158.154:9000/dashboard?id=io.mosip.preregistration%3Apre-registration-parent)), Zephyr report indicating: No Blocker/Critical/Major Defects, 100% test cases executed (link to Zephyr report)|
|2.|Registration|Test Cases|[Click to view](//mosipid.atlassian.net/projects/MOS?version.id=10016&cycle.id=3ecb8208-a6f8-4ce0-9c07-1b87e1842e97&selectedItem=com.thed.zephyr.je__project-centric-view-tests-page&testsTab=test-cycles-tab)||
|3.|Registration|Mindmaps|[Click to View](/mosip/mosip/tree/master/docs/testing/Registration%20Client/Mindmaps)|
|4.|Registration Api|Test Cases|[Click to View](https://github.com/mosip/mosip/blob/master/docs/testing/Registration%20Client/Mindmaps/Reg_Client_NonBio_Integration_TestCases.xlsx)|

**Prerequisites : <br><sub>Dependent module/component with their respective versions should be mentioned here</sub></br>**  

|**Module/Files**|**Component**|**Version**|**Description (If any)**|
|-----|-------------|----------------|--------------|
|Clam AV |NA|NA|<br>Download the windows clam av antivirus by provided link and install the s\w.</br> <br>[https://www.clamav.net/downloads#otherversions]</br>|
|[mosip-sw-0.12.6.zip](https://devops.mosip.io/artifactory/libs-release/io/mosip/registration/registration-client/0.12.6/)|jar,DB, MDM, Props and JRE|0.12.6|<br>Please unzip the file and execute the run.bat</br><br> **run.bat**</br>|
|Master Data Setup |NA|Latest Version|Kernel 0.12.6 version of DB scripts can be used. Refer [MOSIP Getting Started doc.] (https://github.com/mosip/mosip/wiki/Getting-Started#7-configuring-mosip-).|
|kernel-core|NA|0.12.6|Basic core kernel packages.|
|kernel-logger-logback|NA|0.12.6|Use for the logging.|
|kernel-dataaccess-hibernate|NA|0.12.6|Used for the communicating to the DB.|
|kernel-auditmanager-api|NA|0.12.5|Used to audit the records into the DB|
|kernel-idvalidator-rid|NA|0.12.6|Used to validate the RID format.|
|kernel-idvalidator-uin|NA|0.12.6|Used to validate the UIN format|
|kernel-idvalidator-prid|NA|0.12.6|Used to validate the PRID format|
|kernel-idgenerator-rid|NA|0.12.6|Used to Generate the RID.|
|kernel-crypto-signature|NA|0.12.6|Used to validate the signature response from server.|
|kernel-keygenerator-bouncycastle|NA|0.12.6|Used to generate the key pair for AES -256.|
|kernel-templatemanager-velocity|NA|0.12.6|Used to generate the template manager using the velocity|
|kernel-qrcodegenerator-zxing|NA|0.12.6|Used to generate the QR code in acknowledgment page.|
|kernel-pdfgenerator-itext|NA|0.12.6|Used to scan the document in PDF format.|
|kernel-crypto-jce|NA|0.12.6|Used to encrypt the packet information|
|kernel-jsonvalidator|NA|0.12.6|Used to validate the JSON.|
|kernel-virusscanner-clamav|NA|0.12.6|Used to communicate to the Antivirus Clam AV|
|kernel-transliteration-icu4j|NA|0.12.6|Used to transliterate the Arabic to French and vice versa.|
|kernel-applicanttype-api|NA|0.12.6|Used to get the applicant types |
|kernel-cbeffutil-api|NA|0.12.6|Used to generate the CBEFF file and validate against the schema also.|
|kernel-bioapi-provider|NA|0.12.6|Used to integrate for the user-onboarding.|

**Open Issues : <br><sub>List of Open Issues, which would be resolved or fixed in another release version, but same Sprint</sub></br>**  

|Open Items|Description
|-----------------|----------------------
Transliteration|English-Arabic/ French Transliteration  won't work because of non-availability of kernel library. Vice versa also won't work.
Bio-API|Integration with Bio-API for user-onboarding.
MDM | Bio device Integration. 
TPM | Secure with TPM public key.  

