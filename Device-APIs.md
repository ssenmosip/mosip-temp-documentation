This section details about the service APIs in the Document modules


* [Devices API](#devices-master-api)

* [Device Types API](#device-types-master-api)

* [Device Specifications API](#device-specifications)


# Devices Master API

* [POST /devices](#post-devices)
* [GET /devices]/{languagecode}(#get-devices)
* [GET /devices/{languagecode}/{deviceType}](#get-deviceType-languagecode)
* [PUT /devices](#put-devices)
* [DELETE /devices/{id}](#delete-devices-id)

# POST /devices

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request" : {
		"devices": {
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
	     "successfully_created_devices": {
			                     "deviceid": "string"
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

# GET /devices/{languagecode}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    } ],
  "response": {
	"devices": [{
			"deviceSpecId": "string",
                        "id": "string",
                        "ipAddress": "string",
                        "isActive": true,
                        "langCode": "string",
                        "macAddress": "string",
                        "name": "string",
                        "serialNum": "string",
                        "validityDateTime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'"
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


# GET /devices/{languagecode}/{deviceType}

This service will provides the service for the List of devices. 


### Resource URL
### `GET /devices/{languagecode}/{deviceType}`

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
	"devices": [{
			 "deviceSpecId": "string",
                         "deviceTypeCode": "string",
                         "id": "string",
                         "ipAddress": "string",
                         "isActive": true,
                         "langCode": "string",
                         "macAddress": "string",
                         "name": "string",
                         "serialNum": "string",
                         "validityEndDateTime": "2019-04-05T09:30:13.608Z"
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

# PUT /devices

This service will update existing device. 


### Resource URL
### `PUT /devices`

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
                 "id": "string"
             }
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

# DELETE /devices/{id}

This service will delete the devices. 

### Resource URL
### `DELETE /devices/{id}`

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
               "id": "string"
            }
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



# Device Types Master API

* [POST /devicetypes](#post-devicetypes)

## POST /devicetypes

This service will create the list of Device types which are used in the MOSIP platform. 

### Resource URL
### `POST /devicetypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
devicetypecode|Yes|Code of the device type| | 
devicename|Yes|Name of the device type| | 
description|Yes|Description of the device type| | 
languagecode|Yes|Language code of the device type| | 
isactive|Yes|Is the device type active?| | 

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
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
  "response":{
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



# Device Specifications

* [POST /devicespecifications](#post-devicespecifications)
* [PUT /devicespecifications](#put-devicespecifications)
* [DELETE /devicespecifications/{id}](#delete-devicespecifications-id)
* [GET /devicespecifications/{langcode}/{devicetypecode}](#get-devicespecifications-langcode-devicetypecode)
* [GET /devicespecifications/{lang_code}](#get-devicespecifications-lang_code)

# POST /devicespecifications

This service will create a Device Specification which are used in the MOSIP platform. 

### Resource URL
### `POST /devicespecifications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Device Specification| | 
name|Yes|Name of the Device Specification| | 
brand|Yes|Brand of the Device specification| | 
model|Yes|Model of the Device specification| | 
dtyp_code|Yes|device type code of the Device specification| | 
min_driver_ver|Yes|Minimum driver version required for the Device specification| | 
descr|Yes|Description of the Device specification| | 
lang_code|Yes|Language of the Device specification| | 
is_active|Yes|Is the Device Specification active| | 

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
    "DeviceTypeCode": "string",
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

# PUT /devicespecifications

This service will update a Device Specification which are used in the MOSIP platform. 


### Resource URL
### `PUT /devicespecifications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Device Specification| | 
lang_code|Yes|Language code of the Device Specification| | 

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
    "deviceTypeCode": "string",
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

# DELETE /devicespecifications/{id}

This service deletes a Device Specification from the Device Specifications master module. 

### Resource URL
### `DELETE /devicespecifications/{id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|ID of the Device Specification| | 


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

# GET /devicespecifications/{langcode}/{devicetypecode}

This service will provides the list of all Device Specifications for specified language code and device type code . 


### Resource URL
### `GET /devicespecifications/{langcode}/{devicetypecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
lang_code|Yes|Language code of the Device Specification| |
dtyp_code|Yes|device type code of the Device specification| | 

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
  "devicespecifications": [
    {
      "brand": "string",
      "description": "string",
      "deviceTypeCode": "string",
      "id": "string",
      "isActive": true,
      "langCode": "string",
      "minDriverversion": "string",
      "model": "string",
      "name": "string"
    }
  ]
}
}

```


# GET /devicespecifications/{lang_code}

This service will provides the list of all Device Specifications in a specific language. 


### Resource URL
### `GET /devicespecifications/{lang_code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
lang_code|Yes|Language code of the Device Specification| |

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
  "response" : {
  "devicespecifications": [
    {
      "brand": "string",
      "description": "string",
      "deviceTypeCode": "string",
      "id": "string",
      "isActive": true,
      "langCode": "string",
      "minDriverversion": "string",
      "model": "string",
      "name": "string"
    }
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



