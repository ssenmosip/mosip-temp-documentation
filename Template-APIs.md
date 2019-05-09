This section details about the service APIs in the template modules

* [Template Master API](#template-api)

* [Template Types Master API](#template-types-api)

# Template API

* [POST /templates](#post-templates)
* [PUT /templates](#put-templates)
* [DELETE /templates/{id}](#delete-templates-id)

# POST /templates

This service will create the list of Template  which are used in the MOSIP platform. 

### Resource URL
### `POST /templates`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|id of temlate | | 
descr|Yes|Description of the temlate | | 
lang_code|Yes|Language code of the temlate | | 
isActive |Yes|is active or not| |
moduleId |Yes| Id of modul | |
templateTypeCode |Yes| Id of template type | |
fileFormatCode | Yes | Code of file formate| |

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
    "description": "string",
    "fileFormatCode": "string",
    "fileText": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "model": "string",
    "moduleId": "string",
    "moduleName": "string",
    "name": "string",
    "templateTypeCode": "string"
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
  "response":  {
     "id": "string"
  }
}
```
# PUT /templates

This service will update the list of Template  which are used in the MOSIP platform. 

### Resource URL
### `PUT /templates`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|id of temlate | | 
lang_code|Yes|Language code of the temlate | | 
isActive |Yes|is active or not| |
moduleId |Yes| Id of modul | |
templateTypeCode |Yes| Id of template type | |
fileFormatCode | Yes | Code of file formate| |

### Example Request
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
    "description": "string",
    "fileFormatCode": "string",
    "fileText": "string",
    "id": "string",
    "isActive": true,
    "langCode": "string",
    "model": "string",
    "moduleId": "string",
    "moduleName": "string",
    "name": "string",
    "templateTypeCode": "string"
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

# DELETE /templates/{id}
Master data is required across the platform. 

This service will deletes a list of Template from the Template master module. 

### Resource URL
### `DELETE /templates/{id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Yes|id of the Template| 



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
  "response"  : {
      "id": "string"
  }
}
```

# Template Types API

* [GET /templatetype/{code}](#get-templatetype-code)

# GET /templatetype/{code}

This service fetches the template types irrespective of the language. The service returns the results in all the languages. 


### Resource URL
### `GET /templatetype/{code}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
code|Yes|This is the template code field|-NA-|auth-email-content

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
		"code": "string",
		"descr": "string",
		"langCode": "string",
		"isactive": boolean
	} 
}
```

### Response codes
200

Description: Success
