This section details about the service APIs in the Registration center modules

* [Registration Centers API](#registration-centers-master-api)

* [Registration Center - Device Mapping API](#registration-center-device-api)

* [Registration Center - Machine Mapping API](#registration-center-machine-api)

* [Registration Center - User - Machine Mapping API](#registration-center-user-machine-mapping-api)

* [Registration Center - Machine - Device API](#registration-center-machine-device-api)

* [Registration Center - Search API](#post-registrationcenterssearch)

* [Registration Center - Filter values](#registration-center-filter-values)

* [Registration Center Type - Search API](#post-registrationcentertypessearch)

* [Registration Center Type - Filter values](#post-regcentertypesfiltervalues)


# Registration Centers API

* [POST /registrationcenters](#post-registrationcenters)
* [PUT /registrationcenters](#put-registrationcenters)
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
name|Yes|Name of the registration center| | 
centertypecode|Yes|Code of the center type| | 
addressline1|Yes|Line 1 of the address| | 
addressline2|No|Line 2 of the address| | 
addressline3|No|Line 3 of the address| | 
locationcode|Yes|Code of the location of the registration center| | 
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
contactphone|No|Contact phone number of the registration center| |  
workinghours|Yes|Working hours of the registration center| | 
perkioskprocesstime|Yes|Process time per kiosk in the registration center| | 
centerstarttime|Yes|Office start time of the registration center| | 
centerendtime|Yes|Office end time of the registration center| | 
holidaylocationcode|Yes|Holiday location of the registration center| | 
contactperson|No|Contact person of the registration center| | 
lunchstarttime|No|Lunch start time of the registration center| | 
lunchendtime|No|Lunch end time of the registration center| | 
timezone |No | time zone of the registration center | |
lang_code |Yes | language code  | |

### Example Request
```JSON
{
  "id": "string",
  "metadata": {},
  "request": [ {
    "addressLine1": "string",
    "addressLine2": "string",
    "addressLine3": "string",
    "centerEndTime": "HH:mm:ss",
    "centerStartTime": "HH:mm:ss",
    "centerTypeCode": "string",
    "contactPerson": "string",
    "contactPhone": "string",
    "holidayLocationCode": "string",
    "langCode": "string",
    "latitude": "string",
    "locationCode": "string",
    "longitude": "string",
    "lunchEndTime": "HH:mm:ss",
    "lunchStartTime": "HH:mm:ss",
    "name": "string",
    "perKioskProcessTime": "HH:mm:ss",
    "timeZone": "string",
    "workingHours": "HH:mm:ss"
  }],
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "version": "string"
}

```
### Example Response
```JSON
{
    "id": "string",
    "version": "string",
    "responsetime": "2019-07-01T09:42:19.401Z",
    "metadata": null,
    "response": {
        "registrationCenters": [
            {
                "id": "10025",
                "name": "Souk Khemiss Mograne",
                "centerTypeCode": "REG",
                "addressLine1": "Route N1",
                "addressLine2": "Mograne",
                "addressLine3": "Morocco",
                "latitude": "33.99999",
                "longitude": "-6.815281",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "eng",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "Mario Speedwagon",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-07-01T09:42:19.653Z",
                "updatedBy": null,
                "updatedDateTime": null,
                "isDeleted": null,
                "deletedDateTime": null
            },
            {
                "id": "10025",
                "name": "سوق الخميس مكرن",
                "centerTypeCode": "REG",
                "addressLine1": "الطريق N1",
                "addressLine2": "مڭرن",
                "addressLine3": "المغرب",
                "latitude": "33.99999",
                "longitude": "-6.815281",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "ara",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "ماريو سبيدواجون",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-07-01T09:42:19.730Z",
                "updatedBy": null,
                "updatedDateTime": null,
                "isDeleted": null,
                "deletedDateTime": null
            },
            {
                "id": "10025",
                "name": "Souk Khemiss Mograne",
                "centerTypeCode": "REG",
                "addressLine1": "la route N1",
                "addressLine2": "Mograne",
                "addressLine3": "Maroc",
                "latitude": "33.99999",
                "longitude": "-6.81666",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "fra",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "Mick Donalds",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-07-01T09:42:21.500Z",
                "updatedBy": null,
                "updatedDateTime": null,
                "isDeleted": null,
                "deletedDateTime": null
            }
        ]
    },
    "errors": null
}
```
# PUT /registrationcenters
Master data is required across the platform. 

This service will update the list of Registration Centers which are used in the MOSIP platform. 

### Resource URL
### `PUT /registrationcenters`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
name|Yes|Name of the registration center| | 
centertypecode|Yes|Code of the center type| | 
addressline1|Yes|Line 1 of the address| | 
addressline2|No|Line 2 of the address| | 
addressline3|No|Line 3 of the address| | 
locationcode|Yes|Code of the location of the registration center| | 
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
contactphone|No|Contact phone number of the registration center| |  
workinghours|Yes|Working hours of the registration center| | 
perkioskprocesstime|Yes|Process time per kiosk in the registration center| | 
centerstarttime|Yes|Office start time of the registration center| | 
centerendtime|Yes|Office end time of the registration center| | 
holidaylocationcode|Yes|Holiday location of the registration center| | 
isactive|Yes|Is the registration center active| | 
contactperson|No|Contact person of the registration center| | 
lunchstarttime|No|Lunch start time of the registration center| | 
lunchendtime|No|Lunch end time of the registration center| | 
timezone |No | time zone of the registration center | |
lang_code |Yes | language code  | |

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
    "responsetime": "2019-07-01T05:44:29.825Z",
    "metadata": null,
    "response": {
        "registrationCenters": [
            {
                "id": "10022",
                "name": "Center Youssoufialaaaa",
                "centerTypeCode": "REG",
                "addressLine1": "Avenue Ouzguita1",
                "addressLine2": "Rabat",
                "addressLine3": "Morocco",
                "latitude": "-33.9999",
                "longitude": "-6.815281",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "eng",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "Mick Donalds",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-06-28T08:24:11.204Z",
                "updatedBy": "zonal-admin",
                "updatedDateTime": "2019-07-01T05:44:30.448Z",
                "isDeleted": null,
                "deletedDateTime": null
            },
            {
                "id": "10022",
               "name": "سوق الخميس مكرن",
                "centerTypeCode": "REG",
                "addressLine1": "الطريق N1",
                "addressLine2": "مڭرن",
                "addressLine3": "المغرب",
                "latitude": "33.99999",
                "longitude": "-6.815281",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "ara",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "ماريو سبيدواجون",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-06-28T08:24:11.256Z",
                "updatedBy": "zonal-admin",
                "updatedDateTime": "2019-07-01T05:44:30.931Z",
                "isDeleted": null,
                "deletedDateTime": null
            },
            {
                "id": "10022",
                "name": "Souk Khemiss Mograne",
                "centerTypeCode": "REG",
                "addressLine1": "la route N1",
                "addressLine2": "Mograne",
                "addressLine3": "Maroc",
                "latitude": "33.99999",
                "longitude": "-6.81666",
                "locationCode": "10190",
                "holidayLocationCode": "RBT",
                "contactPhone": "803062069",
                "workingHours": "8:00:00",
                "langCode": "fra",
                "numberOfKiosks": 0,
                "perKioskProcessTime": "00:15:00",
                "centerStartTime": "09:00:00",
                "centerEndTime": "17:00:00",
                "timeZone": "(GTM+01:00) CENTRAL EUROPEAN TIME",
                "contactPerson": "Mick Donalds",
                "lunchStartTime": "13:00:00",
                "lunchEndTime": "14:00:00",
                "isActive": false,
                "createdBy": "zonal-admin",
                "createdDateTime": "2019-06-28T08:24:11.349Z",
                "updatedBy": "zonal-admin",
                "updatedDateTime": "2019-07-01T05:44:31.558Z",
                "isDeleted": null,
                "deletedDateTime": null
            }
        ],
        "notUpdatedRegCenters": []
    },
    "errors": null
}

```
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
200

Description: Success


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

200

Description: Success


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


# Registration Center search APIs

* [POST /registrationcenters/search](#post-registrationcenterssearch)

# POST /registrationcenters/search

This service is for the registration centers search functionality. All the filter parameters are passed and the registration centers are searched and the matching results are returned. 

### Resource URL
### `POST /registrationcenters/search`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["in","equals","between"]| -NA- |
value|No|Value or id selected in the filter by the end user| -NA- |
fromName|No|If the type is "between", this field represents the JSON name of the from field| -NA- |
fromValue|No|If the type is "between", this field is the value of the fromName| -NA- |
toName|No|If the type is "between", this field represents the JSON name of the to field| -NA- |
toValue|No|If the type is "between", this field is the value of the toName| -NA- |
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
sort|No|This is an array of the sort field and type| | 
sortfield| The field on which the sort is applied | | modifiedDate
sorttype| This should be either of ['ASC','DESC']| | ASC
pagination|The pagination parameter object| |
pageStart|This is the start index | 0 | 10
pageFetch| This is the amount of records to be fetched | 10 | 10


### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string",
	"request": {
		"filters" : [
			{
				"columnName": "",
				"type": "in",
				"value": "",  
				"fromName": "",
				"fromValue": "",  
				"toName":"",  
				"toValue": "",
				"languageCode":""
			}
		],
		"sort":[
			{
				"sortfield":"string",
				"sorttype":"ASC"
			}
		],
		"pagination":{
			"pageStart":"number",
			"pageFetch":"number"
		}
		
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
  "registrationcenters": [
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
   ],
	"fromRecord" : "number",
	"toRecord":"number",
	"totalRecord":"number"
 }
}
```
# Registration Center filter values

* [POST /registrationcenters/filtervalues](#post-registrationcentersfiltervalues)

# POST /registrationcenters/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.  

### Resource URL
### `POST /registrationcenters/filtervalues`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["unique","all"]| unique | unique
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 


### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string"
	"request": {
		"filters" : [
			{
				"columnName": ""
				"type": "unique"
			}
		],
		"languageCode": "string",
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
  "filters": [
	{
		"fieldID": "string",
		"fieldCode":"string",
		"fieldValue": "string"
	}
   ]
 }
}
```
# Registration Center Type Search APIs

* [POST /registrationcentertypes/search](#post-registrationcentertypessearch)

# POST /registrationcentertypes/search

This service is for the registration center types search functionality. All the filter parameters are passed and the registration center types are searched and the matching results are returned. 

### Resource URL
### `POST /registrationcentertypes/search`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["contains","equals","startsWith","between"]| -NA- |
value|No|Value or id selected in the filter by the end user| -NA- |
fromValue|No|If the type is "between", this field is the value of the start range| -NA- |
toValue|No|If the type is "between", this field is the value of the end range| -NA- |
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 
sort|No|This is an array of the sort field and type| | 
sortfield| The field on which the sort is applied | | modifiedDate
sorttype| This should be either of ['ASC','DESC']| | ASC
pagination|The pagination parameter object| |
pageStart|This is the start index | 0 | 10
pageFetch| This is the amount of records to be fetched | 10 | 10

### Filter Values
Filter Name| Search Values
-----|----------
status|["contains","equals","startsWith"]

### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string",
	"request": {
		"filters" : [
			{
				"columnName": "",
				"type": "in",
				"value": "", 
				"fromValue": "",
				"toValue": ""
			}
		],
		"sort":[
			{
				"sortfield":"string",
				"sorttype":"ASC"
			}
		],
		"pagination":{
			"pageStart":"number",
			"pageFetch":"number"
		},
		"languageCode":""
		
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
  "registrationcentertypes": [
	{
		"code": "string",
                "langCode": "string",
                "name": "string",
                "descr": "string",
                "isActive": true
	}
   ],
	"fromRecord" : "number",
	"toRecord":"number",
	"totalRecord":"number"
 }
}
```

# Registration Center Types Filter values

* [POST /regcentertypes/filtervalues](#post-regcentertypesfiltervalues)

# POST /regcentertypes/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.  

### Resource URL
### `POST /regcentertypes/filtervalues`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
filters|No|Array of the filter applied. In case of "list" screen, this array will be empty| -NA- |
columnName|No|The column name in the JSON response| -NA- |
type|No|The value have to be in ["unique","all"]| unique | unique
languagecode|Yes|Language code in Language code in ISO 639-2 format| | 


### Example Request
```JSON
{
	"id": "string",
	"metadata": {},
	"requesttime": "2018-12-10T06:12:52.994Z",
	"version": "string"
	"request": {
		"filters" : [
			{
				"columnName": ""
				"type": "unique"
			}
		],
		"languageCode": "string",
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
  "filters": [
	{
		"fieldID": "string",
		"fieldCode":"string",
		"fieldValue": "string"
	}
   ]
 }
}
```