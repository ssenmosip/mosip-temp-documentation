This section details about the service APIs in the Registration center modules

* [Registration Centers API](#registration-centers-master-api)

* [Registration Center - Device Mapping API](#registration-center-device-api)

* [Registration Center - Machine Mapping API](#registration-center-machine-api)

* [Registration Center - User - Machine Mapping API](#registration-center-user-machine-mapping-api)

* [Registration Center - Machine - Device API](#registration-center-machine-device-api)


# Registration Centers Master API

* [POST /registrationcenters](#post-registrationcenters)
* [GET /registrationcenters](#get-registrationcenters)
* [GET /registrationcenters/{id}/{languagecode}](#get-registrationcentersidlanguagecode)
* [GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}](#get-getregistrationcenterholidayslanguagecoderegistrationcenteridyear)
* [GET /getlocspecificregistrationcenters/{langcode}/{locationcode}](#get-getlocspecificregistrationcenterslangcodelocationcode)
* [GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}](#get-getcoordinatespecificregistrationcenterslanguagecodelongitudelatitudeproximitydistance)
* [GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}](#get-registrationcentershistoryidlanguagecodeeff_dtimes)
* [GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}](#get-getregistrationmachineusermappinghistoryeff_dtimesregistrationcenteridmachineiduserid)
* [GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}](#get-getlocspecificregistrationcentershierarchyleveltextvaluelanguagecode)

# POST /registrationcenters
Master data is required across the platform. 

This service will create the list of Registration Centers which are used in the MOSIP platform. 

### Resource URL
### `POST /registrationcenters`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
registrationcentername|Yes|Name of the registration center| | 
centertypecode|Yes|Code of the center type| | 
addressline1|No|Line 1 of the address| | 
addressline2|No|Line 2 of the address| | 
addressline3|No|Line 3 of the address| | 
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
contactphone|Yes|Contact phone number of the registration center| |  
workinghours|Yes|Working hours of the registration center| | 
perkioskprocesstime|Yes|Process time per kiosk in the registration center| | 
officestarttime|Yes|Office start time of the registration center| | 
officeendtime|Yes|Office end time of the registration center| | 
holidaylocationcode|Yes|Holiday location of the registration center| | 
isactive|Yes|Is the registration center active| | 
centertype|Yes|Type of the registration center| | 
address|Yes|Address of the registration center| | 
workinghours|Yes|Working hours of the registration center| | 
contactnumber|Yes|Contact number of the registration center| | 
pincode|Yes|Pincode of the registration center| | 
locationcode|Yes|Code of the location of the registration center| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "addressLine1": "string",
    "addressLine2": "string",
    "addressLine3": "string",
    "centerEndTime": "HH:mm:ss",
    "centerStartTime": "HH:mm:ss",
    "centerTypeCode": "string",
    "contactPerson": "string",
    "contactPhone": "string",
    "holidayLocationCode": "string",
    "id": "string",
    "isActive": true,
    "languageCode": "string",
    "latitude": "string",
    "locationCode": "string",
    "longitude": "string",
    "lunchEndTime": "HH:mm:ss",
    "lunchStartTime": "HH:mm:ss",
    "name": "string",
    "numberOfKiosks": 0,
    "perKioskProcessTime": "HH:mm:ss",
    "timeZone": "string",
    "workingHours": "string"
  }
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
	        "id":"string"
             }
}
```
### Response codes
200

Description: OK

201

Description: Created

202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# GET /registrationcenters
Master data is required across the platform. 

This service will provides the service for the List of Registration Centers. 

### Resource URL
### `GET /registrationcenters`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	}
   ]
 }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# GET /registrationcenters/{id}/{languagecode}
Master data is required across the platform. 

This service will provides the service for the List of Registration Centers. 

### Resource URL
### `GET /registrationcenters/{id}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
       	}
   ]
 }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}
This service will list of holidays for a particular registration center for that particular year. 

### Resource URL
### `GET /getregistrationcenterholidays/{languagecode}/{registrationcenterid}/{year}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
registrationcenterid|Yes|ID of the registration center| | 
year|Yes|The year for which the list of holidays is listed| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenter": [
	{
		"registrationcentername":"",
		"centertypecode":"",
		"addressline1":"",
		"addressline2":"",
		"addressline3 ":"",
		"longitude ":"",
		"latitude":"",
		"contactphone":"",
		"numberofkiosks":"",
		"workinghours":"",
		"perkioskprocesstime":"",
		"officestarttime":"",
		"officeendtime":"",
		"holidaylocationcode":"",
		"isactive":"",
		"centertype":"",
		"address":"",
		"workinghours":"",
		"contactnumber":"",
		"pincode":"",
		"locationcode":"",
		"holidays": [
			"holiday" : {
				"holidayID": "string",
				"holidayDate": "string",
				"holidayName": "string",
				"holidayDay": "string",	
				"holidayMonth": "string",
				"holidayYear": "string",
				"languagecode":"string"
			           }
		            ]		
	  }
     ]
   }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# GET /getlocspecificregistrationcenters/{langcode}/{locationcode}
