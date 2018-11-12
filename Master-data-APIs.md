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
	"request" : { "holidayList":[
		  { "holidayDate": "string", "holidayName": "string", "languagecode": "string" },
		  { "holidayDate": "string", "holidayName": "string", "languagecode": "string" },
		  { "holidayDate": "string", "holidayName": "string", "languagecode": "string" }
		]
	}
}  
```
### Example Response
```JSON
{ "successfully_created_holidayList":[
	  { "holidayID": "string" },
	  { "holidayID": "string" },
	  { "holidayID": "string" }
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


## 2.3.1.3 Holiday Master-get by id and language code service

This service will provides the service for the List of holidays based on the holiday ID
It will also ensure audit data stored is archived based on the defined archival policy.

### Resource URL
### `GET /holidays/{holidayid}/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
holidayid|Yes|Id of the holiday| | id123
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
documentcategories|Yes|List of document categories| | 

### Example Request
```JSON
{
	"id": "mosip.documentcategories.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" :{
	  "documentcategories": [
			{ "documentscategory":"POA", "languagecode":"string" },
			{ "documentscategory":""POI", "languagecode":"string" },
			{ "documentscategory":""POR", "languagecode":"string" },
			{ "documentscategory":""POB", "languagecode":"string" }
		]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_documentcategories": [
				{ "categoryid":"id" },
				{ "categoryid":"id" },
				{ "categoryid":"id" },
				{ "categoryid":"id" }
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
	"id": "mosip.machine.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "machines": [
			{ 
				"machine": [
					{"machinename":"string"},
					{"macid":"string"},	
					{"serialnumber":"string"},
					{"isactive":"boolean"},
					{"languagecode":"string" }					
				]
			}, 
			{ 
				"machine": [
					{"machinename":"string"},
					{"macid":"string"},	
					{"serialnumber":"string"},
					{"isactive":"boolean"}
					{"languagecode":"string" }
				]
			}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_machines": [
		{ 
			"machine": [
				{"machineid":"string"}
			]
		}, 
		{ 
			"machine": [
				{"machineid":"string"}
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
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
						{"languagecode":"string"}
				]
				}, 
				{ 
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
						{ "languagecode":"string" }
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


# 2.3.5.3 Machines Master-get machines based on language and id service
Master data is required across the platform. 

This service will provides the service to fetch the List of machines with the machine details based on the language and the machine id.

### Resource URL
### `GET /machines/{id}/{languagecode}`

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
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
						{"languagecode":"string"}
				]
				}, 
				{ 
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
						{ "languagecode":"string" }
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
-NA-


### Example Response
```JSON
{
  "machines": [
				{ 
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
						{"languagecode":"string"}
				]
				}, 
				{ 
					"machine": [
						{"machineid":"string"},
						{"machinename":"string"},
						{"macid":"string"},	
						{"serialnumber":"string"},
						{"isactive":"boolean"}
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

# 2.3.7 Languages Master API
# 2.3.7.1 Languages Master-create service

This service will create the list of Languages which are used in the MOSIP platform. 

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
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "languages": [
			{ 
				"language": [
					{"languagecode":"string"},
					{"languagename":"string"}
				]
			}, 
			{ 
				"language": [
					{"languagecode":"string"},
					{"languagename":"string"}
				]
			}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_languages": [
		{ 
			"language": [
				{"languageid":"string"}
			]
		}, 
		{ 
			"language": [
				{"languageid":"string"}
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
```JSON
{
	"id": "mosip.language.get",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
		{"languagecode":"string"},
		{"languagename":"string"}
	}
}
```

### Example Response
```JSON
{
  "languages": [
				{ 
					"language": [
						{"languagecode":"string"},
						{"languagename":"string"}
					]
				}, 
				{ 
					"language": [
						{"languagecode":"string"},
						{"languagename":"string"}
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

# 2.3.8 Gender Master API
# 2.3.8.1 Gender Master-create service

This service will create the list of Gender which are used in the MOSIP platform. 

### Resource URL
### `POST /genders`

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
	"id": "mosip.gender.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "genders": [
			{ 
				"gender": [
					{"gendertype":"string"},
					{"languagecode":"string"}					
				]
			}, 
			{ 
				"gender": [
					{"gendertype":"string"},
					{"languagecode":"string"}
				]
			}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_genders": [
		{ 
			"gender": [
				{"genderid":"string"}
			]
		}, 
		{ 
			"gender": [
				{"genderid":"string"}
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

# 2.3.8.4 Genders Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Genders. 



### Resource URL
### `GET /genders`

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
  "genders": [
				{ 
					"gender": [
						{"genderid":"string"},
						{"gendertype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"gender": [
						{"genderid":"string"},
						{"gendertype":"string"}
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


# 2.3.8.5 Genders Master-get based on id and language service

This service will provides the service for the List of Genders. 


### Resource URL
### `GET /genders/{id}/{languagecode}`

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
  "genders": [
				{ 
					"gender": [
						{"genderid":"string"},
						{"gendertype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"gender": [
						{"genderid":"string"},
						{"gendertype":"string"}
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

# 2.3.9 Titles Master API
# 2.3.9.1 Title Master-create service
Master data is required across the platform. 

This service will create the list of Title which are used in the MOSIP platform. 

### Resource URL
### `POST /titles`

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
	"id": "mosip.title.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "titles": [
			{ 
				"title": {
					"titletype":"string",
					"languagecode":"string"
				]
			}, 
			{ 
				"title": {
					"titletype":"string",
					"languagecode":"string"
				]
			}
	  ]
	}
}
```
### Example Response
```JSON
{
	  "titles": [
			{ 
				"title": {
					"titletype":"string",
					"languagecode":"string"
				]
			}, 
			{ 
				"title": {
					"titletype":"string",
					"languagecode":"string"
				]
			}
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

# 2.3.9.2 Titles Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Titles. 



### Resource URL
### `GET /titles`

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
  "titles": [
				{ 
					"title": [
						{"titleid":"string"},
						{"titletype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"title": [
						{"titleid":"string"},
						{"titletype":"string"},
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


# 2.3.9.3 Titles Master-get based on id and language service
Master data is required across the platform. 

This service will provides the service for the List of Titles. 



### Resource URL
### `GET /titles/{id}/{languagecode}`

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
  "titles": [
				{ 
					"title": [
						{"titleid":"string"},
						{"titletype":"string"},
						{"languagecode":"string"}
					]
				}, 
				{ 
					"title": [
						{"titleid":"string"},
						{"titletype":"string"},
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
	"id": "mosip.idtype.create",
	"ver": "1.0",
	"timestamp": "",
	"request": {
		"idtypes": [{
				"idtype": "string",
				"languagecode": "string"
			},
			{
				"idtype": "string",
				"languagecode": "string"
			}
		]
	}
}
```
### Example Response
```JSON
{
	"idtypes": [
                {
			"idtype": "string",
			"languagecode": "string"
		},
		{
			"idtype": "string",
			"languagecode": "string"
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
			"languagecode": "string"
		},
		{
			"code": "string",
			"descr": "string",
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
			"languagecode": "string"
		},
		{
			"code": "string",
			"descr": "string",
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
longitude|Yes|Longitude of the registration center| | 
latitude|Yes|Latitude of the registration center| | 
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
	"id": "mosip.registrationcenter.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "registrationcenters": [
		{
			"registrationcentername":"string",
			"longitude":"string",
			"latitude":"string",
			"isactive":"boolean",
			"centertype":"string",
			"address":"string",
			"workinghours":"string",
			"contactnumber":"string",
			"pincode":"string",
			"languagecode":"string"
		}
	  ]
	}
}
```
### Example Response
```JSON
{
  "registrationcenters": [
	{
		"registrationcenterid":"string"
	},
	{
		"registrationcenterid":"string"
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
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
		"languagecode":"string"
	},
	{
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
		"languagecode":"string"
	},
	{
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
### `GET /getlocspecificregistrationcenters/{languagecode}/{locationcode}`

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
  "registrationcenter": [
	{
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
		"languagecode":"string"
	},
	{
		"registrationcenterid":"string",
		"registrationcentername":"string",
		"longitude":"string",
		"latitude":"string",
		"isactive":"boolean",
		"centertype":"string",
		"address":"string",
		"workinghours":"string",
		"contactnumber":"string",
		"pincode":"string",
		"locationcode":"string",
		"stateon":"date",
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
hierarchylevel|Yes|Heirarchy level of the location| | 
hierarchylevelname|Yes|Hierarchy level name of the location| | 
parentloccode|Yes|Parent location code of the location| | 
langcode|Yes|Language Code of the location| | 
isactive|Yes|Is this location active| | 

### Example Request
```JSON
{
	"id": "mosip.location.create",
	"ver" : "1.0",
	"timestamp" : "",
	"request" : {
	  "locations": [
			{
				"code":"string",
				"name":"string",
				"hierarchylevel":"number",
				"hierarchylevelname":"string",
				"parentloccode":"",
				"langcode":"string",
				"isactive":"boolean",
				"languagecode":"string"
			}
	  ]
	}
}
```
### Example Response
```JSON
{
  "successfully_created_locations": [
			"locationcode":"string"
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

# 2.3.15.2 Locations Master-get service
Master data is required across the platform. 

This service will provides the service for the List of Locations. 



### Resource URL
### `GET /locations`

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
			"hierarchylevel":"number",
			"hierarchylevelname":"string",
			"parentloccode":"",
			"langcode":"string",
			"isactive":"boolean",
			"languagecode":"string"
		},
		{
			"code":"string",
			"name":"string",
			"hierarchylevel":"number",
			"hierarchylevelname":"string",
			"parentloccode":"",
			"langcode":"string",
			"isactive":"boolean",
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
			"hierarchylevel":"number",
			"hierarchylevelname":"string",
			"parentloccode":"",
			"langcode":"string",
			"isactive":"boolean",
			"languagecode":"string"
		},
		{
			"code":"string",
			"name":"string",
			"hierarchylevel":"number",
			"hierarchylevelname":"string",
			"parentloccode":"",
			"langcode":"string",
			"isactive":"boolean",
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

