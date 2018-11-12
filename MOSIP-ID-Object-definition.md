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
				"leftSlap": {
					"$ref": "#/definitions/values"
				},
				"rightSlap": {
					"$ref": "#/definitions/values"
				},
				"thumbs": {
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

Below is a sample JSON as per the schema defined above
```
{
	"identity": {
		"firstName": [
			{
				"language": "ar",
				"label": "الاسم الاول",
				"value": "ابراهيم"
			},
			{
				"language": "fr",
				"label": "Prénom",
				"value": "Ibrahim"
			}
		],
		"middleName": [
			{
				"language": "ar",
				"label": "الاسم الأوسط",
				"value": "بن"
			},
			{
				"language": "fr",
				"label": "deuxième nom",
				"value": "Ibn"
			}
		],
		"lastName": [
			{
				"language": "ar",
				"label": "الكنية",
				"value": "علي"
			},
			{
				"language": "fr",
				"label": "nom de famille",
				"value": "Ali"
			}
		],
		"dateOfBirth": [
			{
				"language": "ar",
				"label": "تاريخ الولادة",
				"value": "16/04/1955"
			},
			{
				"language": "fr",
				"label": "date de naissance",
				"value": "16/04/1955"
			}
		],
		"gender": [
			{
				"language": "ar",
				"label": "جنس",
				"value": "الذكر"
			},
			{
				"language": "fr",
				"label": "le sexe",
				"value": "mâle"
			}
		],
		"addressLine1": [
			{
				"language": "ar",
				"label": "العنوان السطر 1",
				"value": "عنوان العينة سطر 1"
			},
			{
				"language": "fr",
				"label": "Adresse 1",
				"value": "exemple d'adresse ligne 1"
			}
		],
		"addressLine2": [
			{
				"language": "ar",
				"label": "العنوان السطر 2",
				"value": "عنوان العينة سطر 2"
			},
			{
				"language": "fr",
				"label": "Adresse 2",
				"value": "exemple d'adresse ligne 2"
			}
		],
		"addressLine3": [
			{
				"language": "ar",
				"label": "العنوان السطر 3",
				"value": "عنوان العينة سطر 3"
			},
			{
				"language": "fr",
				"label": "Adresse 3",
				"value": "exemple d'adresse ligne 3"
			}
		],
		"region": [
			{
				"language": "ar",
				"label": "رمنطقة",
				"value": "طنجة - تطوان - الحسيمة"
			},
			{
				"language": "fr",
				"label": "Région",
				"value": "Tanger-Tétouan-Al Hoceima"
			}
		],
		"province": [
			{
				"language": "ar",
				"label": "المحافظة",
				"value": "فاس-مكناس"
			},
			{
				"language": "fr",
				"label": "province",
				"value": "Fès-Meknès"
			}
		],
		"city": [
			{
				"language": "ar",
				"label": "مدينة",
				"value": "فاس-الدار البيضاء"
			},
			{
				"language": "fr",
				"label": "ville",
				"value": "Casablanca"
			}
		],
		"localAdministrativeAuthority": [
			{
				"language": "ar",
				"label": "الهيئة الإدارية المحلية",
				"value": "طنجة - تطوان - الحسيمة"
			},
			{
				"language": "fr",
				"label": "Autorité administrative locale",
				"value": "Tanger-Tétouan-Al Hoceima"
			}
		],
		"mobileNumber": [
			{
				"language": "ar",
				"label": "رقم الهاتف المحمول",
				"value": "+212-5398-12345"
			},
			{
				"language": "fr",
				"label": "numéro de portable",
				"value": "+212-5398-12345"
			}
		],
		"emailId": [
			{
				"language": "ar",
				"label": "عنوان الايميل",
				"value": "sample@samplamail.com"
			},
			{
				"language": "fr",
				"label": "identifiant email",
				"value": "sample@samplamail.com"
			}
		],
		"CNEOrPINNumber": [
			{
				"language": "ar",
				"label": "رقم CNE / PIN",
				"value": "AB453625"
			},
			{
				"language": "fr",
				"label": "Numéro CNE / PIN",
				"value": "AB453625"
			}
		],
		"parentOrGuardianName": [
			{
				"language": "ar",
				"label": "اسم ولي الأمر / الوصي",
				"value": "سلمى"
			},
			{
				"language": "fr",
				"label": "Nom du parent / tuteur",
				"value": "salma"
			}
		],
		"parentOrGuardianRIDOrUIN": [
			{
				"language": "ar",
				"label": "الوالد / الوصي RID / UIN",
				"value": "123456789123"
			},
			{
				"language": "fr",
				"label": "parent / tuteur RID / UIN",
				"value": "123456789123"
			}
		],
		"leftEye": [
			{
				"language": "ar",
				"label": "العين اليسرى",
				"value": "hashed_fileName.png"
			},
			{
				"language": "fr",
				"label": "oeil gauche",
				"value": "hashed_fileName.png"
			}
		],
		"rightEye": [
			{
				"language": "ar",
				"label": "العين اليمنى",
				"value": "hashed_fileName.png"
			},
			{
				"language": "fr",
				"label": "l'œil droit",
				"value": "hashed_fileName.png"
			}
		],
		"leftSlap": [
			{
				"language": "ar",
				"label": "البيومترية المسح الضوئي 1",
				"value": "hashed_fileName.png"
			},
			{
				"language": "fr",
				"label": "analyse biométrique 1",
				"value": "hashed_fileName.png"
			}
		],
		"rightSlap": [
			{
				"language": "ar",
				"label": "البيومترية المسح الضوئي 2",
				"value": "hashed_fileName.png"
			},
			{
				"language": "fr",
				"label": "analyse biométrique 2",
				"value": "hashed_fileName.png"
			}
		],
		"thumbs": [
			{
				"language": "ar",
				"label": "البيومترية المسح الضوئي 3",
				"value": "hashed_fileName.png"
			},
			{
				"language": "fr",
				"label": "analyse biométrique 3",
				"value": "hashed_fileName.png"
			}
		]
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
Also, please refer to ID Repository API on how an ID Object is managed in MOSIP @ https://github.com/mosip/mosip/wiki/ID-Repository-API