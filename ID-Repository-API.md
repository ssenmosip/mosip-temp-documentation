Each ID generated for an Individual is uniquely identified by the UIN (Unique Identification Number). This is a central API which all other modules of MOSIP will use to retrieve an ID record.

This API will support the following features
 - Creation of a ID record
 - Lookup of an ID record based on the UIN
 - Updation of an ID record based on the UIN
 - Will not support search based on attributes of an ID

## 1. Create    

This operation will create a new ID record in the ID repository and store corresponding demographic and bio-metric documents. 

### Resource URL
### `POST /identity/v1.0/{UIN}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | yes | Id of the API | mosip.id.create | 
version | yes | version of the API | | 1.0
requesttime | yes | timestamp of the request | | 2018-12-11T06:12:25.288Z
request | yes | Request Body attributes | | 
request: registrationId | yes | registration id | | 
request: identity | yes | JSON body as per the ID object schema | | 
request: decouemnts | yes | Documents that are to be uploaded for any ID attribute | | 

**Example request**

```
{
  "id": "mosip.id.create",
  "version": "1.0",
  "requesttime": "2018-12-11T06:12:25.288Z",
  "request": {
    "registrationId": "12342343200065201812120100555",
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
      "CNIENumber": 6789545678909,
      "localAdministrativeAuthority": [
        {
          "language": "ara",
          "value": "سلمى"
        },
        {
          "language": "fra",
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

**Example response**    

```
{
  "id": "mosip.id.create",
  "version": "1.0",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    "status": "ACTIVATED",
    "entity": "http://mosip.io/identity/568469473107"
  }
}
```

## 2. Read         

This operation will retrieve an ID record from the ID repository for a given UIN (Unique Identification Number) and identity type as bio/demo/all. 
1. When type=bio is selected, individualBiometrics along with Identity details of the Individual are returned
2. When type=demo is selected, Demographic documents along with Identity details of the Individual are returned
3. When type=all is selected, both individualBiometrics and demographic documents are returned along with Identity details of the Individual
If no identity type is provided, stored Identity details of the Individual will be returned as a default response.

### Resource URL
### `GET /identity/v1.0/{UIN}?type=bio`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

**Example response**     

```
{
  "id": "mosip.id.read",
  "version": "1.0",
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
      "CNIENumber": 6789545678909,
      "localAdministrativeAuthority": [
        {
          "language": "ara",
          "value": "سلمى"
        },
        {
          "language": "fra",
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

## 3. Update   

This operation will update an existing ID record in the ID repository for a given UIN (Unique Identification Number)

### Resource URL
### `PATCH /identity/v1.0/{UIN}`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | Y | Id of the API | mosip.id.update | 
version | Y | version of the API | | 1.0
requesttime | Y | timestamp of the request | | 2018-12-11T06:12:25.288Z
request | Y | Request body attributes | | 
request: status | N | status of ID | | 
request: registrationId | Y | registration id | | 
request: identity | N | JSON body as per the ID object schema | | 
request: documents | N | Documents that are to be uploaded for any ID attribute | | 

**Example Request**     

```
{
  "id": "mosip.id.update",
  "version": "1.0",
  "requesttime": "2018-12-11T06:12:25.288Z",
  "request": {
    //JSON object as per the ID Object Schema defined by the system owner
    "registrationId": "12342343200065201812120100556",
    "status": "DEACTIVATED",
    "identity": {
      "email": "sample123@email.com",
      "individualBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "updated_bio_doc"
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

**Example response**    

```
{
  "id": "mosip.id.update",
  "version": "1.0",
  "responsetime": "2018-12-11T06:13:05.218Z",
  "response": {
    "status": "DEACTIVATED",
    "entity": "http://mosip.io/identity/568469473107"
  }
}
```