This section details about the REST services in ID Repository module.
* [ID Services](#identity-services-private)
* [VID Services](#vid-services-private)

## Identity Services (Private)
These services is used by Registration Processor to store/update during registration process and ID Authentication to retrieve Identity of an Individual for their authentication.

#### Users of Identity service -
1. `Registration Processor` - *Registration Processor* will create a new ID record or update an existing ID record in ID repository and store corresponding demographic and bio-metric documents. *Registration Processor* can also retrieve Identity details of an Individual using RID.
2. `ID Authentication` - *ID Authentication* can retrieve Identity details of an Individual using UIN for authenticating purpose.

* [POST /idrepository/v1/identity](#post-idrepositoryv1identity)
* [GET /idrepository/v1/identity/UIN/{UIN}?type=bio](#get-idrepositoryv1identityuinuintypebio)
* [GET /idrepository/v1/identity/RID/{RID}?type=bio](#get-idrepositoryv1identityridridtypebio)
* [PATCH /idrepository/v1/identity](#patch-idrepositoryv1identity)     

**Note** - Identity Services does not support search based on attributes of an ID.

### POST /idrepository/v1/identity     

This service will create a new ID record in ID repository and store corresponding demographic and bio-metric documents. 

#### Resource URL
<div>https://mosip.io/idrepository/v1/identity</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | yes | Id of the API | mosip.id.create | 
version | yes | version of the API | | v1
requesttime | yes | timestamp of the request | | 2018-12-11T06:12:25.288Z
request | yes | Request Body attributes | | 
request: registrationId | yes | registration id | | 
request: biometricReferenceId | yes | ABIS Reference ID | | 
request: identity | yes | JSON body as per ID object schema | | 
request: documents | yes | Documents that are to be uploaded for any ID attribute | | 

#### Request:
```JSON
{
  "id": "mosip.id.create",
  "version": "v1",
  "requesttime": "2018-12-11T06:12:25.288Z",
  "request": {
    "registrationId": "12342343200065201812120100555",
    "biometricReferenceId": "<ABIS Reference ID>",
    "identity": {
      "IDSchemaVersion": 1,
      "UIN": 981576026435,
      "fullName": [
        {
          "language": "ara",
          "value": "ابراهيم بن علي"
        },
        {
          "language": "fra",
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
          "language": "fra",
          "value": "mâle"
        }
      ],
      "addressLine1": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 1"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 2"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 3"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 3"
        }
      ],
      "region": [
        {
          "language": "ara",
          "value": "طنجة - تطوان - الحسيمة"
        },
        {
          "language": "fra",
          "value": "Tanger-Tétouan-Al Hoceima"
        }
      ],
      "province": [
        {
          "language": "ara",
          "value": "فاس-مكناس"
        },
        {
          "language": "fra",
          "value": "Fès-Meknès"
        }
      ],
      "city": [
        {
          "language": "ara",
          "value": "الدار البيضاء"
        },
        {
          "language": "fra",
          "value": "Casablanca"
        }
      ],
      "postalCode": "570004",
      "phone": "9876543210",
      "email": "abc@xyz.com",
      "parentOrGuardianRIDOrUIN": 212124324784912,
      "parentOrGuardianName": [
        {
          "language": "ara",
          "value": "سلمى"
        },
        {
          "language": "fra",
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
        "version": 1,
        "value": "fileReferenceID"
      },
      "parentOrGuardianBiometrics": {
        "format": "cbeff",
        "version": 1,
        "value": "fileReferenceID"
      }
    },
    "documents": [
      {
        "category": "proofOfAddress",
        "value": "<Base 64 encoded byte array of PoA document>"
      },
      {
        "category": "proofOfIdentity",
        "value": "<Base 64 encoded byte array of PoI document>"
      },
      {
        "category": "proofOfRelationship",
        "value": "<Base 64 encoded byte array of PoR document>"
      },
      {
        "category": "individualBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      },
      {
        "category": "parentOrGuardianBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      }
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Identity stored successfully
```JSON
{
  "id": "mosip.id.create",
  "version": "v1",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    "status": "ACTIVATED",
    "entity": "http://mosip.io/idrepository/v1/identity/UIN/{UIN}"
  }
}
```

### GET /idrepository/v1/identity/UIN/{UIN}?type=bio         

This service will retrieve an ID record from ID repository for a given UIN (Unique Identification Number) and identity type as bio/demo/all. 
1. When type=bio is selected, individualBiometrics along with Identity details of the Individual are returned
2. When type=demo is selected, Demographic documents along with Identity details of the Individual are returned
3. When type=all is selected, both individualBiometrics and demographic documents are returned along with Identity details of the Individual    

If no identity type is provided, stored Identity details of the Individual will be returned as a default response.

#### Resource URL
<div>https://mosip.io/idrepository/v1/identity/UIN/{UIN}?type=bio</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses: 
##### Success Response:
###### Status code: '200'
###### Description: Identity retrieved successfully 
```JSON
{
  "id": "mosip.id.read",
  "version": "v1",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    //JSON object as per the ID Object Schema defined by the system owner
    "status": "ACTIVATED",
    "identity": {
      "IDSchemaVersion": 1.0,
      "UIN": 981576026435,
      "fullName": [
        {
          "language": "ara",
          "value": "ابراهيم بن علي"
        },
        {
          "language": "fra",
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
          "language": "fra",
          "value": "mâle"
        }
      ],
      "addressLine1": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 1"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 2"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 3"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 3"
        }
      ],
      "region": [
        {
          "language": "ara",
          "value": "طنجة - تطوان - الحسيمة"
        },
        {
          "language": "fra",
          "value": "Tanger-Tétouan-Al Hoceima"
        }
      ],
      "province": [
        {
          "language": "ara",
          "value": "فاس-مكناس"
        },
        {
          "language": "fra",
          "value": "Fès-Meknès"
        }
      ],
      "city": [
        {
          "language": "ara",
          "value": "الدار البيضاء"
        },
        {
          "language": "fra",
          "value": "Casablanca"
        }
      ],
      "postalCode": "570004",
      "phone": "9876543210",
      "email": "abc@xyz.com",
      "parentOrGuardianRIDOrUIN": 212124324784912,
      "parentOrGuardianName": [
        {
          "language": "ara",
          "value": "سلمى"
        },
        {
          "language": "fra",
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
    },
    "documents": [
      {
        "category": "individualBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      }
    ]
  }
}
```

### GET /idrepository/v1/identity/RID/{RID}?type=bio         

This operation will retrieve an ID record from ID repository for a given RID (Registration ID) and identity type as bio/demo/all. 
1. When type=bio is selected, individualBiometrics along with Identity details of Individual are returned
2. When type=demo is selected, Demographic documents along with Identity details of Individual are returned
3. When type=all is selected, both individualBiometrics and demographic documents are returned along with Identity details of Individual    

If no identity type is provided, stored latest Identity details of Individual mapped to the UIN of input RID will be returned as a default response.

#### Resource URL
<div>https://mosip.io/idrepository/v1/identity/RID/{RID}?type=bio</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Responses: 
##### Success Response:
###### Status code: '200'
###### Description: Identity retrieved successfully 
```JSON
{
  "id": "mosip.id.read",
  "version": "v1",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    //JSON object as per the ID Object Schema defined by the system owner
    "status": "ACTIVATED",
    "identity": {
      "IDSchemaVersion": 1.0,
      "UIN": 981576026435,
      "fullName": [
        {
          "language": "ara",
          "value": "ابراهيم بن علي"
        },
        {
          "language": "fra",
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
          "language": "fra",
          "value": "mâle"
        }
      ],
      "addressLine1": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 1"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 1"
        }
      ],
      "addressLine2": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 2"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 2"
        }
      ],
      "addressLine3": [
        {
          "language": "ara",
          "value": "عنوان العينة سطر 3"
        },
        {
          "language": "fra",
          "value": "exemple d'adresse ligne 3"
        }
      ],
      "region": [
        {
          "language": "ara",
          "value": "طنجة - تطوان - الحسيمة"
        },
        {
          "language": "fra",
          "value": "Tanger-Tétouan-Al Hoceima"
        }
      ],
      "province": [
        {
          "language": "ara",
          "value": "فاس-مكناس"
        },
        {
          "language": "fra",
          "value": "Fès-Meknès"
        }
      ],
      "city": [
        {
          "language": "ara",
          "value": "الدار البيضاء"
        },
        {
          "language": "fra",
          "value": "Casablanca"
        }
      ],
      "postalCode": "570004",
      "phone": "9876543210",
      "email": "abc@xyz.com",
      "parentOrGuardianRIDOrUIN": 212124324784912,
      "parentOrGuardianName": [
        {
          "language": "ara",
          "value": "سلمى"
        },
        {
          "language": "fra",
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
    },
    "documents": [
      {
        "category": "individualBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      }
    ]
  }
}
```

### PATCH /idrepository/v1/identity      
This operation will update an existing ID record in the ID repository for a given UIN (Unique Identification Number)

#### Resource URL
<div>https://mosip.io/idrepository/v1/identity/RID/{RID}?type=bio</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | Id of the API | mosip.id.update | 
version | Y | version of the API | | v1
requesttime | Y | timestamp of the request | | 2018-12-11T06:12:25.288Z
request | Y | Request body attributes | | 
request: status | N | status of ID | | 
request: registrationId | Y | Registration id | | 
request: biometricReferenceId | N | ABIS Reference Id | | 
request: identity | N | JSON body as per the ID object schema | | 
request: documents | N | Documents that are to be uploaded for any ID attribute | | 

#### Request:
```JSON
{
  "id": "mosip.id.update",
  "version": "v1",
  "requesttime": "2018-12-11T06:12:25.288Z",
  "request": {
    //JSON object as per the ID Object Schema defined by the system owner
    "registrationId": "12342343200065201812120100556",
    "biometricReferenceId": "<ABIS Reference ID>",
    "status": "DEACTIVATED",
    "identity": {
      "email": "sample123@email.com",
      "individualBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "updated_bio_doc_name"
      }
    },
    "documents": [
      {
        "category": "individualBiometrics",
        "value": "<Base 64 encoded byte array of updated CBEFF document>"
      }
    ]
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: Identity updated successfully
```JSON
{
  "id": "mosip.id.update",
  "version": "v1",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    "status": "DEACTIVATED",
    "entity": "http://mosip.io/identity/568469473107"
  }
}
```

## VID Services (Private)
* [POST /idrepository/v1/vid](#post-idrpositoryv1vid)
* [GET /idrepository/v1/vid/{VID}](#get-idrepositoryv1vid)

### POST /idrepository/v1/vid        
This service will create a new VID based on VID type provided.

#### Resource URL
<div>https://mosip.io/idrepository/v1/vid</div>

#### Resource details     
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | yes | Id of the API | mosip.vid.create | 
version | yes | version of the API | | v1
requesttime | yes | timestamp of the request | | 2019-04-30T06:12:25.288Z
request | yes | Request Body attributes | | 
request: vidType | yes | VID Type |  | Perpetual or Temporary 
request: UIN| yes | Individual's UIN |  | 981576026435

#### Request:
```JSON
{
  "id": "mosip.vid.create",
  "version": "v1",
  "requesttime": "2019-04-30T06:12:25.288Z",
  "request": {
    "vidType": "Perpetual",
    "UIN": 981576026435
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: VID created successfully
```
{
  "id": "mosip.vid.create",
  "version": "v1",
  "responsetime": "2019-04-30T06:13:05.218Z",
  "response": {
    "status": "ACTIVE",
    "VID": 1234512345
  }
}
```
 
 ### GET /idrepository/v1/vid/{VID}        
This service will retrieve associated decrypted UIN for a given VID, once VID is successfully validated.

#### Resource URL
<div>https://mosip.io/idrepository/v1/vid/{VID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes


#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: UIN for a given VID retrieved successfully
```
{
  "id": "mosip.vid.read",
  "version": "v1",
  "responsetime": "2019-04-30T06:13:05.218Z",
  "response": {
    "UIN": 981576026435
  }
}
```

 ### PATCH /idrepository/v1/vid/{VID}   
This service will update status associated with a given VID, if the current status of VID is 'ACTIVE'.

#### Resource URL
<div>https://mosip.io/idrepository/v1/vid/{VID}</div>

#### Resource details
Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Request Body Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | yes | Id of the API | mosip.vid.update | 
version | yes | version of the API | | v1
requesttime | yes | timestamp of the request | | 2019-04-30T06:12:25.288Z
request | yes | Request Body attributes | | 
request: vidStatus | yes | status of VID | | USED or REVOKED or EXPIRED

#### Request:
```JSON
{
  "id": "mosip.vid.update",
  "version": "v1",
  "requesttime": "2019-04-30T06:12:25.288Z",
  "request": {
    "vidStatus": 'REVOKED'
  }
}
```

#### Responses:
##### Success Response:
###### Status code: '200'
###### Description: VID status updated successfully
```JSON
{
  "id": "mosip.vid.update",
  "version": "v1",
  "responsetime": "2019-04-30T06:13:05.218Z",
  "response": {
    "vidStatus": 'REVOKED'
  }
}
```