* [4. Partner Management - SSP](#3-partner-management) 
    * [4.4 Partners- Create/Read/Update/Delete](#33-partners) _(MSP_FR_1.1)_
    * [4.5 Policies - Create/Read/Update/Delete](#33-policies) _(MSP_FR_1.2)_
    * [4.6 Partner-Policy Mapping - Create/Read/Update/Delete](#33-partner-policy-mapping) _(MSP_FR_1.3)_
    * [4.7 MISP-Partner Mapping - Create/Read/Delete](#33-misp-partner-mapping) _(MSP_FR_1.4)_
    * [4.8 Validate and Re-issue Digital Certificate to Partner](#33-digital-certificate) _(MSP_FR_1.5)_
    * [4.9 Distribution of Public Keys to Partners](#33-misp) _(MSP_FR_1.6)_

## 3. Partner Management 
### 3.1 License Key Manager
MOSIP system can generate and validate a license Key
#### A. Generate License Key

Upon receiving a request to generate License Key with input parameters (TSP ID, Expiry Time)

Refer below for the process:

1. Fetch the length from the configurations

1. Validates if the request contains the following input parameters
   * TSP ID - Mandatory
   * Expiry Time - Mandatory
   * If the mandatory input parameters are missing, throw the appropriate message. Refer "Messages" section.
   * License Key generated must be of length configured by ADMIN

3. Generate the License key
1. Map the License key to the TSP ID and Expiry time
1. Responds to the source with the License Key (String)
1. In case of Exceptions, system triggers relevant error messages as specified below.

#### B. Mapping Permissions to License Key


Upon receiving a request to map permissions to the License Key with input parameters (TSP ID, License Key, List of Permissions), the system maps the received permissions to the License Key

Refer below for the process:

1. Validates if the request contains the following input parameters
   * TSP ID - Mandatory
   * License Key - Mandatory
   * List of Permissions - Mandatory

2. If the mandatory input parameters are missing, throw the appropriate message

1. Responds to the source with an appropriate message
1. In case of Exceptions, system triggers relevant error messages

#### C. Fetch Permissions for a License Key


Upon receiving a request to fetch permissions for a License Key with input parameters (TSP ID, License Key), the system Validates if the License Key is Valid

Refer below for the process:

1. Validates if the request contains the following input parameters
   * TSP ID - mandatory
   * License key - Mandatory

2. If the mandatory input parameters are missing, throws the appropriate message.

1. Validates the License key based on following logic
   * License key received should be mapped to the TSP ID received in the request
   * License key should not be expired as per the expiry time mapped to the License Key

4. If the License key is invalid, throws error message

1. In case of Exceptions, system triggers relevant error messages


[**Link to design**](https://github.com/mosip/mosip/blob/master/docs/design/kernel/kernel-licensekeymanager.md)
