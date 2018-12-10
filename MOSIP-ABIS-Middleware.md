A country may use one or more ABIS's to de-duplicate biometric data. The reason for using multiple ABIS's could be
- Use one ABIS for fingerprint and another for Iris
- Use multiple ABIS's for the same biometric data and evaluate the best ABIS based on the de-duplication (However, MOSIP ABIS middleware will not have any logic to evaluate the best ABIS)

MOSIP ABIS middleware will have the following components
- MOSIP ABIS request handler 
- Request router (based on routing policy, an ABIS request is routed to the correct ABIS system)
- ABIS response handler
- ABIS performance evaluator

![MOSIP ABIS Middleware](_images/arch_diagrams/MOSIP_ABIS_middleware.png)

## MOSIP ABIS Middleware API's
MOSIP ABIS Middleware will support a MATCH interface. This interface accepts the biometrics data of an individual, inserts the data into 1 or more ABIS's based on the routing policy then issues an identify request to the ABIS's. Response from all the ABIS's is evaluated and a response is sent back to the requesting party.

### MATCH (A 1:n match of fingerprint or Iris data)

## Possible strategies for Biometric data management in ABIS
A system owner of MOSIP can choose the strategy to store biometrics data in ABIS. Based on the strategy, they have to modify MOSIP ABIS middleware.

### One entry per registered resident
If a system owner decides to have only one entry per registration, the workflow will look as below
1. Registration
  - Each Registration request on MOSIP will result in a INSERT request on ABIS
  - On IDENTIFY request, if a duplicate is detected then the entry will be deleted (DELETE)

2. Re-registration
  - On Re-Registration in MOSIP, an INSERT request is issued to ABIS followed by DELETE on the old record

### One entry per registration request
If a system owner decides to have only multiple entries per registration, the workflow will look as below
1. Registration
  - Each Registration request on MOSIP will result in a INSERT request on ABIS
  - On IDENTIFY request, if a duplicate is detected then the new entry will be associated with the existing UIN

2. Re-registration
  - On Re-Registration in MOSIP, an INSERT request is issued to ABIS followed by association with the existing UIN


## Possible strategies for deduplication in case of multiple ABIS systems
- MOSIP can be configured to send an INSERT request to one or all the ABIS systems
- MOSIP can be configured to send IDENTIFY request to only 1 ABIS system
- MOSIP can be configured to send IDENTIFY request to all the ABIS systems, and choose the best result based on the scores. This helps to calibrate ABIS for better performance. For this to happen, INSERT request must be sent to all ABIS systems

## ABIS performance evaluator (TBD in v2 of MOSIP)
This component will evaluate the performance of an ABIS over a period of time based on the responses received for MATCH request. 