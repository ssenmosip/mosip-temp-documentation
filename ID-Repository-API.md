Each ID generated for an Individual is uniquely identified by the UIN (Unique Identification Number). This is a central API which all other modules of MOSIP will use to retrieve an ID record.

This API will support the following features
 - Creation of a ID record
 - Lookup of an ID record based on the UIN
 - Updation of an ID record based on the UIN
 - Will not support search based on attributes of an ID

**1. Create**

This operation will create a new ID record in the ID repository and store corresponding demographic and biometric documents. 

### Resource URL
### `POST /identity/v1.0/568469473107`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
id | yes | Id of the API | mosip.id.create | 
ver | yes | version of the API | | 1.0
timestamp | yes | timestamp of the request | | 1539936202
registration-id | yes | registration id | | 
request | yes | JSON body as per the ID object schema | | 

**Example request**

```
{
  "id": "mosip.id.create",
  "version": "1.0",
  "timestamp": "2018-12-11T06:12:25.288",
  "registrationId": "12342343200065201812120100555",
  "request": {
    "identity": {
      "firstName": {
        "label": "First Name",
        "values": [
          {
            "language": "ar",
            "value": "ابراهيم"
          },
          {
            "language": "fr",
            "value": "Ibrahim"
          }
        ]
      },
      "middleName": {
        "label": "Middle Name",
        "values": [
          {
            "language": "ar",
            "value": "بن"
          },
          {
            "language": "fr",
            "value": "Ibn"
          }
        ]
      },
      "lastName": {
        "label": "Last Name",
        "values": [
          {
            "language": "ar",
            "value": "علي"
          },
          {
            "language": "fr",
            "value": "Ali"
          }
        ]
      },
      "dateOfBirth": {
        "label": "Date Of Birth",
        "value": "1955/04/15"
      },
      "gender": {
        "label": "Gender",
        "values": [
          {
            "language": "ar",
            "value": "الذكر"
          },
          {
            "language": "fr",
            "value": "mâle"
          }
        ]
      },
      "addressLine1": {
        "label": "Address Line 1",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر 1"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 1"
          }
        ]
      },
      "addressLine2": {
        "label": "Address Line 2",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر 2"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 2"
          }
        ]
      },
      "addressLine3": {
        "label": "Address Line 3",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر3"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 3"
          }
        ]
      },
      "region": {
        "label": "Region",
        "values": [
          {
            "language": "ar",
            "value": "طنجة - تطوان - الحسيمة"
          },
          {
            "language": "fr",
            "value": "Tanger-Tétouan-Al Hoceima"
          }
        ]
      },
      "province": {
        "label": "Province",
        "values": [
          {
            "language": "ar",
            "value": "فاس-مكناس"
          },
          {
            "language": "fr",
            "value": "Fès-Meknès"
          }
        ]
      },
      "city": {
        "label": "City",
        "values": [
          {
            "language": "ar",
            "value": "الدار البيضاء"
          },
          {
            "language": "fr",
            "value": "Casablanca"
          }
        ]
      },
      "postalCode": "570004",
      "phone": {
        "label": "Land Line",
        "value": "+212-5398-12345"
      },
      "email": {
        "label": "Business Email",
        "value": "sample@samplamail.com"
      },
      "CNIENumber": "6789545678909",
      "parentOrGuardianName": {
        "label": "Parent/Guardian",
        "values": [
          {
            "language": "ar",
            "value": "سلمى"
          },
          {
            "language": "fr",
            "value": "salma"
          }
        ]
      },
      "parentOrGuardianRIDOrUIN": "212124324784912",
      "proofOfAddress": {
        "format": "pdf",
        "category": "drivingLicense",
        "value": "PoA_drivingLicense"
      },
      "proofOfIdentity": {
        "format": "txt",
        "category": "passport",
        "value": "PoI_passport"
      },
      "proofOfRelationship": {
        "format": "pdf",
        "category": "passport",
        "value": "PoR_passport"
      },
      "individualBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "test_bio"
      },
      "parentOrGuardianBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "test_parent_bio"
      }
    },
    "documents": [
      {
        "type": "proofOfAddress",
        "value": "<Base 64 encoded byte array of PoA document>"
      },
      {
        "type": "proofOfIdentity",
        "value": "<Base 64 encoded byte array of PoI document>"
      },
      {
        "type": "proofOfRelationship",
        "value": "<Base 64 encoded byte array of PoR document>"
      },
      {
        "type": "individualBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      },
      {
        "type": "parentOrGuardianBiometrics",
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
  "timestamp": "2018-12-11T06:13:05.218",
  "status": "ACTIVATED",
  "err": [],
  "response": {
    "entity": "http://mosip.io/identity/568469473107"
  }
}
```


**2. Read **

This operation will retrieve an ID record from the ID repository for a given UIN (Unique Identification Number) and identity type as bio/demo/all. 
If no identity type is provided, stored identity will be returned as a default response. If any of the identity type - bio and/or demo or all is present, their respective documents will be returned along with stored identity details.