This service will return a list of enrollment center details based on the location code 

### Resource URL
### `GET /getlocspecificregistrationcenters/{langcode}/{locationcode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
locationcode|Yes|The location code for which the list of enrollment centers are needed| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationCenters": [
    {
          "addressLine1": "string",
          "addressLine2": "string",
          "addressLine3": "string",
          "centerEndTime": "HH:mm:ss",
          "centerStartTime": "HH:mm:ss",
          "centerTypeCode": "string",
          "contactPerson": "string",
          "contactPhone": "string",
          "holidayLocationCode": "string",
          "id": "string",
          "isActive": true,
          "languageCode": "string",
          "latitude": "string",
          "locationCode": "string",
          "longitude": "string",
          "lunchEndTime": "HH:mm:ss",
          "lunchStartTime": "HH:mm:ss",
          "name": "string",
          "numberOfKiosks": 0,
          "perKioskProcessTime": "HH:mm:ss",
          "timeZone": "string",
          "workingHours": "string"
       }
   ]
 }
}
```
200

Description: OK

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}
This service will return a list of enrollment center details based on the coordinates

### Resource URL
### `GET /getcoordinatespecificregistrationcenters/{languagecode}/{longitude}/{latitude}/{proximitydistance}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
longitude|Yes|The longitude for which the list of enrollment centers are needed| | 
latitude|Yes|The latitude code for which the list of enrollment centers are needed| | 
proximitydistance|Yes|The proximity diameter in meter| | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
  "registrationcenter": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	   }
     ]
  }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}

This service will provides the service for the List of Registration Centers History. 

### Resource URL
### `GET /registrationcentershistory/{id}/{languagecode}/{eff_dtimes}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenters": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	},
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	}
    ]
  }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}

This service will provides the history of mappings of mapping History of Registration, Machine and User based on Registration Center ID, Machine ID, User ID, Date and Language Code 

### Resource URL
### `GET /getregistrationmachineusermappinghistory/{eff_dtimes}/{registrationcenterid}/{machineid}/{userid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
eff_dtimes|Yes|From which date this change is with effective| | 2018-11-02T05:20:31.075
registrationcenterid|Yes|ID of the registration center| | 
machineid|Yes|ID of the machine| | 

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenters": [
	{
		"registrationcenterid":"string",
		"machineid":"string",
		"userid":"string"
	},
	{
		"registrationcenterid":"string",
		"machineid":"string",
		"userid":"string"
	}
    ]
  }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}
This service will return a list of enrollment center details based on hierarchy level, text value and language code

### Resource URL
### `GET /getlocspecificregistrationcenters/{hierarchylevel}/{textvalue}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
hierarchylevel|Yes|The hierarchy level for which the list of enrollment centers are needed| | 
textvalue|Yes|This is a free text. The search will happen with the combination of heirarchy level, language code and this free text. The enrollment centers which satisfy these 3 criteria will be returned| | 
languagecode|Yes|The enrollment center description will be returned in this language code | | 


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":{
  "registrationcenter": [
	{
			"registrationcentername":"",
			"centertypecode":"",
			"addressline1":"",
			"addressline2":"",
			"addressline3 ":"",
			"longitude ":"",
			"latitude":"",
			"contactphone":"",
			"numberofkiosks":"",
			"workinghours":"",
			"perkioskprocesstime":"",
			"officestarttime":"",
			"officeendtime":"",
			"holidaylocationcode":"",
			"isactive":"",
			"centertype":"",
			"address":"",
			"workinghours":"",
			"contactnumber":"",
			"pincode":"",
			"locationcode":""
	 }
     ]
  }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-041 | Error occured while fetching Registration Centers | registration center fetch exception
