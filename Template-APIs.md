This section details about the service APIs in the template modules

* [Templates API](#template-api)

* [Template Types API](#template-types-api)

* [Template- Search API](#post-templatessearch)

* [Template- Filter values](#post-templatesfiltervalues)

# Template API

* [POST /templates](#post-templates)
* [PUT /templates](#put-templates)
* [DELETE /templates/{id}](#delete-templatesid)

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
  "errors": null,
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
  "errors": null,
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



### Success Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": null,
  "response"  : {
      "id": "string"
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
  "response":  null
}
```

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-045 | Error occurred while fetching Templates | Fetch Issue
KER-MSD-145 | Exception during inserting data into db | Insertion Issue
KER-MSD-046 | Template not found. | Data Not Found
KER-MSD-095 | Error occurred while updating Template | Update Issue
KER-MSD-096 | Error occurred while deleting Template | Delete Issue

# Template Types API

* [GET /templatetype/{code}](#get-templatetypecode)

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

#### Failure details
Error Code | Error Message | Error Description
------------|------------------------------|-------------
KER-MSD-072 | Error occurred while inserting Template Type details into db | Insertion Issue




### Resource URL
### `POST /template/search`

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
type|No|The value have to be in ["in","equals","startsWith","between"]| -NA- |
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
  "templates": [
      {
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
    ],
	"fromRecord" : "number",
	"toRecord":"number",
	"totalRecord":"number"
 }
}
```
# Templatefilter values

* [POST /template/filtervalues](#post-templatefiltervalues)

# POST /template/filtervalues

This service returns the filter values which are required in the dropdown entries of the filter screen.  

### Resource URL
### `POST /template/filtervalues`

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
		"fieldValue": "string"
	}
   ]
 }
}
```