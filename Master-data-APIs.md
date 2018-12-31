This section details about the service APIs in the Master data modules

[2.3.1 Holiday Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#231-holiday-master-api)

[2.3.2 Blacklisted words Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#232-blacklisted-words-master-api)

[2.3.3 Documents Category Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#233-documents-category-master-api)

[2.3.4 Document formats Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#234-document-formats-master-api)

[2.3.5 Machines Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#235-machines-master-api)

[2.3.6 Devices Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#236-devices-master-api)

[2.3.7 Languages Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#237-languages-master-api)

[2.3.8 Gender Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#238-gender-master-api)

[2.3.9 Titles Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#239-titles-master-api)

[2.3.10 Biometric Types Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2310-biometric-types-master-api)

[2.3.11 ID Types Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2311-id-types-master-api)

[2.3.12 Application Types Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2312-application-types-master-api)

[2.3.13 Registration Centers Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2313-registration-centers-master-api)

[2.3.14 Biometrics Attributes Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2314-biometric-attributes-master-api)

[2.3.15 Locations Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2315-locations-master-api)

[2.3.16 Packet rejection reasons Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2316-packet-rejection-reasons-master-api)

[2.3.17 Packet on hold reasons Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2317-packet-on-hold-reasons-master-api)

[2.3.18 Documents Types Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2318-documents-types-api)

[2.3.19 Machine Types Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2319-machine-types-master-api)

[2.3.20 Machine Specifications Master API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2320-machine-specifications)

[2.3.21 Registration Center User Machine Mapping API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2321-registration-center-user-machine-mapping-api)

[2.3.22 Registration Center Machine API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2322-registration-center-machine-api)

[2.3.23 Registration Center Device API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2323-registration-center-device-api)

[2.3.24 Registration Center Machine Device API](https://github.com/mosip/mosip/wiki/Master-data-APIs#2324-registration-center-machine-device-api)



# 2.3.1 Holiday Master API
## 2.3.1.1 Holiday Master-create service
Master data is required across the platform. 

This service will create the holiday in the Holiday Master module. 

### Resource URL
### `POST /holidays`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
holidayDate|Yes|Holiday date in UTC standard ISO8601 format| | 2028-10-04T05:57:20.929Z
holidayName|Yes|Name of the holiday| | 

### Example Request
```JSON
{
	"id": "mosip.holiday.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : { 
		  "holiday":{ "holidayDate": "string", "holidayName": "string", "languagecode": "string" }
	}
}  
```
### Example Response
```JSON
  { "holidayID": "string" }
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden


## 2.3.1.2 Holiday Master-get service
Master data is required across the platform. 

This service will provides the service for the List of holidays. 
It will also ensure audit data stored is archived based on the defined archival policy.

### Resource URL
### `GET /holidays`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------


### Example Response
```JSON
{
  "holidays": [
	"holiday" : {
		"holidayID": "string",
		"holidayDate": "string",
		"holidayName": "string",
		"holidayDay": "string",	
		"holidayMonth": "string",
		"holidayYear": "string",
		"languagecode": "string"
	}
  ]
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


## 2.3.1.3 Holiday Master-get by language code service

This service will provides the service for the List of holidays based on the holiday ID
It will also ensure audit data stored is archived based on the defined archival policy.

### Resource URL
### `GET /holidays/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in ISO 639-2 Code of the holiday| | eng

### Example Response
```JSON
{
  "holidays": [
	"holiday" : {
		"holidayID": "string",
		"holidayDate": "string",
		"holidayName": "string",
		"holidayDay": "string",	
		"holidayMonth": "string",
		"holidayYear": "string"		
		"languagecode": "string"
	}
  ]
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

# 2.3.2 Blacklisted words Master API

# 2.3.2.1 Blacklisted words Master-create service
Master data is required across the platform. 

This service will the create the list of blacklisted words in the Blacklisted Master module. 

### Resource URL
### `POST /blacklistedwords`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
blacklistedwords|Yes|List of black listed words| | 
languagecode|Yes|Language code in ISO 639-2 Code of the holiday| | eng


### Example Request
```JSON
{
	"id": "mosip.blacklistedwords.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
		"blacklistedwords": ["asdf","lkjh","qwer"],
		"languagecode": "string"
	}
}
```
### Example Response
```JSON
{
  "successfully_created_words": ["asdf","lkjh","qwer"]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.2.2 Blacklisted Master-get service
Master data is required across the platform. 

This service will provides the service for the List of blacklistedwords. 



### Resource URL
### `GET /blacklistedwords`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
	"id": "mosip.blacklistedwords.get",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
		"blacklistedwords":[
			{
				"id":"string",
				"value":"asdf",
				"languagecode":"string",
			},
			{
				"id":"string",
				"value":"asdf"
				"languagecode":"string",
			},
			{
				"id":"string",
				"value":"asdf"
				"languagecode":"string",
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


# 2.3.2.3 Blacklisted Master-get by id and languagecode service

This service will provides the service for the List of blacklistedwords based on the id. 

### Resource URL
### `GET /blacklistedwords/{id}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
	"blacklistedwords":[
		{
			"id":"string",
			"value":"asdf",
			"languagecode":"string"
		},
		{
			"id":"string",
			"value":"asdf",
			"languagecode":"string"
		},
		{
			"id":"string",
			"value":"asdf",
			"languagecode":"string"
		}
	]
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

# 2.3.2.4 Blacklisted Master-update blacklisted word service

This service will provides the service to update blacklistedwords. 

### Resource URL
### `PUT /blacklistedwords`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
word |YES|Blacklisted word| |abc|
description|YES|Description of the blacklisted word|||
langCode|YES|Language Code of the blacklisted word|||
isActive|YES|Blacklisted word is active|||
 

### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-31T10:01:24.578Z",
  "request": {
    "description": "string",
    "isActive": true,
    "langCode": "string",
    "word": "string"
  }
}
```
### Example Response
```JSON
{
  "langCode": "string",
  "word": "string"
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

# 2.3.2.35 Blacklisted Master-delete blacklisted word service

This service will provides the service to delete blacklistedwords. 

### Resource URL
### `DELETE /blacklistedwords/{word}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
word |YES|Blacklisted word| |abc||
 

### Example Request
```JSON
NA
```
### Example Response
```
word(String)
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# 2.3.3 Documents Category Master API
# 2.3.3.1 Documents Category Master-create service

This service will create the list of Documents Category which are used in the MOSIP platform. 

### Resource URL
### `POST /documentcategories`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Document category code| |
description|optional|document description||
isActive|Yes|is active or not||
langCode|Yes|language code||
name|Yes|Document category name|| 

### Example Request
```JSON
{
  "id": "mosip.documentcategories.create",
  "ver": "1.0",
  "timestamp": "2018-12-28T10:56:55.972Z",
  "request": {
    "code": "string",
    "description": "string",
    "isActive": true,
    "langCode": "string",
    "name": "string"
  },
}
```
### Example Response
```JSON
{
  "code": "string",
  "langCode": "string"
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


# 2.3.3.2 Documents Category Master-get service

This service will provides the service for the List of documents categories. 


### Resource URL
### `GET /documentcategories`

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
  "documentcategories": [
		{"id": id, "value": "POA", "languagecode":"string"},
		{"id": id, "value": "POI", "languagecode":"string"},
		{"id": id, "value": "POR", "languagecode":"string"},
		{"id": id, "value": "POB", "languagecode":"string"}
	]
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

# 2.3.3.3 Documents Category Master-get document cateogory based on id and language service

This service will provides the service for the List of documents categories. 


### Resource URL
### `GET /documentcategories/{id}/{languagecode}`

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
  "documentcategories": [
		{"id": id, "value": "POA", "languagecode":"string"},
		{"id": id, "value": "POI", "languagecode":"string"},
		{"id": id, "value": "POR", "languagecode":"string"},
		{"id": id, "value": "POB", "languagecode":"string"}
	]
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

# 2.3.4 Document formats Master API
# 2.3.4.1 Documents Formats Master-create service
Master data is required across the platform. 

This service will create the list of Documents Formats which are used in the MOSIP platform. 

### Resource URL
### `POST /documentformats`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
documentformats|Yes|List of document formats| | 

### Example Request
```JSON
{
	"id": "mosip.documentformats.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "documentformats": [
			{ "documentformat":"pdf", "languagecode":"string" },
			{ "documentformat":"png", "languagecode":"string" },
			{ "documentformat":"jpeg", "languagecode":"string" },
			{ "documentformat":"gif", "languagecode":"string" }
		]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_documentformats": [
		{"documentformatid":id },
		{"documentformatid":id },
		{"documentformatid":id },
		{"documentformatid":id }  
  ]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.4.2 Documents Format Master-get service
Master data is required across the platform. 

This service will provides the service for the List of documents formats. 



### Resource URL
### `GET /documentformats`

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
  "documentformats": [
			{"id":"id", "format": "pdf" ,"languagecode":"string"},
			{"id":"id", "format": "png" ,"languagecode":"string"},
			{"id":"id", "format": "jpeg" ,"languagecode":"string"},
			{"id":"id", "format": "gif" ,"languagecode":"string"}
		]
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

# 2.3.4.3 Documents Format Master-get documents format based on language and id service

This service will provides the service for the List of documents formats. 

### Resource URL
### `GET /documentformats/{id}/{languagecode}`

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
  "documentformats": [
			{"id":"id", "format": "pdf" ,"languagecode":"string"},
			{"id":"id", "format": "png" ,"languagecode":"string"},
			{"id":"id", "format": "jpeg" ,"languagecode":"string"},
			{"id":"id", "format": "gif" ,"languagecode":"string"}
		]
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

# 2.3.5 Machines Master API
# 2.3.5.1 Machines Master-create service

This service will create the list of Machines which are used in the MOSIP platform. 

### Resource URL
### `POST /machines`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machinename|Yes|Name of the machine| | 
macid|Yes|Mac ID of the machine| | 
serialnumber|Yes|Serial number of the machine| | 
isactive|Yes|Is the machine active?| | 

### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-24T05:52:46.758Z",
  "request": {
    "id": "string",
    "ipAddress": "string",
    "isActive": true,
    "langCode": "string",
    "macAddress": "string",
    "machineSpecId": "string",
    "name": "string",
    "serialNum": "string",
    "validityDateTime": "2018-12-24T05:52:46.758Z"
  }
}
```
### Example Response
```JSON
{
  "id": "string"
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.5.2 Machines Master-get service

This service will provides the service to fetch the complete List of machines with the machine details. 

### Resource URL
### `GET /machines`

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
  "machines": [
    {
      "id": "string",
      "ipAddress": "string",
      "isActive": true,
      "langCode": "string",
      "macAddress": "string",
      "machineSpecId": "string",
      "name": "string",
      "serialNum": "string",
      "validityDateTime": "2018-12-24T05:54:42.097Z"
    },
  {
      "id": "string",
      "ipAddress": "string",
      "isActive": true,
      "langCode": "string",
      "macAddress": "string",
      "machineSpecId": "string",
      "name": "string",
      "serialNum": "string",
      "validityDateTime": "2018-12-24T05:54:42.097Z"
    }
  ]
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


# 2.3.5.3 Machines Master-get machines based on language service
Master data is required across the platform. 

This service will provides the service to fetch the List of machines with the machine details based on the language.

### Resource URL
### `GET /machines/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode| Yes | Machine Languge Code|


### Example Response
```JSON
{
  "machines": [
    {
      "id": "string",
      "ipAddress": "string",
      "isActive": true,
      "langCode": "string",
      "macAddress": "string",
      "machineSpecId": "string",
      "name": "string",
      "serialNum": "string",
      "validityDateTime": "2018-12-24T05:58:03.286Z"
    },
{
      "id": "string",
      "ipAddress": "string",
      "isActive": true,
      "langCode": "string",
      "macAddress": "string",
      "machineSpecId": "string",
      "name": "string",
      "serialNum": "string",
      "validityDateTime": "2018-12-24T05:58:03.286Z"
    }
  ]
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


# 2.3.5.4 Machines Master History-get service

This service will provides the service for the List of machines with their history. 


### Resource URL
### `GET /machineshistory/{id}/{languagecode}/{eff_dtimes}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
ID|Yes|Machine History Id|
languagecode|Yes|Language code for the Machine|
eff_dtimes|Yes |Effective Date and Time of the Machine|

### Example Response
```JSON
{
  "machineHistoryDetails": [
    {
      "effectDateTime": "2018-12-24T06:05:26.304Z",
      "id": "string",
      "ipAddress": "string",
      "isActive": true,
      "langCode": "string",
      "macAddress": "string",
      "machineSpecId": "string",
      "name": "string",
      "serialNum": "string",
      "validityDateTime": "2018-12-24T06:05:26.304Z"
    }
  ]
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

# 2.3.6 Devices Master API
# 2.3.6.1 Devices Master-create service

This service will create the list of Devices which are used in the MOSIP platform. 

### Resource URL
### `POST /devices`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
devicetype|Yes|Name of the device| | 
devicemodel|Yes|Mac ID of the device| | 

### Example Request
```JSON
{
	"id": "mosip.device.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
		"devices": [{
				"devicetype": "string",
				"devicemodel": "string",
				"languagecode":"string"				
			},
			{
				"devicetype": "string",
				"devicemodel": "string",
				"languagecode":"string"
			}
		]
	}
}
```
### Example Response
```JSON
{
	"successfully_created_devices": [{
			"deviceid": "string"
		},
		{
			"deviceid": "string"
		}
	]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.6.2 Devices Master-get service

This service will provides the service for the List of devices. 


### Resource URL
### `GET /devices`

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
	"devices": [{
			"devicetype": "string",
			"devicemodel": "string",
			"languagecode":"string"
		},
		{
			"devicetype": "string",
			"devicemodel": "string",
			"languagecode":"string"
		}
	]
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


# 2.3.6.3 Devices Master-get devices based on language and id service

This service will provides the service for the List of devices. 


### Resource URL
### `GET /devices/{id}/{languagecode}`

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
	"devices": [{
			"devicetype": "string",
			"devicemodel": "string",
			"languagecode":"string"
		},
		{
			"devicetype": "string",
			"devicemodel": "string",
			"languagecode":"string"
		}
	]
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

# 2.3.6.4 Devices Master-update devices

This service will update existing device. 


### Resource URL
### `PUT /v1.0/devices`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-


### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-31T05:47:36.645Z",
  "request": {
    "deviceSpecId": "string",
    "id": "string",
    "ipAddress": "string",
    "isActive": true,
    "langCode": "string",
    "macAddress": "string",
    "name": "string",
    "serialNum": "string",
    "validityDateTime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'"
  }
}
```
### Example Response
```JSON
{
  "id": "string"
}
```
### Response codes
200

Description: When Device updated successfully

201

Description: Created

400

Description: When Request body passed is null or invalid

401

Description: Unauthorized

403

Description: Forbidden

404

Description: When Device is not found

500

Description: While updating device any error occurred

# 2.3.6.5 Devices Master-delete devices based on id service

This service will delete the devices. 

### Resource URL
### `DELETE /v1.0/devices/{id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
deviceId|Yes|The device Id| | 

### Example Response
```JSON
{
  "id": "string"
}
```
200

Description: When Device deleted successfully

204

Description: No Content

401

Description: Unauthorized

403
	
Description: Forbidden

404

Description: When Device not found

500

Description: Error occurred while deleting Device

# 2.3.7 Languages Master API
# 2.3.7.1 Languages Master-create service

This service will create a Language which is used in the MOSIP platform. 

### Resource URL
### `POST /languages`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Code of the language| | 
languagename|Yes|Name of the language| | 

### Example Request
```JSON
{
	"id": "mosip.language.create",
	"ver": "1.0",
	"timestamp": "",
	"request": {
		"code": "string",
		"name": "string"
		"family": "string",
		"native_name": "string",
		"is_active": boolean
	}
}
```
### Example Response
```JSON
{
	"code": "string"
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

# 2.3.7.2 Languages Master-get service

This service will provides the service for the List of languages. 

### Resource URL
### `GET /languages`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Code of the language| | 
languagename|Yes|Name of the language| | 


### Example Request
-NA-

### Example Response
```JSON
{
	"languages": [{
		"code": "string",
		"name": "string",
		"family": "string",
		"native_name": "string",
		"is_active": "boolean"
	}]
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

# 2.3.7.3 Languages Master-update service

This service will update a Language which is used in the MOSIP platform. 

### Resource URL
### `POST /languages`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Code of the language| | 
languagename|Yes|Name of the language| | 

### Example Request
```JSON
{
	"id": "mosip.language.update",
	"ver": "1.0",
	"timestamp": "",
	"request": {
		"code": "string",
		"name": "string"
		"family": "string",
		"native_name": "string",
		"is_active": boolean
	}
}
```
### Example Response
```JSON
{
	"code": "string"
}
```
### Response codes
200

Description: Ok

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden


# 2.3.7.4 Languages Master-delete service

This service will delete a Language which is used in the MOSIP platform. 

### Resource URL
### `POST /languages/{code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the language| | 


### Example Request
-NA-
```
### Example Response
```JSON
{
	"code": "string"
}
```
### Response codes
200

Description: Ok

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.8 Gender Master API
# 2.3.8.1 Gender Master-create service

This service will create the list of Gender which are used in the MOSIP platform. 

### Resource URL
### `POST /gendertypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
gendertype|Yes|Name of the gender| | 

### Example Request
```JSON
{
  "id": "string",
  "request": {
    "code": "GC002",
    "genderName": "Male",
    "isActive": true,
    "langCode": "ENG"
  },
  "timestamp": "2018-12-27T09:29:01.351Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
  "code": "GC002",
  "langCode": "ENG"
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.8.2 Gender Master-update service

This service will update Gender which are used in the MOSIP platform. 

### Resource URL
### `PUT/gendertypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of gender type| | 
genderName|Yes|Name of gender type| | 
isActive|Yes|is active or not| | 
code|Yes|language code of gender| | 

### Example Request
```JSON
{
  "id": "string",
  "request": {
    "code": "GC001",
    "genderName": "Male",
    "isActive": true,
    "langCode": "ENG"
  },
  "timestamp": "2018-12-28T08:33:56.217Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
  "code": "GC001",
  "langCode": "ENG"
}
```
### Response codes
200

Description: OK

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.8.3 Gender Master-delete service

This service will delete Gender which are used in the MOSIP platform. 

### Resource URL
### `DELETE/gendertypes/{code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of gender type| |  

### Example Response
```JSON
{
  "code": "GC001",
}
```
### Response codes
200

Description: OK

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.8.4 Genders Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Genders. 



### Resource URL
### `GET /gendertypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
genderid|Yes|Code of the language| | 
gendertype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "genderType": [
    {
      "code": "GC001",
      "genderName": "Female",
      "langCode": "eu",
      "isActive": true
    },
    {
      "code": "GC002",
      "genderName": "Male",
      "langCode": "ENG",
      "isActive": true
    }
  ]
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


# 2.3.8.5 Genders Master-get based on language service

This service will provides the service for the List of Genders. 


### Resource URL
### `GET /gendertypes/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
genderid|Yes|Code of the language| | 
gendertype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "genderType": [
    {
      "code": "GC002",
      "genderName": "Male",
      "langCode": "ENG",
      "isActive": true
    }
  ]
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

# 2.3.9 Titles Master API
# 2.3.9.1 Title Master-create service
Master data is required across the platform. 

This service will create the list of Title which are used in the MOSIP platform. 

### Resource URL
### `POST /title`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
titletype|Yes|Name of the title| | 

### Example Request
```JSON
{
  "id": "string",
  "request": {
    "code": "cvf",
    "isActive": true,
    "langCode": "ghf",
    "titleDescription": "string",
    "titleName": "string"
  },
  "timestamp": "2018-12-27T09:38:58.574Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
  "code": "cvf",
  "langCode": "ghf"
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

# 2.3.9.2 Titles Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Titles. 



### Resource URL
### `GET /title`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
titleid|Yes|Code of the language| | 
titletype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "titleList": [
    {
      "code": "43",
      "titleName": "string",
      "titleDescription": "string",
      "isActive": true,
      "langCode": "ENG"
    },
    {
      "code": "1",
      "titleName": "mosip@#$",
      "titleDescription": "MOSIP@@",
      "isActive": true,
      "langCode": "ENG"
    },
    {
      "code": "234",
      "titleName": "string123",
      "titleDescription": "string123",
      "isActive": true,
      "langCode": "ENG"
    },
    {
      "code": "12345",
      "titleName": "string",
      "titleDescription": "string",
      "isActive": true,
      "langCode": "GER"
    },
    {
      "code": "cvf",
      "titleName": "string",
      "titleDescription": "string",
      "isActive": true,
      "langCode": "ghf"
    }
  ]
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


# 2.3.9.3 Titles Master-get based on language service
Master data is required across the platform. 

This service will provides the service for the List of Titles. 



### Resource URL
### `GET /title/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
titleid|Yes|Code of the language| | 
titletype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "titleList": [
    {
      "code": "xcv",
      "titleName": "string",
      "titleDescription": "string",
      "isActive": true,
      "langCode": "qwe"
    }
  ]
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

# 2.3.9.4 Titles Master-put based on language service
Master data is required across the platform. 

This service will provides the service for updating a particular title. 



### Resource URL
### `PUT /title`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the title| | 
titleName|Yes|Name of the title| | 
isActive|Yes|Name of the title| |
langCode|Yes|Name of the title| |
titleDescription|Yes|Name of the title| |


### Example Response
```JSON
{
  "code": "xcv",
  "langCode": "qwe"
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

# 2.3.9.5 Titles Master-delete based on language service
Master data is required across the platform. 

This service will provides the service for deleting a particular title. 



### Resource URL
### `DELETE /title/{code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the title| | 


### Example Response
```JSON
{
  "code": "xcv"
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




# 2.3.10 Biometric types Master API
# 2.3.10.1 Biometric types Master-create service
Master data is required across the platform. 

This service will create the list of Biometric types which are used in the MOSIP platform. 

### Resource URL
### `POST /biometrictypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometrictype|Yes|Array of the biometric types| | 

### Example Request
```JSON
{
	"id": "mosip.biometrictype.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "biometrictypes": [
				{"biometrictype":"string"},
				{"biometrictype":"string"}
				{"languagecode":"string"}
	  ]
	}
}
```
### Example Response
```JSON
{
	"biometrictypes": [
			{"biometrictype":"string"},
			{"biometrictype":"string"}
			{"languagecode":"string"}
	]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.10.2 Biometrics Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Biometrics. 



### Resource URL
### `GET /biometrictypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometrictypeid|Yes|Code of the language| | 
biometrictype|Yes|Name of the language| | 

### Example Response
```JSON
{
  "biometrictypes": [
				{ 
					"biometrictype": [
						{"biometrictypeid":"string"},
						{"biometrictype":"string"},
						{"languagecode":"string"}						
					]
				}, 
				{ 
					"biometrictype": [
						{"biometrictypeid":"string"},
						{"biometrictype":"string"},
						{"languagecode":"string"}						
					]
				}
			]
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


# 2.3.10.3 Biometrics Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Biometrics. 



### Resource URL
### `GET /biometrictypes/{id}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometrictypeid|Yes|Code of the language| | 
biometrictype|Yes|Name of the language| | 

### Example Response
```JSON
{
  "biometrictypes": [
				{ 
					"biometrictype": [
						{"biometrictypeid":"string"},
						{"biometrictype":"string"},
						{"languagecode":"string"}						
					]
				}, 
				{ 
					"biometrictype": [
						{"biometrictypeid":"string"},
						{"biometrictype":"string"},
						{"languagecode":"string"}						
					]
				}
			]
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

# 2.3.11 ID Types Master API
# 2.3.11.1 Id Types Master-create service
Master data is required across the platform. 

This service will create the list of Id types which are used in the MOSIP platform. 

### Resource URL
### `POST /idtypes type`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
idtype|Yes|Name of the id type| | 
languagecode|Yes|Language of the id type| | 

### Example Request
```JSON
{
  "id": "string",
  "request": {
    "code": "string",
    "descr": "string",
    "isActive": true,
    "langCode": "string",
    "name": "string"
  },
  "timestamp": "2018-12-24T06:24:48.149Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
  "code": "string",
  "langCode": "string"
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.11.2 Ids Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Id. 



### Resource URL
### `GET /idtypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the language| | 
descr|Yes|Name of the language| | 


### Example Response
```JSON
{
	"idtypes": [{
			"code": "string",
			"descr": "string",
			"langCode": "string"
		},
		{
			"code": "string",
			"descr": "string",
			"langCode": "string"
		}
	]
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


# 2.3.11.3 Ids Master-get service
Master data is required across the platform. 

This service will provides the service for the List of id types based on language. 



### Resource URL
### `GET /idtypes/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the language| | 
descr|Yes|Name of the language| | 


### Example Response
```JSON
{
	"idtypes": [{
			"code": "string",
			"descr": "string",
			"langCode": "string"
		},
		{
			"code": "string",
			"descr": "string",
			"langCode": "string"
		}
	]
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

# 2.3.12 Application Types Master API
# 2.3.12.1 ApplicationTypes Master-create service
Master data is required across the platform. 

This service will create the list of ApplicationTypes which are used in the MOSIP platform. 

### Resource URL
### `POST /applicationtypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicationtypetype|Yes|Array of applicationtype| | 

### Example Request
```JSON
{
	"id": "mosip.applicationtype.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "applicationtypes": [
		{"applicationtypetype":"string"},
		{"languagecode":"string"}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_applicationtypes": [
		{"applicationtypeid":"string"},
		{"languagecode":"string"}
  ]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.12.2 ApplicationTypess Master-get service
Master data is required across the platform. 

This service will provides the service for the List of ApplicationTypes. 



### Resource URL
### `GET /applicationtypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicationtypeid|Yes|Code of the language| | 
applicationtype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "applicationtypes": [
				{ 
					"applicationtype": [
						{"applicationtypeid":"string"},
						{"applicationtypetype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"applicationtype": [
						{"applicationtypeid":"string"},
						{"applicationtypetype":"string"}
						{"languagecode":"string"}
					]
				}
			]
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


# 2.3.12.3 ApplicationTypess Master-get service
Master data is required across the platform. 

This service will provides the service for the List of ApplicationTypes. 



### Resource URL
### `GET /applicationtypes/{id}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicationtypeid|Yes|Code of the language| | 
applicationtype|Yes|Name of the language| | 


### Example Response
```JSON
{
  "applicationtypes": [
				{ 
					"applicationtype": [
						{"applicationtypeid":"string"},
						{"applicationtypetype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"applicationtype": [
						{"applicationtypeid":"string"},
						{"applicationtypetype":"string"}
						{"languagecode":"string"}
					]
				}
			]
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


# 2.3.13 Registration Centers Master API
# 2.3.13.1 Registration Centers Master-create service
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
  },
  "timestamp": "2018-12-27T18:14:54.063Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
	"id":"string"
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

# 2.3.13.2 Registration Centers Master-get service
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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# 2.3.13.3 Registration Centers Master-get service
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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# 2.3.13.5 Registration Centers Master-get holidays for a year service
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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# 2.3.13.6 Registration Centers Master-get registration center based on location code
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
```
200

Description: OK

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# 2.3.13.7 Registration Centers Master-get registration center based on coordinates
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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# 2.3.13.8 Registration Centers History Master-get service

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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found

# 2.3.13.9 Registration Centers History Master-get service

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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found


# 2.3.13.10 Registration Centers Master-get registration center based on hierarchy level, text value and language code
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
```
200

Description: Success

400

Description: Bad request

401

Description: Unauthorized

404

Description: Not Found



# 2.3.14 Biometric attributes Master API
# 2.3.14.1 Biometric attributes Master-create service

This service will create the list of Biometric attributes which are used in the MOSIP platform. 

### Resource URL
### `POST /biometricattributes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometricattribute|Yes|Array of the biometric attributes| | 

### Example Request
```JSON
{
	"id": "mosip.biometricattribute.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "biometricattributes": [
				"biometricattribute",
				"languagecode":"string"
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_biometricattributes": [
		{"biometricatributeid":"string"}
		{"languagecode":"string"}
  ]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.14.2 Biometrics attributes Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Biometrics. 



### Resource URL
### `GET /biometricattributes/{biometricatributeid}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometricatributeid|Yes|Code of the language| | 
biometricattribute|Yes|Name of the language| | 

### Example Response
```JSON
{
  "biometricattributes": [
				{ 
					"biometricattribute": [
						{"biometricatributeid":"string"},
						{"biometricattribute":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"biometricattribute": [
						{"biometricatributeid":"string"},
						{"biometricattribute":"string"},
						{"languagecode":"string"}
					]
				}
			]
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

# 2.3.14.5 Biometrics attributes Master-get based on biometric authentication type service

This service will provides the service for the List of Biometrics based on the biometric authentication type. 


### Resource URL
### `GET /getbiometricattributesbyauthtype/{languagecode}/{biometrictypeid}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
biometrictypeid|Yes|Id of the biometric auth type| | 

### Example Response
```JSON
{
  "biometricattributes": [
    {
      "code": "string",
	  "name": "string",
	  "description": "string",
      "active": true
    },
	{
	  "code": "string",
	  "name": "string",
	  "description": "string",
      "active": true
    }
  ]
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


# 2.3.15 Locations Master API
# 2.3.15.1 Locations Master-create service

### Resource URL
### `POST /locations`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the location| | 
name|Yes|Name of the location| | 
hierarchyLevel|Yes|Heirarchy level of the location| | 
hierarchyName|Yes|Hierarchy level name of the location| | 
parentLocCode|Yes|Parent location code of the location| | 
langCode|Yes|Language Code of the location| | 
isActive|Yes|Is this location active| | 


### Example Request
```JSON
{
	"id": "string",
	"ver" : "string",
	"timestamp" : "2018-12-28T10:56:55.972Z",
	"request": {
                      "code": "string",
                      "hierarchyLevel": 0,
                      "hierarchyName": "string",
                      "isActive": true,
                      "langCode": "string",
                      "name": "string",
                      "parentLocCode": "string"
  }
}
```
### Example Response
```JSON
{
	
  "code": "string",
  "isActive": true,
  "parentLocCode": "string"

}
```
### Response codes
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

# 2.3.15.2 Locations Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Locations. 



### Resource URL
### `GET /locations/{langcode}`

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
    "locations": [
        {
            "locationHierarchylevel": number,
            "locationHierarchyName": "string",
            "isActive":true
        },
        {
           "locationHierarchylevel": number,
           "locationHierarchyName": "string",
           "isActive":true
        }
    ]
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

500

Description: Internal Server Error


# 2.3.15.3 Locations Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Locations. 



### Resource URL
### `GET /locations/{locationcode}/{languagecode}`

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
  "locations": [
		{
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean",
			
		},
		{
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean",
			
		}
	]
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


# 2.3.16 Packet Rejection Reasons Master API
# 2.3.16.1 Packet Rejection Reasons Master-create service

This service will create the list of Packet Rejection Reasons which are used in the MOSIP platform. 

### Resource URL
### `POST /packetrejectionreasons`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetrejectionreasondesc|Yes|Name of the packet rejection reason| | 

### Example Request
```JSON
{
	"id": "mosip.packetrejectionreason.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
		"reason_category" : [
			{
				"code":"string",
				"name":"string",
				"desc":"string",
				"lang_code":"string", 
				"reason_lists" : [
					{
						"code":"string",
						"name":"string",
						"desc":"string",
						"lang_code":"string"
					},
					{
						"code":"string",
						"name":"string",
						"desc":"string",
						"lang_code":"string"
					}
				]
			}
		]	
	}
}
```
### Example Response
```JSON
	{
		"reason_category" : [
			{
				"code":"string",
				"lang_code":"string", 
				"reason_lists" : [
					{
						"code":"string",
						"lang_code":"string"
					},
					{
						"code":"string",
						"lang_code":"string"
					}
				]
			}
		]	
	}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.16.4 Packet Rejection Reasons Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Packet Rejection Reasons.



### Resource URL
### `GET /packetrejectionreasons`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetrejectionreasonid|Yes|Code of the language| | 
packetrejectionreasondesc|Yes|Name of the language| | 


### Example Response
```JSON
{
	"reason_category" : [
		{
			"code":"string",
			"name":"string",
			"desc":"string",
			"lang_code":"string", 
			"reason_lists" : [
				{
					"code":"string",
					"name":"string",
					"desc":"string",
					"lang_code":"string"
				},
				{
					"code":"string",
					"name":"string",
					"desc":"string",
					"lang_code":"string"
				}
			]
		}
	]	
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


# 2.3.16.5 Packet Rejection Reasons Master-get based on id and language service

This service will provides the service for the List of Packet Rejection Reasons. 


### Resource URL
### `GET /packetrejectionreasons/{reasoncategorycode}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetrejectionreasonid|Yes|Code of the language| | 
packetrejectionreasondesc|Yes|Name of the language| | 


### Example Response
```JSON
{
	"reason_category" : {
		"code":"string",
		"name":"string",
		"desc":"string",
		"lang_code":"string", 
		"reason_lists" : [
			{
				"code":"string",
				"name":"string",
				"desc":"string",
				"lang_code":"string"
			},
			{
				"code":"string",
				"name":"string",
				"desc":"string",
				"lang_code":"string"
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


# 2.3.16.6 Packet Rejection Reasons Master-get based on id, language and location code service

This service will provides the service for the List of Packet Rejection Reasons based on id, language and location code. 


### Resource URL
### `GET /packetrejectionreasons/{id}/{languagecode}/{locationcode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetrejectionreasonid|Yes|Code of the language| | 
packetrejectionreasondesc|Yes|Name of the language| | 


### Example Response
```JSON
{
  "packetrejectionreasons": [
				{ 
						"packetrejectionreasonid":"string",
						"packetrejectionreasondesc":"string",
						"languagecode":"string",
						"locationcode":"string"
				}, 
				{ 
						"packetrejectionreasonid":"string",
						"packetrejectionreasondesc":"string",
						"languagecode":"string"
						"locationcode":"string"
				}
			]
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


# 2.3.17 Packet On-hold Reasons Master API
# 2.3.17.1 Packet On-hold Reasons Master-create service

This service will create the list of Packet On-hold Reasons which are used in the MOSIP platform. 

### Resource URL
### `POST /packetonholdreasons`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetonholdreasondesc|Yes|Name of the packet rejection reason| | 

### Example Request
```JSON
{
	"id": "mosip.packetonholdreason.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "packetonholdreasons": [
			{ 
				"packetonholdreasondesc":"string",
				"languagecode":"string"
			}, 
			{ 
				"packetonholdreasondesc":"string",
				"languagecode":"string"
			}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_packetonholdreasons": [
			{ 
				"packetonholdreasonid":"string"
			}, 
			{ 
				"packetonholdreasonid":"string"
			}
  ]
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.17.4 Packet On-hold Reasons Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Packet On-hold Reasons.



### Resource URL
### `GET /packetonholdreasons`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetonholdreasonid|Yes|Code of the language| | 
packetonholdreasondesc|Yes|Name of the language| | 


### Example Response
```JSON
{
  "packetonholdreasons": [
				{ 
					"packetonholdreasonid":"string",
					"packetonholdreasondesc":"string",
					"languagecode":"string"
				}, 
				{ 
					"packetonholdreasonid":"string",
					"packetonholdreasondesc":"string",
					"languagecode":"string"
				}
			]
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


# 2.3.17.5 Packet On-hold Reasons Master-get based on id and language service

This service will provides the service for the List of Packet On-hold Reasons. 


### Resource URL
### `GET /packetonholdreasons/{id}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
packetonholdreasonid|Yes|Code of the language| | 
packetonholdreasondesc|Yes|Name of the language| | 


### Example Response
```JSON
{
  "packetonholdreasons": [
				{ 
						"packetonholdreasonid":"string",
						"packetonholdreasondesc":"string",
						"languagecode":"string"
				}, 
				{ 
						"packetonholdreasonid":"string",
						"packetonholdreasondesc":"string",
						"languagecode":"string"
				}
			]
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

# 2.3.18 Documents Types API

# 2.3.18.1 Documents Type Master-create service

This service will create the list of Documents types which are used in the MOSIP platform. There is another service to map the document category and document type.

### Resource URL
### `POST /documenttype`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of document type| | 
name|Yes|Name of the document type| | 
descr|Yes|Description of the document type| | 
lang_code|Yes|Language code of the document type| | 

### Example Request
```JSON
{
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	]
}
```
### Example Response
```JSON
{
  "successfully_created_documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	]
}
```

# 2.3.18.2 Documents Type Master-update service

This service will update the list of Documents types which are used in the MOSIP platform. 

### Resource URL
### `PUT /documenttype`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of document type| | 
name|Yes|Name of the document type| | 
descr|Yes|Description of the document type| | 
lang_code|Yes|Language code of the document type| | 

### Example Request
```JSON
{
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	]
}
```
### Example Response
```JSON
{
  "successfully_updated_documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	]
}
```

# 2.3.18.3 Documents Category-delete service
Master data is required across the platform. 

This service will deletes a list of Document Categories from the Documents Category master module. 

### Resource URL
### `DELETE /documenttypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|Code of the document type| | 


### Example Request
```JSON
{
  "documentcodes": ["PSPRT","DRVNGLCNC","RNTLAGRMNT","POB"]
}
```
### Example Response
```JSON
{
  "successfully_deleted_documentcodes": ["PSPRT","DRVNGLCNC","RNTLAGRMNT","POB"]
}
```

# 2.3.18.4 Document Types Master-get service

This service will provides the service for the List of documents types. 

### Resource URL
### `GET /documentcategorytypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
```JSON
-NA-
```
### Example Response
```JSON
{
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
	]
}
```

# 2.3.19 Machine Types Master API
# 2.3.19.1 Machines Types Master-create service

This service will create the list of Machine types which are used in the MOSIP platform. 

### Resource URL
### `POST /machinetypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machinetypecode|Yes|Code of the machine type| | 
machinename|Yes|Name of the machine type| | 
description|Yes|Description of the machine type| | 
languagecode|Yes|Language code of the machine type| | 
isactive|Yes|Is the machine type active?| | 

### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-24T05:27:49.183Z",
  "request": {
    "code": "string",
    "description": "string",
    "isActive": true,
    "langCode": "string",
    "name": "string"
  }
}
```
### Example Response
```JSON
{
  "code": "string",
  "langCode": "string"
}
```
### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.19.2 Machine types Master-get service

This service will provides the service to fetch the complete List of machine types with the machine details. 

### Resource URL
### `GET /machinetypes`

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
  "machinetypes": [
				{ 
					"machinetypecode":"string",
					"machinename":"string",	
					"description":"string",
					"languagecode":"boolean",
					"isactive":"string" 
				}, 
				{ 
					"machinetypecode":"string",
					"machinename":"string",	
					"description":"string",
					"languagecode":"boolean",
					"isactive":"string" 
				}
			]
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


# 2.3.19.3 Machine types Master-get machines based on language

This service will provides the service to fetch the List of machines with the machine details based on the language code.

### Resource URL
### `GET /machinetypes/{languagecode}`

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
  "machines": [
				{ 
					"machinetypecode":"string",
					"machinename":"string",	
					"description":"string",
					"languagecode":"boolean",
					"isactive":"string" 
				}, 
				{ 
					"machinetypecode":"string",
					"machinename":"string",	
					"description":"string",
					"languagecode":"boolean",
					"isactive":"string" 
				}
			]
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

# 2.3.20 Machine Specifications

# 2.3.20.1 Machine Specification Master-create service

This service will create a Machine Specification which are used in the MOSIP platform. 

### Resource URL
### `POST /machinespecifications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Machine Specification| | 
name|Yes|Name of the machine Specification| | 
brand|Yes|Brand of the machine specification| | 
model|Yes|Model of the machine specification| | 
mtyp_code|Yes|Machine type code of the machine specification| | 
min_driver_ver|Yes|Minimum driver version required for the machine specification| | 
descr|Yes|Description of the machine specification| | 
lang_code|Yes|Language of the machine specification| | 
is_active|Yes|Is the Machine Specification active| | 

### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-24T05:33:45.899Z",
  "request": {
    "brand": "string",
    "description": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "machineTypeCode": "string",
    "minDriverversion": "string",
    "model": "string",
    "name": "string"
  }
}
```
### Example Response
```JSON
{
  "id": "string"
}
```

# 2.3.20.2 Machine Specifications Master-update service

This service will update a Machine Specification which are used in the MOSIP platform. 


### Resource URL
### `PUT /machinespecifications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Machine Specification| | 
lang_code|Yes|Language code of the Machine Specification| | 

### Example Request
```JSON
{
  "id": "string",
  "ver": "string",
  "timestamp": "2018-12-24T05:36:25.656Z",
  "request": {
    "brand": "string",
    "description": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "machineTypeCode": "string",
    "minDriverversion": "string",
    "model": "string",
    "name": "string"
  }
}
```
### Example Response
```JSON
{
  "id": "string"
}
```


# 2.3.20.3 Machine Specifications-delete service

This service deletes a Machine Specification from the Machine Specifications master module. 

### Resource URL
### `DELETE /machinespecifications/{id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Machine Specification| | 


### Example Response
```JSON
{
  "id": "string"
}
```

# 2.3.20.4 Machine Specifications Master-get service

This service will provides the list of all Machine Specifications in all languages. 


### Resource URL
### `GET /machinespecifications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
```JSON
-NA-
```

### Example Response
```JSON
{
	"id":"KJDS9",
	"name":"Laptop",
	"brand":"Hewlett Packard",
	"model":"L34-324",
	"mtyp_code":"GEW8",
	"min_driver_ver":"1.4",
	"descr":"This is a medium configuration",
	"lang_code":"eng",
	"is_active":true
}
```


# 2.3.20.5 Machine Specifications Master-get based on language service

This service will provides the list of all Machine Specifications in a specific language. 


### Resource URL
### `GET /machinespecifications/{lang_code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
-NA-

### Example Request
```JSON
-NA-
```

### Example Response
```JSON
{
	"id":"KJDS9",
	"name":"Laptop",
	"brand":"Hewlett Packard",
	"model":"L34-324",
	"mtyp_code":"GEW8",
	"min_driver_ver":"1.4",
	"descr":"This is a medium configuration",
	"lang_code":"eng",
	"is_active":true
}
```

### Response codes
202

Description: Accepted

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

# 2.3.21 Registration Center User Machine Mapping API

## 2.3.21.1 Registration Center-User-Machine Mapping Master-create service

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
  "request": {
    "cntrId": "RC001",
    "isActive": true,
    "machineId": "MC001",
    "usrId": "QC001"
  },
  "timestamp": "2018-12-28T09:21:27.472Z",
  "ver": "string"
}
```
### Example Response
```JSON
{
  "cntrId": "RC001",
  "machineId": "MC001",
  "usrId": "QC001"
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

## 2.3.21.2 Registration Center-User-Machine Mapping Master-create service

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
  "registrationCenters": [
    {
      "cntrId": "RC001",
      "effectivetimes": "2018-12-28T10:14:49.849Z",
      "isActive": true,
      "machineId": "MC001",
      "usrId": "QC001"
    }
  ]
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

# 2.3.22 Registration Center Machine API
## 2.3.22.1 Registration Center Machine-create service
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
  "id": "mosip.registrationCenterMachine.create",
  "ver": "1.0",
  "timestamp": "2018-12-28T09:26:22.886Z",
  "request": {
    "isActive": true,
    "machineId": "string",
    "regCenterId": "string"
  }
}


```
### Example Response
```JSON
  {
  "machineId": "string",
  "regCenterId": "string"
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

## 2.3.22.2 Registration Center Machine Mapping Master-delete service

This service will provides the service for delete mapping of  Center-Machine. 


### Resource URL
### `DELETE/registrationcentermachine/{regCenterId}/{machineId}`

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
  "machineId": "MC001",
  "regCenterId": "RC001"
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

# 2.3.23 Registration Center Device API
## 2.3.22.1 Registration Center Device-create service
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
  "id": "mosip.registrationCenterDevice.create",
  "ver": "1.0",
  "timestamp": "2018-12-28T09:26:22.886Z",
  "request": {
    "isActive": true,
    "deviceId": "string",
    "regCenterId": "string"
  }
}


```
### Example Response
```JSON
  {
  "deviceId": "string",
  "regCenterId": "string"
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

## 2.3.23.2 Registration Center Device Mapping Master-delete service

This service will provides the service for delete mapping of  Device-Machine. 


### Resource URL
### `DELETE/registrationcenterdevice/{regCenterId}/{deviceId}`

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
  "deviceId": "DV001",
  "regCenterId": "RC001"
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

# 2.3.24 Registration Center Machine Device API
## 2.3.24.1 Registration Center Machine Device-create service
Master data is required across the platform. 

This service will create the mapping of registration canter, machine and device in the RegistrationCenterMachineDevice Master module. 

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
  "id": "mosip.registrationCenterMachineDevice.create",
  "ver": "1.0",
  "timestamp": "2018-12-28T09:26:22.886Z",
  "request": {
    "deviceId": "string",
    "isActive": true,
    "machineId": "string",
    "regCenterId": "string"
  }
}


```
### Example Response
```JSON
  {
   "deviceId": "string",
   "machineId": "string",
   "regCenterId": "string"
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