### Resource URL
### `GET /identity/v1.0/568469473107?type=bio`

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
  "timestamp": "2018-12-11T06:13:05.218",
  "status": "ACTIVATED",
  "err": [],
  "response": {
    //JSON object as per the ID Object Schema defined by the system owner
    "identity": {
      "firstName": {
        "label": "First Name",
        "values": [
          {
            "language": "ar",
            "value": "ابراهيم"
          },
          {
            "language": "fr",
            "value": "Ibrahim"
          }
        ]
      },
      "middleName": {
        "label": "Middle Name",
        "values": [
          {
            "language": "ar",
            "value": "بن"
          },
          {
            "language": "fr",
            "value": "Ibn"
          }
        ]
      },
      "lastName": {
        "label": "Last Name",
        "values": [
          {
            "language": "ar",
            "value": "علي"
          },
          {
            "language": "fr",
            "value": "Ali"
          }
        ]
      },
      "dateOfBirth": {
        "label": "Date Of Birth",
        "value": "1955/04/15"
      },
      "gender": {
        "label": "Gender",
        "values": [
          {
            "language": "ar",
            "value": "الذكر"
          },
          {
            "language": "fr",
            "value": "mâle"
          }
        ]
      },
      "addressLine1": {
        "label": "Address Line 1",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر 1"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 1"
          }
        ]
      },
      "addressLine2": {
        "label": "Address Line 2",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر 2"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 2"
          }
        ]
      },
      "addressLine3": {
        "label": "Address Line 3",
        "values": [
          {
            "language": "ar",
            "value": "عنوان العينة سطر3"
          },
          {
            "language": "fr",
            "value": "exemple d'adresse ligne 3"
          }
        ]
      },
      "region": {
        "label": "Region",
        "values": [
          {
            "language": "ar",
            "value": "طنجة - تطوان - الحسيمة"
          },
          {
            "language": "fr",
            "value": "Tanger-Tétouan-Al Hoceima"
          }
        ]
      },
      "province": {
        "label": "Province",
        "values": [
          {
            "language": "ar",
            "value": "فاس-مكناس"
          },
          {
            "language": "fr",
            "value": "Fès-Meknès"
          }
        ]
      },
      "city": {
        "label": "City",
        "values": [
          {
            "language": "ar",
            "value": "الدار البيضاء"
          },
          {
            "language": "fr",
            "value": "Casablanca"
          }
        ]
      },
      "postalCode": "570004",
      "phone": {
        "label": "Land Line",
        "value": "+212-5398-12345"
      },
      "email": {
        "label": "Business Email",
        "value": "sample@samplamail.com"
      },
      "CNIENumber": "6789545678909",
      "parentOrGuardianName": {
        "label": "Parent/Guardian",
        "values": [
          {
            "language": "ar",
            "value": "سلمى"
          },
          {
            "language": "fr",
            "value": "salma"
          }
        ]
      },
      "parentOrGuardianRIDOrUIN": "212124324784912",
      "proofOfAddress": {
        "format": "pdf",
        "category": "drivingLicense",
        "value": "PoA_drivingLicense"
      },
      "proofOfIdentity": {
        "format": "txt",
        "category": "passport",
        "value": "PoI_passport"
      },
      "proofOfRelationship": {
        "format": "pdf",
        "category": "passport",
        "value": "PoR_passport"
      },
      "individualBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "test_bio"
      },
      "parentOrGuardianBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "test_parent_bio"
      }
    },
    "documents": [
      {
        "type": "individualBiometrics",
        "value": "<Base 64 encoded byte array of CBEFF document>"
      }
    ]
  }
}
```

**3. Update**

This operation will update an existing ID record in the ID repository for a given UIN (Unique Identification Number)

### Resource URL
### `PATCH /identity/568469473107`

### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

**Example Request**     

```
{
  "id": "mosip.id.update",
  "version": "1.0",
  "timestamp": "2018-12-11T06:12:25.288",
  "registrationId": "12342343200065201812120100556",
  "status": "DEACTIVATED",
  "request": {
    //JSON object as per the ID Object Schema defined by the system owner
    "identity": {
      "email": {
        "label": "Business Email",
        "value": "sample123@email.com"
      },
      "individualBiometrics": {
        "format": "cbeff",
        "version": 1.0,
        "value": "updated_bio_doc"
      }
    },
    "documents": [
      {
        "type": "individualBiometrics",
        "value": "<Base 64 encoded byte array of updated CBEFF document>"
      }
    ]
  }
}
```

**Example response**    

```
{
	"id" : "mosip.id.update",
	"version" : "1.0",
	"timestamp" : "2018-12-11T06:13:05.218",
	"status" : "DEACTIVATED",
	"err" : [],
	"response" : {
		"entity" : "http://mosip.io/identity/568469473107"
	}	
}
```