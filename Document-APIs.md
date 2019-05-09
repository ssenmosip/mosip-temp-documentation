This section details about the service APIs in the Document modules


* [Documents Categories API](#documents-category-master-api)

* [Document Formats API](#document-formats-master-api)

* [Documents Types API](#documents-types-api)

* [Valid Documents API](#valid-documents-api)



# Documents Category Master API

* [POST /documentcategories](#post-documentcategories)
* [PUT /documentcategories](#put-documentcategories)
* [GET /documentcategories](#get-documentcategories)
* [GET /documentcategories/{code}/{langcode}](#get-documentcategories-code-langcode)
* [GET /documentcategories/{languagecode}](#get-documentcategories-languagecode)
* [DELETE /documentcategories/{code}](#get-documentcategories-code)

# POST /documentcategories

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
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden
-----
This service will create the list of Documents Category which are used in the MOSIP platform. 

### Resource URL
### `PUT /documentcategories`

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
201

Description: Created

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden

404 

Description: Not Found


-----
# GET /documentcategories

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
             "errorCode": "string",
             "message": "string"
    }], 
  "response": {
             "documentcategories": [
                                      {
		                      "code": "string",
                                      "description": "string",
                                      "isActive": true,
                                      "langCode": "string",
                                      "name": "string"
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

# GET /documentcategories/{code}/{langcode}

This service will provides the service for the List of documents categories. 


### Resource URL
### `GET /documentcategories/{code}/{langcode}`

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
               "documentcategories": [
		                        { 
                                          "code": "string",
                                          "description": "string",
                                          "isActive": true,
                                          "langCode": "string",
                                          "name": "string"
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


# GET /documentcategories/{langcode} 

This service will provides the service for the List of documents categories based on the passed langcode. 


### Resource URL
### `GET /documentcategories/{langcode}`

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
	"documentcategories": [{
		                 "code": "string",
                                 "description": "string",
                                 "isActive": true,
                                 "langCode": "string",
                                 "name": "string"
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
------
# DELETE /documentcategories/{code} 

This service will provides the service to delete documents categories based on the passed given code. 


### Resource URL
### `DELETE /documentcategories/{code}`

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
		 "code": "string"
              }
}
```
204

Description: No Content

401

Description: Unauthorized

404 

Description: Not Found



# Document formats Master API

* [POST /documentformats](#post-documentformats)
* [GET /documentformats](#get-documentformats)
* [GET /documentformats/{id}/{languagecode}](#get-documentformats-id-languagecode)

# POST /documentformats
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request" : {
	  "documentformats": [
			          { "documentformat":"pdf", "languagecode":"string" },
			          { "documentformat":"png", "languagecode":"string" },
			          { "documentformat":"jpeg", "languagecode":"string"},
			          { "documentformat":"gif", "languagecode":"string" }
		           ]
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
  "successfully_created_documentformats": [
		                             {"documentformatid":id },
		                             {"documentformatid":id },
		                             {"documentformatid":id },
		                             {"documentformatid":id }  
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

# GET /documentformats
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
             "documentformats": [
			         {"id":"id", "format": "pdf" ,"languagecode":"string"},
			         {"id":"id", "format": "png" ,"languagecode":"string"},
			         {"id":"id", "format": "jpeg" ,"languagecode":"string"},
			         {"id":"id", "format": "gif" ,"languagecode":"string"}
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

# GET /documentformats/{id}/{languagecode}

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
 "response": {
             "documentformats": [
			           {"id":"id", "format": "pdf" ,"languagecode":"string"},
			           {"id":"id", "format": "png" ,"languagecode":"string"},
			           {"id":"id", "format": "jpeg" ,"languagecode":"string"},
			           {"id":"id", "format": "gif" ,"languagecode":"string"}
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


# Documents Types API

* [POST /documenttype](#post-documenttype)
* [PUT /documenttype](#put-documenttype)
* [GET /documenttypes/{documentcategorycode}/{langcode}](#get-documenttypes-documentcategorycode-langcode)
* [GET /doccattypes](#get-doccattypes)
* [GET /checkapptypedoccattypedoctype](#get-checkapptypedoccattypedoctype)


# POST /documenttype

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	     ]
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
  "successfully_created_documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	]
       }
}
```

# PUT /documenttype

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
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
  "successfully_updated_documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"}
	     ]
         }
}
```

# GET /documenttypes/{documentcategorycode}/{langcode}

This service will provides the service for the valid doucment type avialbale for specific Document Category code


### Resource URL
### `GET /documenttypes/{documentcategorycode}/{langcode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------

documentcategorycode |Yes| Code of document category | |
langcode | Yes | language code | |

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
                "description": "string",
                "isActive": true,
                "langCode": "string",
                "name": "string"
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


# GET /documentcategorytypes

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
  "documenttypes": [
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
		{"code": "code", "name": "name", "descr":"descr", "lang_code":"lang_code", "is_active":"is_active"},
	          ]
             }
  }
```


# GET /doccattypes

This service will give back the document category and it's corresponding category types based on Individal type code, Age group type code and Gender type code. 

### Resource URL
### `GET /doccattypes`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
individualtypecode |Yes| Code of Individual type | |
agegrouptypecode |Yes| Code of Age group type | |
gendertypecode |Yes| Code of Gender type | |

### Example Request
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
    "individualtypecode": "string",
    "agegrouptypecode": "string",
    "gendertypecode": "string"
  }
}
```
### Example Response
```JSON
{
	"documentcategories": [
		{
			"code": "string",
			"description": "string",
			"isActive": true,
			"langCode": "string",
			"name": "string",
			"documenttype": [
				{
					"code": "code",
					"name": "name",
					"descr": "descr",
					"lang_code": "lang_code",
					"is_active": "is_active"
				}
			]
		}
	]
}
```



# GET /checkapptypedoccattypedoctype

This service checks the mapping between the Applicant type code, Document category and the Document type mapping. Result message will be success, if the mapping exists. 

### Resource URL
### `GET /checkapptypedoccattypedoctype`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
applicanttypecode |Yes| Code of Individual type | |
documentcategorycode |Yes| Code of Age group type| |
documenttypecode |Yes| Code of Document type | |

### Example Request
```JSON
{
  "id": "mosip.master.doccattypesonindtypagegndr",
  "ver": "1.0",
  "timestamp": "2018-12-24T05:27:49.183Z",
  "request": {
    "applicanttypecode": "string",
    "documentcategorycode": "string",
    "documenttypecode": "string"
  }
}
```
### Example Response
```JSON
{
	"resultMessage":"Success"
}
```


# Valid documents API

* [GET /validdocuments](#get-validdocuments)

### Resource URL
### `GET /validdocuments/{languagecode}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
languagecode|Yes|Language code in ISO 639-2|-NA-|fra

### Example Request
```JSON
-NA-
```

### Example Success Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [],
  "response":   {
	  "documentcategories": [
		{
			"code": "string",
			"description": "string",
			"isActive": true,
			"langCode": "string",
			"name": "string", 
			"documenttypes": [
					{
						"code": "string",
						"description": "string",
						"isActive": true,
						"langCode": "string",
						"name": "string"
					}
			]
		}
	  ]
	}
}
```


### Example Failure Response
```JSON
{
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [
	{
		"errorCode": "KER-VLDDOC-001",
		"message": "Mandatory fields are missing"
	}  
  ],
  "response": null
}
```


### Response codes
200

Description: Success