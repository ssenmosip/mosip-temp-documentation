ID definition is the key to use MOSIP. ID definition describes the attributes a country or entity will capture from an Individual. Since, MOSIP is a generic Identity platform the attributes of an ID cannot be predefined by MOSIP. One country may capture 5 attributes and another 10 attributes. So, to accommodate this flexibility MOSIP provides a feature where a country defines an ID object definition schema. This will be the first step in using MOSIP. Once an ID object schema is defined, all applications built on top of MOSIP platform to capture data MUST conform to the ID object schema.

* As a rule of thumb, only attributes related to an individual (demographic and biometric), his/her parent/guardian attributes (demographic and biometric) should be captured in the ID object
* All other data captured in the field like operator/supervisor data should not be part of the ID object
* Schema can use predefined JSON data types to define attributes
* Schema can also create User Defined Types (UDTs) to specify the format of data to be captured. For example, biometrics data should always be in CBEFF ISO 19795 - 1 format. This helps in specifying the format of the data that is captured
* MOSIP will provide in-built validators for certain data types like CBEFF which can be used for data validation

Below is a sample ID object definition schema and a sample of a JSON object based on the schema.

```
{
	"$id": "http://mosip.io/id_object/1.0/id_object.json",
	"$schema": "http://json-schema.org/draft-07/schema#",
	"title": "MOSIP ID schema",
	"description": "Sample ID schema",
	"type": "object",
	"additionalProperties": false,
	"properties": {
		"identity": {
			"title": "identity",
			"description": "This schema holds all the attributes of an Identity",
			"type": "object",
			"additionalProperties": false,
			"properties": {
				"IDSchemaVersion": {
					"type": "number"
				},
				"UIN": {
					"type": "number"
				},
				"fullName": {
					"$ref": "#/definitions/simpleType"
				},
				"dateOfBirth": {
					"$ref": "#/definitions/dateOfBirthType"
				},
				"age": {
					"type": "number"
				},
				"gender": {
					"$ref": "#/definitions/simpleType"
				},
				"addressLine1": {
					"$ref": "#/definitions/simpleType"
				},
				"addressLine2": {
					"$ref": "#/definitions/simpleType"
				},
				"addressLine3": {
					"$ref": "#/definitions/simpleType"
				},
				"region": {
					"$ref": "#/definitions/simpleType"
				},
				"province": {
					"$ref": "#/definitions/simpleType"
				},
				"city": {
					"$ref": "#/definitions/simpleType"
				},
				"postalCode": {
					"$ref": "#/definitions/postalCodeType"
				},
				"phone": {
					"$ref": "#/definitions/phoneType"
				},
				"email": {
					"$ref": "#/definitions/emailType"
				},
				"CNIENumber": {
					"type": "number"
				},
				"localAdministrativeAuthority": {
					"$ref": "#/definitions/simpleType"
				},
				"parentOrGuardianName": {
					"$ref": "#/definitions/simpleType"
				},
				"parentOrGuardianRIDOrUIN": {
					"type": "number"
				},
				"proofOfAddress": {
					"$ref": "#/definitions/documentType"
				},                               
				"proofOfIdentity": {
					"$ref": "#/definitions/documentType"
				},
				"proofOfRelationship": {
					"$ref": "#/definitions/documentType"
				},
				"proofOfDateOfBirth": {
					"$ref": "#/definitions/documentType"
				},
				"individualBiometrics": {
					"$ref": "#/definitions/biometricsType"
				},
				"parentOrGuardianBiometrics": {
					"$ref": "#/definitions/biometricsType"
				}
			}
		}
	},
	"definitions": {
		"simpleType": {
			"type": "array",
			"additionalItems": false,
			"uniqueItems": true,
			"items": {
				"type": "object",
				"required": [
					"language",
					"value"
				],
				"additionalProperties": false,
				"properties": {
					"language": {
						"type": "string",
						"pattern": "^[(?i)a-z]{3}$"
					},
					"value": {
						"type": "string"
					}
				}
			}
		},
		"dateOfBirthType": {
			"type": "string",
			"pattern": "^\\d{4}/([0]\\d|1[0-2])/([0-2]\\d|3[01])$"
		},
		"phoneType": {		
			"type": "string",
			"pattern": "^([9]{1})([234789]{1})([0-9]{8})$"
		},
		"postalCodeType": {		
			"type": "string",
			"pattern": "^[(?i)A-Z0-9]{6}$"
		},
		"emailType": {
			"type": "string",
			"pattern": "^\\w+@[a-zA-Z_]+?\\.[a-zA-Z]{2,3}$"
		},
		"documentType": {
			"type": "object",
			"properties": {
				"format": {
					"type": "string"
				},
				"type": {
					"type": "string"
				},
				"fileReference": {
					"type": "string"
				}
			}
		},
		"biometricsType": {
			"type": "object",
			"properties": {
				"format": {
					"type": "string"
				},
				"version": {
					"type": "number"
				},
				"fileReference": {
					"type": "string"
				}
			}
		}
	}
}
```

