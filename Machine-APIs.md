This section details about the service APIs in the Document modules


* [Machines API](#machines-master-api)

* [Machine Types Master API](#machine-types-master-api)

* [Machine Specifications API](#machine-specifications)


# Machines Master API

* [POST /machines](#post-machines)
* [GET /machines](#get-machines)
* [GET /machines/{languagecode}](#get-machineslanguagecode)
* [GET /machineshistory/{id}/{languagecode}/{eff_dtimes}](#get-machineshistoryidlanguagecodeeff_dtimes)
* [DELETE /machines/{id}](#delete-machinesid)
* [PUT /machines](#put-machines)


# POST /machines

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
             "errorCode": "string",
             "message": "string"
            }],
 "response": {
               "id": "string"
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

# GET /machines

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
            "errorCode": "string",
            "message": "string"
            }],
  "response": {
               "machines": [{
                            "id": "string",
                            "ipAddress": "string",
                            "isActive": true,
                            "langCode": "string",
                            "macAddress": "string",
                            "machineSpecId": "string",
                            "name": "string",
                            "serialNum": "string",
                            "validityDateTime": "2018-12-24T05:54:42.097Z"
                           }]
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


# GET /machines/{languagecode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
            "errorCode": "string",
            "message": "string"
            }],
  "response": {
              "machines": [{
                           "id": "string",
                           "ipAddress": "string",
                           "isActive": true,
                           "langCode": "string",
                           "macAddress": "string",
                           "machineSpecId": "string",
                           "name": "string",
                           "serialNum": "string",
                           "validityDateTime": "2018-12-24T05:58:03.286Z"
                          }]
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


# GET /machineshistory/{id}/{languagecode}/{eff_dtimes}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
 "response": {
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

# DELETE /machines/{id}

This service will delete the machines. 

### Resource URL
### `DELETE /machines/{id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineId|Yes|The machineId| | 

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
              "id": "string"
             }
}
```
200

Description: When Machine deleted successfully

204

Description: No Content

401

Description: Unauthorized

403
	
Description: Forbidden

404

Description: When machine not found

500

Description: Error occurred while deleting Machine

# PUT /machines

This service will update existing machines. 


### Resource URL
### `PUT /machines`

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
               "machineSpecId": "string",
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
"response": {
               "id": "string"
            }
}
```
### Response codes
200

Description: When machine updated successfully

201

Description: Created

400

Description: When Request body passed is null or invalid

401

Description: Unauthorized

403

Description: Forbidden

404

Description: When Machine is not found

500

Description: While updating machine any error occurred


# Machine Types Master API

* [POST /machinetypes](#post-machinetypes)
* [GET /machinetypes](#get-machinetypes)
* [GET /machinetypes/{languagecode}](#get-machinetypeslanguagecodee)

# POST /machinetypes

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
            "code": "string",
            "langCode": "string"
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

# GET /machinetypes

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
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


# GET /machinetypes/{languagecode}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
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


# Machine Specifications

* [POST /machinespecifications](#post-machinespecifications)
* [PUT /machinespecifications](#put-machinespecifications)
* [DELETE /machinespecifications/{id}](#delete-machinespecificationsid)
* [GET /machinespecifications](#get-machinespecifications)
* [GET /machinespecifications/{lang_code}](#get-machinespecificationslang_code)


# POST /machinespecifications

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
              "id": "string"
               }
}
```

# PUT /machinespecifications

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
             "id": "string"
             }
}
```


# DELETE /machinespecifications/{id}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
                "id": "string"
              }
 }
```

# GET /machinespecifications

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":  {
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
}
```


# GET /machinespecifications/{lang_code}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":   {
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