KER-MSD-111 | Error occurred while updating Registration Center details | registration center update exception
KER-MSD-112 | Error occurred while deleting Registration Center details | registration center delete exception
KER-MSD-042 | Registration Center not found | registration center not found
KER-MSD-149 | Cannot delete as dependency found | dependency exception
KER-MSD-043 | Invalid date format | date time parse exception
KER-MSD-XXX | start/end time Data not configured in database | data to be validated with not found

# Registration Center User Machine Mapping API

* [POST /registrationmachineusermappings](#post-registrationmachineusermappings)
* [GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}](#get-getregistrationmachineusermappinghistoryeffdtimesregistrationcenteridmachineiduserid-1)
* [PUT /registrationmachineusermappings](#put-registrationmachineusermappings-1)


## POST /registrationmachineusermappings

This service will create a Registration Center-User-Machine Mapping which are used in the MOSIP platform. 

### Resource URL
### `POST /registrationmachineusermappings`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
cntrId|Yes|Registration Center Id for request| | 
machineId|Yes|Machine Id for request| | 
usrId|Yes|User Id for request| | 
isActive|Yes|Mapping is active or not| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "cntrId": "RC001",
    "isActive": true,
    "machineId": "MC001",
    "usrId": "QC001"
  }
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
            "cntrId": "RC001",
            "machineId": "MC001",
            "usrId": "QC001"
            }
}
```
### Response codes
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

## GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}

This service will provides the service for the Center-User-Machine with their history. 


### Resource URL
### `GET /getregistrationmachineusermappinghistory/{effdtimes}/{registrationcenterid}/{machineid}/{userid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
ID|Yes|Machine History Id|
effdtimes|Yes|Effective Date and Time of the Machine|
registrationcenterid|Yes|Registration Center Id|
machineid|Yes|Machine Id |
userid|Yes|User Id|

### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response":  {
      "registrationCenters": [
             {
              "cntrId": "string",
              "effectivetimes": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
              "isActive": true,
              "langCode": "string",
              "machineId": "string",
              "usrId": "string"
             }
        ]
    }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

## PUT /registrationmachineusermappings

This service will create or update a Registration Center-User-Machine Mapping which are used in the MOSIP platform. 

### Resource URL
### `PUT /registrationmachineusermappings`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
cntrId|Yes|Registration Center Id for request| | 
machineId|Yes|Machine Id for request| | 
usrId|Yes|User Id for request| | 
isActive|Yes|Mapping is active or not| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
      "cntrId": "RC001",
      "isActive": true,
      "langCode": "string",
      "machineId": "MC001",
      "usrId": "QC001"
  }
}
```
### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response": {
    "mapped": [
      {
        "cntrId": "string",
        "machineId": "string",
        "usrId": "string"
      }
    ],
    "notmapped": [
       {
        "cntrId": "string",
        "machineId": "string",
        "usrId": "string"
      }
    ]
  }
}
```
### Response codes
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-078 | Error occurred while inserting mapping of Center, User and Machine details | registration center user machine mapping insert exception
KER-MSD-131 | Registration Center, Machine and User Mapping not found | registration center user machine not found
KER-MSD-108 | Error occurred while deleting mapping of Center, User and Machine details | registration center user machine delete exception
KER-MSD-136 | Error occurred while updating mapping of Center, User and Machine details | registration center user machine update exception
			
			
# Registration Center Machine API

