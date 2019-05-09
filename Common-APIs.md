This section details about the service APIs in the common modules

* [Titles API](#titles-master-api)

* [Gender API](#gender-master-api)

* [Age Groups API](#age-group-types-api)

* [ID Types API](#id-types-master-api)

* [Holidays API](#holiday-master-api) 

* [Locations API](#locations-master-api)

* [Languages API](#languages-master-api)

* [Individual Types API](#individual-types-api)

* [Application Types API](#application-types-master-api)

* [Blacklisted Words API](#blacklisted-words-master-api)

# Titles Master API

* [POST /title](#post-title)
* [GET /title](#get-title)
* [GET /title/{languagecode}](#get-titlelanguagecode)
* [PUT /title](#put-title)
* [DELETE /title/{code}](#delete-titlecode)

# POST /title
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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
              "code": "cvf",
              "isActive": true,
              "langCode": "ghf",
              "titleDescription": "string",
              "titleName": "string"
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
  "errors": [ {
      "errorCode": "string",
      "message": "string"
    } ],
  "response": {
              "code": "cvf",
              "langCode": "ghf"
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

# GET /title
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
          "titleList": [ {
                        "code": "43",
                        "titleName": "string",
                        "titleDescription": "string",
                        "isActive": true,
                        "langCode": "ENG"
                       } ]
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


# GET /title/{languagecode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
              "titleList": [{
                            "code": "xcv",
                            "titleName": "string",
                            "titleDescription": "string",
                            "isActive": true,
                            "langCode": "qwe"
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

# PUT /title
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

# DELETE /title/{code}
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


# Gender Master API

* [POST /gendertypes](#post-gendertypes)
* [PUT/gendertypes](#putgendertypes)
* [DELETE/gendertypes/{code}](#deletegendertypescode)
* [GET /gendertypes](#get-gendertypes)
* [GET /gendertypes/{languagecode}](#get-gendertypeslanguagecode)
* [GET /gendertypes/{gendername}](#get-gendertypesgendername)

# POST /gendertypes

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
              "code": "GC002",
              "genderName": "Male",
              "isActive": true,
             "langCode": "ENG"
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
               "code": "GC002",
               "langCode": "ENG"
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

# PUT/gendertypes

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
               "code": "GC001",
               "genderName": "Male",
               "isActive": true,
               "langCode": "ENG"
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
                 "code": "GC001",
                 "langCode": "ENG"
              }
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

# DELETE/gendertypes/{code}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
               "errorCode": "string",
               "message": "string"
            }],
  "response": {
               "code": "GC001",
              }
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

# GET /gendertypes
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
              "errorCode": "string",
              "message": "string"
            }],
  "response": {  
               "genderType": [{
                               "code": "GC001",
                               "genderName": "Female",
                               "langCode": "eu",
                               "isActive": true
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


# GET /gendertypes/{languagecode}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
             "genderType": [{
                           "code": "GC002",
                           "genderName": "Male",
                           "langCode": "ENG",
                           "isActive": true
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



# GET /gendertypes/{gendername}
Master data is required across the platform. 

This service will provides the gender based on the gender name. 



### Resource URL
### `GET /gendertypes/{gendername}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
gendername|Yes|Name of the gender| | 


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
	       "code": "GC001",
	       "genderName": "Female",
	       "langCode": "eu",
	       "isActive": true
              }
}
```
200

Description: Success

# Age group Types API

* [GET /agegrouptype/{age}](#get-agegrouptypeage)

# GET /agegrouptype/{age}

This service will provides the age group based on the passed age. 


### Resource URL
### `GET /agegrouptype/{age}`

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
	"agegrouptypecode": "string",
	"name": "string",
	"description": "string",
	"minimumage": "number",
	"maximumage": "number",
	"langCode": "string",
	"isactive": boolean
  }
}
```

### Response codes
200

Description: Success


# ID Types Master API

* [POST /idtypes](#post-idtypes)
* [GET /idtypes](#get-idtypes)
* [GET /idtypes/{languagecode}](#get-idtypeslanguagecode)

# POST /idtypes
Master data is required across the platform. 

This service will create the list of Id types which are used in the MOSIP platform. 

### Resource URL
### `POST /idtypes`

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request": {
               "code": "string",
               "descr": "string",
               "isActive": true,
               "langCode": "string",
               "name": "string"
              },
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
    } ],
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

# GET /idtypes
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
               "errorCode": "string",
               "message": "string"
            }],
  "response": {
	"idtypes": [{
			"code": "string",
			"descr": "string",
			"langCode": "string"
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


# GET /idtypes/{languagecode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
             "errorCode": "string",
             "message": "string"
           }],
  "response": {
	"idtypes": [{
			"code": "string",
			"descr": "string",
			"langCode": "string"
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


# Holiday Master API

* [POST /holidays](#post-holidays)
* [GET /holidays](#get-holidays)
* [GET /holidays/{languagecode}](#get-holidayslanguagecode)

## POST /holidays
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
	"request" : { 
		  "holiday":{ "holidayDate": "string", "holidayName": "string", "languagecode": "string" }
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
  "errors": [
    {
      "errorCode": "string",
      "message": "string"
    }
  ],
  "response" : { "holidayID": "string" }
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


## GET /holidays
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [ {
             "errorCode": "string",
             "message": "string"
             }
           ],
 "response" : {
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


## GET /holidays/{languagecode}

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{ 
               "errorCode": "string",
               "message": "string"
             }],
  "response" : {
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

 
# Locations Master API

* [POST /locations](#post-locations)
* [PUT /locations](#put-locations)
* [DELETE /locations/{locationcode}](#delete-locationslocationcode)
* [GET /locations/{langcode}](#get-locationslangcode)
* [GET /locations/{locationcode}/{languagecode}](#get-locationslocationcodelanguagecode)
* [GET /locations/immediatechildren/{locationcode}/{languagecode}](#get-locationsimmediatechildrenlocationcodelanguagecode)
* [GET /locations/locationhierarchy/{hierarchyname}](#get-locationslocationhierarchyhierarchyname)

# `POST /locations`

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
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
             "isActive": true,
             "parentLocCode": "string"
             }
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


# PUT /locations

### Resource URL
### `PUT /locations`

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
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
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
               "langCode:"string"

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



# DELETE /locations/{locationcode}

### Resource URL
### `DELETE /locations/{locationcode}`

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
                "code": "string"
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



# GET /locations/{langcode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
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



# GET /locations/{locationcode}/{languagecode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response":{
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


# GET /locations/immediatechildren/{locationcode}/{languagecode}
Master data is required across the platform. 

This service will provides the service for the List of Locations. 



### Resource URL
### `GET /locations/immediatechildren/{locationcode}/{languagecode}`

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
          "locations": [ 
                       {
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean"	
		      },
		      {
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean"
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



# GET /locations/locationhierarchy/{hierarchyname}
Master data is required across the platform. 

This service will provides the service for the List of Locations based on the location hierarchy name. 



### Resource URL
### `GET /locations/locationhierarchy/{hierarchyname}`

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
           "locations": [
	         	{
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean"	
		        },
		       {
			"code":"string",
			"name":"string",
			"hierarchyLevel":"number",
			"hierarchyLevelName":"string",
			"parentLocCode":"",
			"langCode":"string",
			"isActive":"boolean"
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




# GET /locations/locationhierarchy/{locationname}

This service will provides the service for the List of Locations based on the location name. 


### Resource URL
### `GET /locations/locationhierarchy/{locationname}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
locationname|yes|This is the location name. | -NA- | 

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
}
```
200

Description: Success


# Languages Master API

* [POST /languages](#post-languages)
* [GET /languages](#get-languages)
* [PUT /languages](#put-languages)
* [DELETE /languages/{code}](#delete-languagescode)

# POST /languages

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
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

# GET /languages

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
	"languages": [{
		      "code": "string",
		      "name": "string",
		      "family": "string",
		      "native_name": "string",
		      "is_active": "boolean"
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

# PUT /languages

This service will update a Language which is used in the MOSIP platform. 

### Resource URL
### `PUT /languages`

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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
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
### Response codes
200

Description: Ok

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden


# DELETE /languages/{code}

This service will delete a Language which is used in the MOSIP platform. 

### Resource URL
### `DELETE /languages/{code}`

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
### Response codes
200

Description: Ok

400

Description: Bad request

401

Description: Unauthorized

403

Description: Forbidden


# Individual Types API

* [GET /individualtypes](#get-individualtypes)

# GET /individualtypes

This service will provides the complete list of all individual types in the MOSIP platform


### Resource URL
### `GET /individualtypes`

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
  "individualtypes": [
    {
      "individualtypecode": "string",
      "name": "string",
      "description": "string",
      "langCode": "string",
      "isactive": boolean
    }
  ]
 }
}
```

### Response codes
200

Description: Success


# Application Types Master API

* [POST /applicationtypes](#post-applicationtypes)
* [GET /applicationtypes](#get-applicationtypes)
* [GET /applicationtypes/{id}/{languagecode}](#get-applicationtypesidlanguagecode)

# POST /applicationtypes
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request":  {
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
  "successfully_created_applicationtypes": [
	                	               {"applicationtypeid":"string"},
		                               {"languagecode":"string"}
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

# GET /applicationtypes
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
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


# GET /applicationtypes/{id}/{languagecode}
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
  "response": {
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


# Blacklisted words Master API

* [POST /blacklistedwords](#post-blacklistedwords)
* [GET /blacklistedwords](#get-blacklistedwords)
* [GET /blacklistedwords/{id}/{languagecode}](#get-blacklistedwordsidlanguagecode-1)
* [PUT /blacklistedwords](#put-blacklistedwords)
* [DELETE /blacklistedwords/{word}](#delete-blacklistedwordsword)

## POST /blacklistedwords 
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "requesttime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "request" : {
		"blacklistedwords": ["asdf","lkjh","qwer"],
		"languagecode": "string"
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
"response" : {
  "successfully_created_words": ["asdf","lkjh","qwer"]
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

## GET /blacklistedwords
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
  "id": "string",
  "version": "string",
  "metadata": {},
  "responsetime": "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'",
  "errors": [{
      "errorCode": "string",
      "message": "string"
    }],
 "response" : {
		"blacklistedwords":[
			{
				"id":"string",
				"value":"asdf",
				"languagecode":"string"
			},
	                {
				"id":"string",
				"value":"asdf",
				"languagecode" :"string"
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


## GET /blacklistedwords/{id}/{languagecode}

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
"response":{
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

# PUT /blacklistedwords

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
"request":{
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
"resonpse" : {
              "langCode": "string",
              "word": "string"
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

# DELETE /blacklistedwords/{word}

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

