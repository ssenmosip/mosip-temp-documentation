Definition of an ID Object i.e., the attributes of an ID are country specific and MOSIP cannot define them. To achieve this, MOSIP will have a provision for a country to define their own ID Object schema and provide it as an input to MOSIP. 

The first step for a system owner to use MOSIP is to define the ID Object schema. ID Object schema should be a JSON schema. Below is a sample schema which defines a set of attributes for an ID. 

```
{
	"$id": "http://mosip.io/schemas/mosip-id-schema.json",
	"$schema": "http://json-schema.org/draft-07/schema#",
	"title": "MOSIP ID schema",
	"description": "Sample ID schema to refer to",
	"type": "object",
	"additionalProperties": false,
	"properties": {
		"identity": {
			"title": "identity",
			"description": "This holds all the attributes of an Identity",
			"type": "object",
			"additionalProperties": false,
			"properties": {
				"firstName": {
					"$ref": "#/definitions/values"
				},
				"middleName": {
					"$ref": "#/definitions/values"
				},
				"lastName": {
					"$ref": "#/definitions/values"
				},
				"dateOfBirth": {
					"$ref": "#/definitions/values"
				},
				"gender": {
					"$ref": "#/definitions/values"
				},
				"addressLine1": {
					"$ref": "#/definitions/values"
				},
				"addressLine2": {
					"$ref": "#/definitions/values"
				},
				"addressLine3": {
					"$ref": "#/definitions/values"
				},
				"region": {
					"$ref": "#/definitions/values"
				},
				"province": {
					"$ref": "#/definitions/values"
				},
				"city": {
					"$ref": "#/definitions/values"
				},
				"localAdministrativeAuthority": {
					"$ref": "#/definitions/values"
				},
				"mobileNumber": {
					"$ref": "#/definitions/values"
				},
				"emailId": {
					"$ref": "#/definitions/values"
				},
				"CNEOrPINNumber": {
					"$ref": "#/definitions/values"
				},
				"parentOrGuardianName": {
					"$ref": "#/definitions/values"
				},
				"parentOrGuardianRIDOrUIN": {
					"$ref": "#/definitions/values"
				},
				"leftEye": {
					"$ref": "#/definitions/values"
				},
				"rightEye": {
					"$ref": "#/definitions/values"
				},
				"biometricScan1": {
					"$ref": "#/definitions/values"
				},
				"biometricScan2": {
					"$ref": "#/definitions/values"
				},
				"biometricScan3": {
					"$ref": "#/definitions/values"
				}
			}
		}
	},
	"definitions": {
		"values": {
			"type": "array",
			"additionalItems": false,
			"uniqueItems": true,
			"items": {
				"type": "object",
				"required": [
					"language",
					"label",
					"value"
				],
				"additionalProperties": false,
				"properties": {
					"language": {
						"type": "string"
					},
					"label": {
						"type": "string"
					},
					"value": {
						"type": "string"
					}
				}
			}
		}
	}
}
```
All operations related to ID will have a place holder to receive the ID Object as per the schema, validate it as per the schema and store it AS IS. For example, when an Individual creates a Pre-Registration, the API for Pre-Registration will look as below

```
//CREATE Pre-Registration
request body
{
	"id" : "mosip.pre-registration.create",
	"ver" : "1.0",	
	"request" : 
	{
		//JSON request as per the id object schema defined by the country				
	}
}
```