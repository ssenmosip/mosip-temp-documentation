This section details about the service APIs in the Pre-Registration modules

[2.7.1 Login API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#271-login-api)

[2.7.2 Login OTP Validation API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#272-login-otp-validation-api)

[2.7.3 User ID Updation API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#273-user-id-updation-api)

[2.7.4 Create Pre-Registration API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#274-create-pre-registration-api)

[2.7.5 Reterive all Pre-Registration API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#275-reterive-all-pre-registration-api)

[2.7.6 Reterive all Pre-Registration status API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#276-reterive-all-pre-registration-status-api)

[2.7.7 Discard Pre-Registration API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#277-discard-pre-registration-api)

[2.7.8 Document Upload API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#278-document-upload-api)

[2.7.9 Get Document API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#279-get-document-api)

[2.7.10 Get All Document API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2710-get-all-document-api)

[2.7.11 Delete Document API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2711-delete-document-api)

[2.7.12 Delete All Document  API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2712-delete-all-document-api)

[2.7.13 Copy Document API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2713-delete-all-document-api)

[2.7.14 Update Pre-Registartion API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2714-update-pre-registration-api)

[2.7.15 Data-Sync Reterive all Pre-Registartion Ids API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2715-Data-Sync-Reterive-all-Pre-Registartion-Ids-api)

[2.7.16 Data-Sync Reterive Pre-Registartion data API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2716-Data-Sync-Reterive-Pre-Registartion-data-api)

[2.7.17 Reverse Data-Sync Store Pre-Registartion Ids API](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs#2717-Reverse-Data-Sync-Store-Pre-Registartion-Ids-api)


## 2.7.1. Login API
This service details Login Request to be used by Pre-Registration portal to authenticate an user by providing his/her mobile number or email address. 
After validating the mobile number/email address an OTP get generated and same get notified to the user correspondingly. 

### Resource URL -  `GET pre-registration/login`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id||mosip.pre-registration.auth
ver|Y|API version||1.0
reqTime|Y|Time when Request was captured||2018-10-04T05:57:20.929+0000
request|Y|Request to be authenticated||
request.user-id | Y | Mobile Number/ Email Address| | 9911836586/ user@mail.com


### Sample Request
```JSON
{
		"id": "mosip.pre-registration.auth",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"user-id":"9911836586"
		}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"message": "USER_OTP_GENERATED"
		}
}
```
#### Fail Response:
```JSON
{
	       "status" : false,
	       "err": [
                   {
		      			"code":"PRG-AUTH-LOGIN-001",
		      			"message": "USER_OTP_GENERATION_FAILED"
                   }
                ],
	        "resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.2 Login OTP Validation API
This service enables Pre-Registration portal to request for an OTP for validation. Once the OTP received via message or email. This OTP should then be used to authenticate an user.

### Resource URL - `POST pre-registration/login/{user-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id||mosip.pre-registration.auth
ver|Y|API version||1.0
reqTime|Y|Time when Request was captured||2018-10-04T05:57:20.929+0000
request|Y|Request to be authenticated||
request.user-otp | Y | OTP| | 212132


### Sample Request
##### Request Body
```JSON
{
		"id": "mosip.pre-registration.auth",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"user-otp":"212132"
		}
}
```
##### Request Param
```String
9911836586
```
### Sample Response
#### Success Response:
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"message": "OTP_VALIDATION_SUCESSFUL"
		}
}
```

#### Failed Response :
```JSON
{
		"status" : false,
		"err": [
		{
			"code":"PRG-AUTH-LOGIN-002",
			"message": "USER_ID_INVALID"
		}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.3 User ID Updation API
This service enables Pre-Registration portal to request for an new user id for updation. Once new user id revceived an OTP get generated and send via message or email accordingly. This OTP should then be used to authenticate by user, once the OTP validation get successful then an old user id get updated to new user id.

### Resource URL - `PUT pre-registration/user/{user-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id|Y|API Id||mosip.pre-registration.auth
ver|Y|API version||1.0
reqTime|Y|Time when Request was captured||2018-10-04T05:57:20.929+0000
request|Y|Request to be authenticated||
request.new-user-id | Y | Mobile Number/ Email Address| | 9911836586/ user@mail.com


### Sample Request
##### Request Body
```JSON
{
		"id": "mosip.pre-registration.auth",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"new-user-id":"user@mail.com"
		}
}
```
##### Request Param
```String
9911836586
```
### Sample Response
#### Success Response:
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"message": "USER_UPDATION_SUCCESSFUL"
		}
}
```

#### Failed Response :
```JSON
{
		"status" : false,
		"err": [
		{
			"code":"PRG-AUTH-UPDATE-001",
			"message": "USER_UPDATION_FAILED"
		}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.4 Create Pre-Registration API
This service details used by Pre-Registration portal to create the demographic form by providing his/her basic demographic details.

### Resource URL -  `POST /pre-registration/applications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Request
```JSON
{
		"id": "mosip.pre-registration.demographic.create",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"preRegistrationId": "",
			"createdBy": "9900806086",
			"createdDatetime": "2018-10-17T07:22:57.086+0000",
			"updatedBy": "",
			"updatedDatetime": "",
			"statusCode": "Pending_Appointment",
			"langCode": "AR",
			"demographicDetails":
			{
				"identity":
				{
					"FullName": [
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
				"dateOfBirth": [
					{
						"language": "ar",
						"label": "تاريخ الميلاد",
						"value": "18/03/1995"
					},
					{
						"language": "fr",
						"label": "date de naissance",
						"value": "18/03/1995"
					}
				],
				"gender":[
					{
						"language": "ar",
						"label": "جنس",
						"value": "الذكر"
					},
					{
						"language": "fr",
						"label": "Le sexe",
						"value": "Male"
					}
				],
				"addressLine1": [
					{
						"language": "ar",
						"label": "العنوان السطر 1",
						"value": "عالمي"
					},
					{
						"language": "fr",
						"label": "Adresse 1",
						"value": "Global"
					}
				],
				"addressLine2": [
					{
						"language": "ar",
						"label": "سطر العنوان 2",
						"value": "قرية"
					},
					{
						"language": "fr",
						"label": "Adresse 2",
						"value": "Village"
					}
				],
				"addressLine3": [
					{
						"language": "ar",
						"label": "العنوان الخط 3",
						"value": "ابراهيم"
					},
					{
						"language": "fr",
						"label": "Adresse 3",
						"value": "Mindtree"
					}
				],
				"region": [
					{
						"language": "ar",
						"label": "منطقة",
						"value": "أودوبي"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Udupi"
					}
				],
				"province": [
					{
						"language": "ar",
						"label": "المحافظة",
						"value": "كوب"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Koppa"
					}
				],
				"city": [
					{
						"language": "ar",
						"label": "مدينة",
						"value": "مانجالور"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Mangalore"
					}
				],
				"postalcode": [
					{
						"language": "ar",
						"label": "الكود البريدى",
						"value": "675123"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "675123"
					}
				],
				"localAdministrativeAuthority": [
					{
						"language": "ar",
						"label": "السلطة الإدارية المحلية",
						"value": "إدارة"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "La gestion"
					}
				],
				"emailId": [
					{
						"language": "ar",
						"label": "البريد الإلكتروني",
						"value": "ram@gmail.com"
					},
					{
						"language": "fr",
						"label": "Email",
						"value": "ram@gmail.com"
					}
				],
				"mobileNumber":[
					{
						"language": "ar",
						"label": "رقم الهاتف المحمول",
						"value": "984839347"
					},
					{
						"language": "fr",
						"label": "Numéro de portable",
						"value": "984839347"
					}
				],
				"CNEOrPINNumber": [
					{
						"language": "ar",
						"label": "الرقم السري",
						"value": "45667677"
					},
					{
						"language": "fr",
						"label": "Code PIN",
						"value": "45667677"
					}
				],
				"age": [
					{
						"language": "ar",
						"label": "عمر",
						"value": "35"
					},
					{
						"language": "fr",
						"label": "Âge",
						"value": "35"
					}
				]
			}
		}
	}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"Pre-Registration-Id": "59276903416082",
			"createdBy": "9900806086",
			"createDateTime": "2018-10-26T07:04:10.844+0000"
			"statusCode": "Pending_Appointment",
			"langCode": "AR",
			"demographicDetails":
			{
				"identity":
				{
					"FullName": [
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
				"dateOfBirth": [
					{
						"language": "ar",
						"label": "تاريخ الميلاد",
						"value": "18/03/1995"
					},
					{
						"language": "fr",
						"label": "date de naissance",
						"value": "18/03/1995"
					}
				],
				"gender":[
					{
						"language": "ar",
						"label": "جنس",
						"value": "الذكر"
					},
					{
						"language": "fr",
						"label": "Le sexe",
						"value": "Male"
					}
				],
				"addressLine1": [
					{
						"language": "ar",
						"label": "العنوان السطر 1",
						"value": "عالمي"
					},
					{
						"language": "fr",
						"label": "Adresse 1",
						"value": "Global"
					}
				],
				"addressLine2": [
					{
						"language": "ar",
						"label": "سطر العنوان 2",
						"value": "قرية"
					},
					{
						"language": "fr",
						"label": "Adresse 2",
						"value": "Village"
					}
				],
				"addressLine3": [
					{
						"language": "ar",
						"label": "العنوان الخط 3",
						"value": "ابراهيم"
					},
					{
						"language": "fr",
						"label": "Adresse 3",
						"value": "Mindtree"
					}
				],
				"region": [
					{
						"language": "ar",
						"label": "منطقة",
						"value": "أودوبي"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Udupi"
					}
				],
				"province": [
					{
						"language": "ar",
						"label": "المحافظة",
						"value": "كوب"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Koppa"
					}
				],
				"city": [
					{
						"language": "ar",
						"label": "مدينة",
						"value": "مانجالور"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Mangalore"
					}
				],
				"postalcode": [
					{
						"language": "ar",
						"label": "الكود البريدى",
						"value": "675123"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "675123"
					}
				],
				"localAdministrativeAuthority": [
					{
						"language": "ar",
						"label": "السلطة الإدارية المحلية",
						"value": "إدارة"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "La gestion"
					}
				],
				"emailId": [
					{
						"language": "ar",
						"label": "البريد الإلكتروني",
						"value": "ram@gmail.com"
					},
					{
						"language": "fr",
						"label": "Email",
						"value": "ram@gmail.com"
					}
				],
				"mobileNumber":[
					{
						"language": "ar",
						"label": "رقم الهاتف المحمول",
						"value": "984839347"
					},
					{
						"language": "fr",
						"label": "Numéro de portable",
						"value": "984839347"
					}
				],
				"CNEOrPINNumber": [
					{
						"language": "ar",
						"label": "الرقم السري",
						"value": "45667677"
					},
					{
						"language": "fr",
						"label": "Code PIN",
						"value": "45667677"
					}
				],
				"age": [
					{
						"language": "ar",
						"label": "عمر",
						"value": "35"
					},
					{
						"language": "fr",
						"label": "Âge",
						"value": "35"
					}
				]
			}
		}
	}
  }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
           {
				"code":"PRG-PAM-APP-001",
				"message": "PRE_REGISTRATION_CREATE_FAILED"
           }
        ],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.5 Reterive all Pre-Registration API
This service enables Pre-Registration portal to request for all pre-registration applications created by logged-in user. 

### Resource URL - `GET /pre-registration/applications/{user-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
user-id | Y | Mobile Number/ Email Address| | 9911836586/ user@mail.com

### Sample Response
#### Success Response:
```JSON
{
	"status" : false,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000"
	"response":
	{
		"preRegistartions":[
		{
			"appointment_dtimesz": "2018-10-26 07:04:10.996",
			"pre-registration-id": "936857697491",
			"status_code": "Pending-Appointment",
			"fullname": "Ibrahim",
		},
		{
			"appointment_dtimesz": "2018-10-24 07:04:10.996",
			"pre-registration-id": "123122297491",
			"status_code": "Pending-Appointment",
			"fullname": "George",
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

## 2.7.6 Reterive Pre-Registration status API
This service enables Pre-Registration portal to request to reterive pre-registration status based on pre-registartion id.

### Resource URL - 
`GET /pre-registration/applications/status/{pre-reg-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | No

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
pre-reg-id | Y | ID for group of application | | 936857697491

### Sample Response
#### Success Response:
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":{
			"PreRegistartionId:"59276903416082",
			"StatusCode": "Pending-Appointment"
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

## 2.8.4 Discard Pre-Registration API
This service enables Pre-Registration portal to request to discard pre-registration based on pre-registration id. 

### Resource URL - 
`DELETE /pre-registration/applications/{pre-reg-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
--------|----------|-------------|---------------|--------
pre-reg-id| Y | pre-registration id of the application | | 59276903416082

### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-26T13:40:19.590+0000",
	"response":{
		"preRegistrationId": "59276903416082",
		"deletedBy": "921714816",
		"deletedDateTime": "2018-10-26T07:04:10.996+0000"
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

## 2.7.8 Document Upload API
This service enables Pre-Registration portal to request for uploading the document for a perticular pre-registration.

### Resource URL - 
`POST /pre-registration/documents`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


### Sample Request
##### Request Body
```JSON 
{
		"id": "mosip.pre-registration.document.upload",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"prereg_id" : "59276903416082",
			"doc_cat_code" : "POA",
			"doc_typ_code" : "address",
			"doc_file_format" : "pdf",
			"status_code" : "Pending-Appoinment",
			"upload_by" : "9217148168",
			"upload_DateTime" : "2018-10-17T07:22:57.086+0000"
		 }
}
```
######Multipart File:
```String
Choose file (.pdf)
```
### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"message":
	{
			"resMsg": "DOCUMENT_UPLOAD_SUCCESSFUL"
	}
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_009",
			"message": "DOCUMENT_INVALID_FORMAT"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_007",
			"message": "DOCUMENT_EXCEDING_PERMITTED_SIZE"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.9 Get Document API
This service enables Pre-Registration portal to request for reterive the perticular document by pre-registration id and document id.

### Resource URL - 
`GET /pre-registration/documents/{pre-reg-id}/{doc-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
doc-id | Y | Document id| | 16082

### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"response":[
		{
			"prereg_id" : "59276903416082",
			"doc-id":"16082",
			"MultipartFile":"{ByteCode}",
			"doc_cat_code" : "POA",
			"doc_typ_code" : "address",
			"doc_file_format" : "pdf"
		}
	]
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_014",
			"message": "Document not present"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.10 Get All Document API
This service enables Pre-Registration portal request to reterive all document associated with perticular pre-registration.

### Resource URL - 
`GET /pre-registration/documents/{pre-reg-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
pre-reg-id | Y | Pre-Registartion id| | 59276903416082

### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"response":[
		{
			"prereg_id" : "59276903416082",
			"doc-id":"21321",
			"MultipartFile":"{ByteCode}",
			"doc_cat_code" : "POA",
			"doc_typ_code" : "address",
			"doc_file_format" : "pdf"
		},
		{
			"prereg_id" : "59276903416082",
			"doc-id":"21322",
			"MultipartFile":"{ByteCode}",
			"doc_cat_code" : "POI",
			"doc_typ_code" : "id",
			"doc_file_format" : "pdf"
		}
	]
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_014",
			"message": "Document not present"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.11 Delete Document API
This service enables Pre-Registration portal, request to delete the document for a perticular document id.

### Resource URL - 
`DELETE /pre-registration/documents/{doc-id}`


### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
doc-id | Y | Document id| | 16082


### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"message":
	{
			"resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
	}
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_004",
			"message": "Document failed to delete"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_014",
			"message": "Documentt not present"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```
## 2.7.12 Delete All Document  API
This service enables Pre-Registration portal, request to delete all the document for a particular pre-registration id.

### Resource URL - 
`DELETE /pre-registration/documents/{pre-reg-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
pre-reg-id | Y | Pre-Registartion id| | 59276903416082

### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"message":
	{
			"resMsg": "DOCUMENT_DELETE_SUCCESSFUL"
	}
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_004",
			"message": "Document failed to delete"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_014",
			"message": "Documentt not present"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.13 Copy Document  API
This service enables Pre-Registration portal to request for copy the document from one pre-registration id to another.

### Resource URL - 
`PUT /pre-registration/documents/{cat_type}/{pre-reg-id}/{pre-reg-id}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
cat_type | Y | Document category code | | POA
pre-reg-id | Y | Source Pre-Registartion id| | 59276903416082
pre-reg-id | Y | Destination Pre-Registartion id| | 59276903416090

### Sample Response
#### Success Response:
```JSON
{
	"status" : true,
	"err": [],
	"resTime": "2018-10-17T13:40:19.590+0000",
	"message":
	{
			"resMsg": "DOCUMENT_COPY_SUCCESSFUL"
	}
 }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
		{
			"code":"PRG_PAM_DOC_016",
			"message": "Document failed to copy"
		}
	],
	"resTime": "2018-10-17T13:40:19.590+0000"
}
```
## 2.7.14 Update Pre-Registration  API
This service enables Pre-Registration portal, request to update the perticular pre-registration.

### Resource URL - `PUT /pre-registration/applications`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Request
```JSON
{
		"id": "mosip.pre-registration.demographic.update",
		"ver" : "1.0",
		"reqTime" : "2018-10-20T07:22:57.086+0000",
		"request" :
		{
			"preRegistrationId": "59276903416082",
			"createdBy": "9900806086",
			"createdDatetime": "2018-10-17T07:22:57.086+0000",
			"updatedBy": "9900806086",
			"updatedDatetime": "2018-10-20T07:22:57.086+0000",
			"statusCode": "Pending_Appointment",
			"langCode": "AR",
			"demographicDetails":
			{
				"identity":
				{
					"FullName": [
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
				"dateOfBirth": [
					{
						"language": "ar",
						"label": "تاريخ الميلاد",
						"value": "18/03/1995"
					},
					{
						"language": "fr",
						"label": "date de naissance",
						"value": "18/03/1995"
					}
				],
				"gender":[
					{
						"language": "ar",
						"label": "جنس",
						"value": "الذكر"
					},
					{
						"language": "fr",
						"label": "Le sexe",
						"value": "Male"
					}
				],
				"addressLine1": [
					{
						"language": "ar",
						"label": "العنوان السطر 1",
						"value": "عالمي"
					},
					{
						"language": "fr",
						"label": "Adresse 1",
						"value": "Global"
					}
				],
				"addressLine2": [
					{
						"language": "ar",
						"label": "سطر العنوان 2",
						"value": "قرية"
					},
					{
						"language": "fr",
						"label": "Adresse 2",
						"value": "Village"
					}
				],
				"addressLine3": [
					{
						"language": "ar",
						"label": "العنوان الخط 3",
						"value": "ابراهيم"
					},
					{
						"language": "fr",
						"label": "Adresse 3",
						"value": "Mindtree"
					}
				],
				"region": [
					{
						"language": "ar",
						"label": "منطقة",
						"value": "أودوبي"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Udupi"
					}
				],
				"province": [
					{
						"language": "ar",
						"label": "المحافظة",
						"value": "كوب"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Koppa"
					}
				],
				"city": [
					{
						"language": "ar",
						"label": "مدينة",
						"value": "مانجالور"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Mangalore"
					}
				],
				"postalcode": [
					{
						"language": "ar",
						"label": "الكود البريدى",
						"value": "675123"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "675123"
					}
				],
				"localAdministrativeAuthority": [
					{
						"language": "ar",
						"label": "السلطة الإدارية المحلية",
						"value": "إدارة"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "La gestion"
					}
				],
				"emailId": [
					{
						"language": "ar",
						"label": "البريد الإلكتروني",
						"value": "ram@gmail.com"
					},
					{
						"language": "fr",
						"label": "Email",
						"value": "ram@gmail.com"
					}
				],
				"mobileNumber":[
					{
						"language": "ar",
						"label": "رقم الهاتف المحمول",
						"value": "984839347"
					},
					{
						"language": "fr",
						"label": "Numéro de portable",
						"value": "984839347"
					}
				],
				"CNEOrPINNumber": [
					{
						"language": "ar",
						"label": "الرقم السري",
						"value": "45667677"
					},
					{
						"language": "fr",
						"label": "Code PIN",
						"value": "45667677"
					}
				],
				"age": [
					{
						"language": "ar",
						"label": "عمر",
						"value": "35"
					},
					{
						"language": "fr",
						"label": "Âge",
						"value": "35"
					}
				]
			}
		}
	}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-20T13:40:19.590+0000",
		"response":
		{
			"Pre-Registration-Id": "59276903416082",
			"updateBy": "9900806086",
			"updateDateTime": "2018-10-20T07:04:10.844+0000",
			"statusCode": "Pending_Appointment",
			"langCode": "AR",
			"demographicDetails":
			{
				"identity":
				{
					"FullName": [
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
				"dateOfBirth": [
					{
						"language": "ar",
						"label": "تاريخ الميلاد",
						"value": "18/03/1995"
					},
					{
						"language": "fr",
						"label": "date de naissance",
						"value": "18/03/1995"
					}
				],
				"gender":[
					{
						"language": "ar",
						"label": "جنس",
						"value": "الذكر"
					},
					{
						"language": "fr",
						"label": "Le sexe",
						"value": "Male"
					}
				],
				"addressLine1": [
					{
						"language": "ar",
						"label": "العنوان السطر 1",
						"value": "عالمي"
					},
					{
						"language": "fr",
						"label": "Adresse 1",
						"value": "Global"
					}
				],
				"addressLine2": [
					{
						"language": "ar",
						"label": "سطر العنوان 2",
						"value": "قرية"
					},
					{
						"language": "fr",
						"label": "Adresse 2",
						"value": "Village"
					}
				],
				"addressLine3": [
					{
						"language": "ar",
						"label": "العنوان الخط 3",
						"value": "ابراهيم"
					},
					{
						"language": "fr",
						"label": "Adresse 3",
						"value": "Mindtree"
					}
				],
				"region": [
					{
						"language": "ar",
						"label": "منطقة",
						"value": "أودوبي"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Udupi"
					}
				],
				"province": [
					{
						"language": "ar",
						"label": "المحافظة",
						"value": "كوب"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Koppa"
					}
				],
				"city": [
					{
						"language": "ar",
						"label": "مدينة",
						"value": "مانجالور"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "Mangalore"
					}
				],
				"postalcode": [
					{
						"language": "ar",
						"label": "الكود البريدى",
						"value": "675123"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "675123"
					}
				],
				"localAdministrativeAuthority": [
					{
						"language": "ar",
						"label": "السلطة الإدارية المحلية",
						"value": "إدارة"
					},
					{
						"language": "fr",
						"label": "Prénom",
						"value": "La gestion"
					}
				],
				"emailId": [
					{
						"language": "ar",
						"label": "البريد الإلكتروني",
						"value": "ram@gmail.com"
					},
					{
						"language": "fr",
						"label": "Email",
						"value": "ram@gmail.com"
					}
				],
				"mobileNumber":[
					{
						"language": "ar",
						"label": "رقم الهاتف المحمول",
						"value": "984839347"
					},
					{
						"language": "fr",
						"label": "Numéro de portable",
						"value": "984839347"
					}
				],
				"CNEOrPINNumber": [
					{
						"language": "ar",
						"label": "الرقم السري",
						"value": "45667677"
					},
					{
						"language": "fr",
						"label": "Code PIN",
						"value": "45667677"
					}
				],
				"age": [
					{
						"language": "ar",
						"label": "عمر",
						"value": "35"
					},
					{
						"language": "fr",
						"label": "Âge",
						"value": "35"
					}
				]
			}
		}
	}
  }
```
#### Failure Response:
```JSON
{
	"status" : false,
	"err": [
           {
				"code":"PRG_PAM_APP_006",
				"message": "Failed to update the demographic data"
           }
        ],
	"resTime": "2018-10-20T13:40:19.590+0000"
}
```

## 2.7.15 Data-Sync Reterive all Pre-Registartion Ids API
This service enables by Pre-Registration to a registration client , request to reterive all pre-registration ids based on registartion client id, appointment date and an user type.

### Resource URL - `GET /pre-registration/dataSync/ids`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Request
```JSON
{
		"id": "mosip.pre-registration.datasync",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"registration-center-ids":"59276903416082",
			"from-date":"15-11-2018",
			"to-date":"15-11-2018",
			"user-type":"Officer"
		}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"Transaction-id":"337324416082",
			"pre-registration-ids":[
				"59276903416082",
				"79276903416082",
				"89276903416082",
				"99276903416082",
				"59276616044482"
			]
		}
}
```
#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-001",
				"message": "Records Not Found For Requested Date Range"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-002",
				"message": "Records Not Found For Requested Registartion Center"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-003",
				"message": "Invalid User Type"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.15 Data-Sync Reterive Pre-Registartion data API
This service enables by Pre-Registration to a registration client , request to reterive particular pre-registration data based on pre registartion id.

### Resource URL - `GET /pre-registration/dataSync/data`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Request
```JSON
{
		"id": "mosip.pre-registration.datasync",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"pre-registration-id":"59276903416082",
			"registration-center-ids":"59276903416082",
			"user-type":"Officer"
		}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"Transaction-id":"337324416082",
			"pre-registration-id":"59276903416082"
		}
}
```
```ZipFile
59276903416082.zip
```
#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-004",
				"message": "Records Not Found For Requested PreRegId"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-005",
				"message": "Failed to create a zip file"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-DATA-SYNC-003",
				"message": "Invalid User Type"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```

## 2.7.16 Reverse Data-Sync Store Pre-Registartion ids API
This service enables by Pre-Registration to a registration processor , request to reterive all processed pre-registration ids and store in pre-registration database and update the status code in main table.

### Resource URL - `PUT /pre-registration/reverseDataSync/`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Sample Request
```JSON
{
		"id": "mosip.pre-registration.reverse.datasync",
		"ver" : "1.0",
		"reqTime" : "2018-10-17T07:22:57.086+0000",
		"request" :
		{
			"CountOfPreRegIds":"5",
			"pre-registration-ids":[
				"59276903416082",
				"79276903416082",
				"89276903416082",
				"99276903416082",
				"59276616044482"
			]
		}
}
```
### Sample Response
#### Success Response :
```JSON
{
		"status" : true,
		"err": [],
		"resTime": "2018-10-17T13:40:19.590+0000",
		"response":
		{
			"Transaction-Id":"2332432432",
			"message": "Pre-Registration IDs stored sucessfully"
		}
}
```

#### Failure Response:
```JSON
{
		"status" : false,
		"err": [
			{
				"code":"PRG-REVESE-DATA-SYNC-001",
				"message": "Failed to store Pre-Reg Ids"
			}
		],
		"resTime": "2018-10-17T13:40:19.590+0000"
}
```