Below is a sample JSON as per the schema defined above 

```
{
  "identity": {
    "IDSchemaVersion": 1.0,
    "UIN": 981576026435,
    "fullName": [
      {
        "language": "ara",
        "value": "ابراهيم بن علي"
      },
      {
        "language": "fre",
        "value": "Ibrahim Ibn Ali"
      }
    ],
    "dateOfBirth": "1955/04/15",
    "age": 45,
    "gender": [
      {
        "language": "ara",
        "value": "الذكر"
      },
      {
        "language": "fre",
        "value": "mâle"
      }
    ],
    "addressLine1": [
      {
        "language": "ara",
        "value": "عنوان العينة سطر 1"
      },
      {
        "language": "fre",
        "value": "exemple d'adresse ligne 1"
      }
    ],
    "addressLine2": [
      {
        "language": "ara",
        "value": "عنوان العينة سطر 2"
      },
      {
        "language": "fre",
        "value": "exemple d'adresse ligne 2"
      }
    ],
    "addressLine3": [
      {
        "language": "ara",
        "value": "عنوان العينة سطر 2"
      },
      {
        "language": "fre",
        "value": "exemple d'adresse ligne 2"
      }
    ],
    "region": [
      {
        "language": "ara",
        "value": "طنجة - تطوان - الحسيمة"
      },
      {
        "language": "fre",
        "value": "Tanger-Tétouan-Al Hoceima"
      }
    ],
    "province": [
      {
        "language": "ara",
        "value": "فاس-مكناس"
      },
      {
        "language": "fre",
        "value": "Fès-Meknès"
      }
    ],
    "city": [
      {
        "language": "ara",
        "value": "الدار البيضاء"
      },
      {
        "language": "fre",
        "value": "Casablanca"
      }
    ],
    "postalCode": "570004",
    "phone": "9876543210",
    "email": "abc@xyz.com",
    "CNIENumber": 6789545678909,
    "localAdministrativeAuthority": [
      {
        "language": "ara",
        "value": "سلمى"
      },
      {
        "language": "fre",
        "value": "salma"
      }
    ],
    "parentOrGuardianRIDOrUIN": 212124324784912,
    "parentOrGuardianName": [
      {
        "language": "ara",
        "value": "سلمى"
      },
      {
        "language": "fre",
        "value": "salma"
      }
    ],
    "proofOfAddress": {
      "format": "pdf",
      "type": "drivingLicense",
      "value": "fileReferenceID"
    },
    "proofOfIdentity": {
      "format": "txt",
      "type": "passport",
      "value": "fileReferenceID"
    },
    "proofOfRelationship": {
      "format": "pdf",
      "type": "passport",
      "value": "fileReferenceID"
    },
    "proofOfDateOfBirth": {
      "format": "pdf",
      "type": "passport",
      "value": "fileReferenceID"
    },
    "individualBiometrics": {
      "format": "cbeff",
      "version": 1.0,
      "value": "fileReferenceID"
    },
    "parentOrGuardianBiometrics": {
      "format": "cbeff",
      "version": 1.0,
      "value": "fileReferenceID"
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
	"version" : "1.0",	
	"request" : 
	{
		//JSON request as per the id object schema defined by the country				
	}
}
```
Also, please refer to ID Repository API on how an ID Object is managed in MOSIP @ https://github.com/mosip/mosip/wiki/ID-Repository-API