* [POST /registrationcentermachine](#post-registrationcentermachine)
* [DELETE /registrationcentermachine/{regCenterId}/{machineId}](#deleteregistrationcentermachineregcenteridmachineid)

## POST /registrationcentermachine
Master data is required across the platform. 

This service will create the mapping of registration canter and machine in the RegistrationCenterMachine Master module. 

### Resource URL
### `POST /registrationcentermachine`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|Available machine id| | 
regCenterId|Yes|Available registration center| | 

### Example Request
```JSON  
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "isActive": true,
    "langCode": "string",
    "machineId": "MC001",
    "regCenterId": "RC001"
  }
}


```
### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
      "machineId": "string",
      "regCenterId": "string"
  }
}
```
### Response codes
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

500

Description: Internal Server Error 

## DELETE/registrationcentermachine/{regCenterId}/{machineId}

This service will provides the service for delete mapping of  Center-Machine. 


### Resource URL
### `DELETE /registrationcentermachine/{regCenterId}/{machineId}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
regCenterId|Yes|Registration Center Id|
machineId|Yes|Machine Id |


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
  "machineId": "MC001",
  "regCenterId": "RC001"
   }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-074 | Error occurred while inserting a mapping of Machine and Center | registration center machine create exception
KER-MSD-114 | Mapping for Machine and Center not found | registration center machine data not found
KER-MSD-106 | Error occurred while deleting a mapping of Machine and Center | registration center machine delete exception

# Registration Center Device API

* [POST /registrationcenterdevice](#post-registrationcenterdevice)
* [DELETE /registrationcenterdevice/{regCenterId}/{deviceId}](#deleteregistrationcenterdeviceregcenteriddeviceid)

## POST /registrationcenterdevice
Master data is required across the platform. 

This service will create the mapping of registration canter and device in the RegistrationCenterDevice Master module. 

### Resource URL
### `POST /registrationcenterdevice`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
deviceId|Yes|Available device id| | 
regCenterId|Yes|Available registration center| | 

### Example Request
```JSON  
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
     "deviceId": "string",
    "isActive": true,
    "langCode": "string",
    "regCenterId": "string"
  }
}


```
### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   {
        "deviceId": "string",
        "regCenterId": "string"
  }
}
```
### Response codes
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

500

Description: Internal Server Error 

## DELETE/registrationcenterdevice/{regCenterId}/{deviceId}

This service will provides the service for delete mapping of  Device-Machine. 


### Resource URL
### `DELETE /registrationcenterdevice/{regCenterId}/{deviceId}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
regCenterId|Yes|Registration Center Id|
deviceId|Yes|Device Id |


### Example Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   {
           "deviceId": "DV001",
          "regCenterId": "RC001"
    }
}
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-075 | Error occurred while inserting a mapping of Device and Center | registration center device create exception
KER-MSD-115 | Mapping for Device and Center not found | registration center device data not found
KER-MSD-105 | Error occurred while deleting a mapping of Device and Center | registration center device delete exception

# Registration Center Machine Device API

* [POST /registrationcentermachinedevice](#post-registrationcentermachinedevice)
* [DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}](#delete-registrationcentermachinedeviceregcenteridmachineiddeviceid)

## POST /registrationcentermachinedevice
Master data is required across the platform. 

This service will create the mapping of registration center, machine and device in the RegistrationCenterMachineDevice Master module. 

### Resource URL
### `POST /registrationcentermachinedevice`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|Available machine id| | 
regCenterId|Yes|Available registration center| | 
deviceId|Yes|Available device id| | 

### Example Request
```JSON  
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
    "deviceId": "string",
    "isActive": true,
    "langCode": "string",
    "machineId": "string",
    "regCenterId": "string"
  }
}


```
### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   {
   "deviceId": "string",
   "machineId": "string",
   "regCenterId": "string"
  }
}
```
### Response codes
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

500

Description: Internal Server Error 


## DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}
Master data is required across the platform. 

This service will delete the mapping of registration center, machine and device in the RegistrationCenter-Machine-Device Master module. 

### Resource URL
### `DELETE /registrationcentermachinedevice/{regcenterid}/{machineid}/{deviceid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
NA


### Example Response
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
   "deviceId": "string",
   "machineId": "string",
   "regCenterId": "string"
  }
}
```
### Response codes

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

500

Description: Internal Server Error 

### Failure Response:
```JSON
 {
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-076 | Error occurred while inserting a mapping of Center, Machine and Device | registration center machine device create exception
KER-MSD-107 | Error occurred while deleting a mapping of Center, Machine and Device | registration center machine device delete exception
KER-MSD-116 | Mapping for Center, Machine and Device not found | registration center machine device data not found exception
