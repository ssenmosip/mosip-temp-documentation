An ABIS system that integrates with MOSIP should support the following operations. All ABIS operations are via a message queue and asynchronous.

### Common parameters used for all ABIS operations

Name | Description | Restrictions | Default Value | Example
-----|----------|-------------|--------------|---------------
requestID | ID that is associated with each request sent to ABIS | ABIS should not use this ID in any other context outside the request | | 80bd41f8-31b2-46ac-ac9c-3534fc1b220e (UUID)
referenceID |  Id of a single registration record. Registration record is maintained in MOSIP. This ID is the mapping between MOSIP and ABIS | None | | 80bd41f8-31b2-46ac-ac9c-3534fc1b220e (UUID)
referenceURL | URL to the biometrics data stored in MOSIP. This URL will have read only access | None | | 
biometricType | Type of biometric data sent in the request | FMR/FIR/IIR | |
Return Value | Response | None | None | Integer
failureReason | Response | None | None | Integer
scaledScore | Score of the match against the population | None | None | Integer
targetFPIR | FPIR score as per the formula | None | None | Integer
maxResults | maximum number of results returned for IDENTIFY operation | 30 | 30 | Integer

### Standard return codes
0 | not used
--|---------
1 | Success
2 | Failed

## Failure reasons
Code | Reason
-----| ------
1 | Internal error - Unknown
2 | Aborted
3 | Unexpected error - Unable to access biometric data
4 | Unable to serve the request

All the below operations send biometric data in CBEFF format. (Please refer https://github.com/mosip/mosip/wiki/MOSIP-Biometric-Data-Specifications#cbeff-xml-format-sample for sample cbeff data)
### INSERT (insert biometric data of an Individual)
```
//Request
{
	"id" : "Insert",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"referenceId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"referenceURL" : "https://mosip.io/biometric/45678"
        	
}

//Success response
{
	"id" : "Insert",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "1"
}

//Failure response
{
	"id" : "Insert",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "2",
	"failureReason" : ""
}
```
### Behavior of Insert
 - ABIS must get biometric data from referenceURL, process it and store it locally within the ABIS reference database
 - Demographic data corresponding to the individual will be sent as name value pairs in the request
 - referenceId must not be active prior to this pperation i.e., it must not have been used before this operation
 - De-duplication must not be performed in this operation
 - MOSIP must provide CBEFF format biometric data to ABIS

### IDENTIFY
```
//Request
{
	"id" : "Identify",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"referenceId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"maxResults" : "30",
	"targetFPIR" : "30",
	"gallery" : {
		"url" : "",
		"referenceIds" : [
			"referenceId" : "",
			"referenceId" : "",
		]
	}	
}

//Success response
{
	"id" : "Identify",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "1",
	"candidateList" : {
		"count" : "",
		"candidates" : [
			{
				"referenceId" : "",
				"scaledScore" : ""
			},
			{
				"referenceId" : "",
				"scaledScore" : ""
			}
		]
	}
}

//Failure response
{
	"id" : "Identify",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "2",
	"failureReason" : ""
}
```

### Behavior of IDENTIFY
 - IDENTIFY request MUST provide a 1:n comparison
 - The input set for comparison can be provided by referenceID
 - The collection against which the input set has to be matched is specified by galleryURL or set of referenceID's. Either 
   URL or reference ID's can be provided, but not both. If referenceId is provided, atleast one referenceID must be 
   provided in the input. The provided referenceID's must be present in the reference database.
 - maxResults specify how many results can be returned
 - IDENTIFY should give all candidates which match targetFIPR or a better score than the targetFIPR
 - This request should not match against referenceID that is not in the reference database

### VERIFY
```
//Request
{
	"id" : "Verify",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",	
	"referenceURL" : "https://mosip.io/biometric/45678",
	
	"maxResults" : "30",
	"targetFMR" : "30",
	
	"biometrics" : [
		"biometric" : {
			"type" : "FMR (Finger Print Minutiae Record)|FIR (FingerPrint Image Record)|IIR (Iris Image Record)",
			"value" : "base64 encoded value"
		},
		"biometric" : {
			"type" : "FMR (Finger Print Minutiae Record)|FIR (FingerPrint Image Record)|IIR (Iris Image Record)",
			"value" : "base64 encoded value"
		}
	],
	"gallery" : {		
		"referenceIds" : [
			"referenceId" : "",
			"referenceId" : "",
		]
	}	
}

//Success response
{
	"id" : "Verify",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "",
	"candidateList" : {
		"count" : "",
		"hasMore" "",
		"candidates" : [
			{
				"referenceId" : "",
				"scaledScore" : ""
			},
			{
				"referenceId" : "",
				"scaledScore" : ""
			}
		]
	}
}

//Failure response
{
	"id" : "Verify",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "",
	"failureReason" : ""
}
```
### Behavior of VERIFY
- Verify request must provide a 1:n comparison
- Request can contain one or more biometric data i.e., FingerPrint and/or Iris
- FingerPrint Minutiae Record (FMR) should be in ISO format without any proprietary extensions
- FingerPrint Image Record (FIR) should be in ISO 19794-4 format only. Image type can be JPEG 2000 or PNG
- Iris Image Record (IIR) should be in ISO 19794-6 format only. Image type can be JPEG 2000 or PNG
- Biometrics data can be provided inline or through referenceURL, but not both

### DELETE
```
//Request
{
	"id" : "Delete",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"referenceId" : ""
}

//Success response
{
	"id" : "Delete",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : ""
}

//Failure response
{
	"id" : "Delete",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "",
	"failureReason" : ""
}
```

### Behavior of DELETE
- Removes only the entry referred by the referenceId
- This operation can be used to remove duplicates found by Identify

### PING
```
//Request
{
	"id" : "Ping",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717"
}

//Success response
{
	"id" : "Ping",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"returnValue" : "",
	"failureReason" : ""
}
```

### Behavior of PING
A PING request should respond with a response on the liveness of the ABIS system

### Pending Jobs
```
//Request
{
	"id" : "PendingJobs",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717"
}

//Success response
{
	"id" : "PendingJobs",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"jobscount" : "",
	"returnValue" : "",
	"failureReason" : ""	
}
```

### Behavior of Pending Jobs
- ABIS responds with the count of requests that are still pending

### Reference Count
```
//Request
{
	"id" : "ReferenceCount",
	"ver" : "1.0",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717"
}

//Success response
{
	"id" : "ReferenceCount",
	"requestId" : "01234567-89AB-CDEF-0123-456789ABCDEF",
	"timestamp" : "1539777717",
	"count" : "",
	"returnValue" : "",
	"failureReason" : ""	
}
```
### Behavior of Reference Count
- ABIS will send a count of records in the reference database
