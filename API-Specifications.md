# MOSIP API List
This page and its sub-pages will have the API specifications of various features of MOSIP

## Kernel
### Public key-get service

This service will provides the public key of the Enrolment client. 

#### Resource URL
#### `GET /publickey`

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description |  Example
-----|----------|-------------|--------
applicationId |Yes|Id of the application| REGISTRATION,IDA
referenceId|Yes|Id of the Machine/TSP|
timeStamp |Yes|Date-time without time-zone in ISO-8601| 2007-12-03T10:15:30

#### Example Request
/publickey/REGISTRATION?referenceId=1001&timeStamp=2018-11-29T12%3A00

#### Example Response
```JSON
{
  "publicKey": "publicKey",
  "keyExpiryTime": "keyExpiryTime",
  "keyGenerationTime": "keyGenerationTime"
}
```
### Sync Master data-get service

This service will provides the list of all master data. This service is used mainly by the Enrolment client module. In case, other modules calls this service, the machineid will be empty. The machineid will be used to get the location and based on the location, the holiday list will be retrieved. If the requestdate is not passed, all the master data will be returned. If the requestdate is passed, all the data will be returned for which the created or updated date is greater than equal request date. 

#### Resource URL
#### `GET /syncmasterdata`

#### Resource details

Resource Details | Description
------------ | -------------
Response format | JSON
Requires Authentication | Yes

#### Parameters
Name | Required | Description | Default Value | Example
-----|----------|-------------|---------------|--------
machineid|No|Id of the machine| | 
requestdate|No|Date in ISO format| | 

#### Example Request
-NA-

#### Example Response
```JSON
{
   "holidays":[
      {
         "holidayID":"string",
         "holidayDate":"string",
         "holidayName":"string",
         "holidayDay":"string",
         "holidayMonth":"string",
         "holidayYear":"string",
         "languagecode":"string"
      }
   ],
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
      },
      {
         "id":"string",
         "value":"asdf",
         "languagecode":"string"
      }
   ],
   "machinetypes":[
      {
         "machinetypecode":"string",
         "machinename":"string",
         "description":"string",
         "languagecode":"boolean",
         "isactive":"string"
      },
      {
         "machinetypecode":"string",
         "machinename":"string",
         "description":"string",
         "languagecode":"boolean",
         "isactive":"string"
      }
   ],
   "successfully_updated_documenttypes":[
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      },
      {
         "code":"code",
         "name":"name",
         "descr":"descr",
         "lang_code":"lang_code",
         "is_active":"is_active"
      }
   ],
   "packetonholdreasons":[
      {
         "packetonholdreasonid":"string",
         "packetonholdreasondesc":"string",
         "languagecode":"string"
      },
      {
         "packetonholdreasonid":"string",
         "packetonholdreasondesc":"string",
         "languagecode":"string"
      }
   ],
   "packetrejectionreasons":[
      {
         "packetrejectionreasonid":"string",
         "packetrejectionreasondesc":"string",
         "languagecode":"string",
         "locationcode":"string"
      },
      {
         "packetrejectionreasonid":"string",
         "packetrejectionreasondesc":"string",
         "languagecode":"string",
         "locationcode":"string"
      }
   ],
   "reason_category":[
      {
         "code":"string",
         "name":"string",
         "desc":"string",
         "lang_code":"string",
         "reason_lists":[
            {
               "code":"string",
               "name":"string",
               "desc":"string",
               "lang_code":"string"
            },
            {
               "code":"string",
               "name":"string",
               "desc":"string",
               "lang_code":"string"
            }
         ]
      }
   ],
   "locations":[
      {
         "locationHierarchylevel":"number",
         "locationHierarchyName":"string",
         "isActive":true
      },
      {
         "locationHierarchylevel":"number",
         "locationHierarchyName":"string",
         "isActive":true
      }
   ],
   "biometricattributes":[
      {
         "biometricattribute":[
            {
               "biometricatributeid":"string"
            },
            {
               "biometricattribute":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "biometricattribute":[
            {
               "biometricatributeid":"string"
            },
            {
               "biometricattribute":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "registrationcenters":[
      {
         "registrationcentername":"",
         "centertypecode":"",
         "addressline1":"",
         "addressline2":"",
         "addressline3 ":"",
         "longitude ":"",
         "latitude":"",
         "contactphone":"",
         "numberofkiosks":"",
         "workinghours":"",
         "perkioskprocesstime":"",
         "officestarttime":"",
         "officeendtime":"",
         "holidaylocationcode":"",
         "isactive":"",
         "centertype":"",
         "address":"",
         "contactnumber":"",
         "pincode":"",
         "locationcode":""
      },
      {
         "registrationcentername":"",
         "centertypecode":"",
         "addressline1":"",
         "addressline2":"",
         "addressline3 ":"",
         "longitude ":"",
         "latitude":"",
         "contactphone":"",
         "numberofkiosks":"",
         "workinghours":"",
         "perkioskprocesstime":"",
         "officestarttime":"",
         "officeendtime":"",
         "holidaylocationcode":"",
         "isactive":"",
         "centertype":"",
         "address":"",
         "contactnumber":"",
         "pincode":"",
         "locationcode":""
      }
   ],
   "applicationtypes":[
      {
         "applicationtype":[
            {
               "applicationtypeid":"string"
            },
            {
               "applicationtypetype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "applicationtype":[
            {
               "applicationtypeid":"string"
            },
            {
               "applicationtypetype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "idtypes":[
      {
         "code":"string",
         "descr":"string",
         "languagecode":"string"
      },
      {
         "code":"string",
         "descr":"string",
         "languagecode":"string"
      }
   ],
   "biometrictypes":[
      {
         "biometrictype":[
            {
               "biometrictypeid":"string"
            },
            {
               "biometrictype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "biometrictype":[
            {
               "biometrictypeid":"string"
            },
            {
               "biometrictype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "titles":[
      {
         "title":[
            {
               "titleid":"string"
            },
            {
               "titletype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "title":[
            {
               "titleid":"string"
            },
            {
               "titletype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "genders":[
      {
         "gender":[
            {
               "genderid":"string"
            },
            {
               "gendertype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      },
      {
         "gender":[
            {
               "genderid":"string"
            },
            {
               "gendertype":"string"
            },
            {
               "languagecode":"string"
            }
         ]
      }
   ],
   "languages":[
      {
         "language":[
            {
               "languagecode":"string"
            },
            {
               "languagename":"string"
            }
         ]
      },
      {
         "language":[
            {
               "languagecode":"string"
            },
            {
               "languagename":"string"
            }
         ]
      }
   ],
   "devices":[
      {
         "devicetype":"string",
         "devicemodel":"string",
         "languagecode":"string"
      },
      {
         "devicetype":"string",
         "devicemodel":"string",
         "languagecode":"string"
      }
   ],
   "machines":[
      {
         "machineid":"string",
         "machinename":"string",
         "macid":"string",
         "serialnumber":"string",
         "isactive":"boolean",
         "languagecode":"string"
      },
      {
         "machineid":"string",
         "machinename":"string",
         "macid":"string",
         "serialnumber":"string",
         "isactive":"boolean",
         "languagecode":"string"
      }
   ],
   "documentformats":[
      {
         "id":"id",
         "format":"pdf",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"png",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"jpeg",
         "languagecode":"string"
      },
      {
         "id":"id",
         "format":"gif",
         "languagecode":"string"
      }
   ],
   "documentcategories":[
      {
         "id":"id",
         "value":"POA",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POI",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POR",
         "languagecode":"string"
      },
      {
         "id":"id",
         "value":"POB",
         "languagecode":"string"
      }
   ]
}
```
## Authentication
AM: Put auth list here
* Auth API 1
* Auth API 2

## Pre-Registration
* [Service APIs](https://github.com/mosip/mosip/wiki/Pre-Registration-APIs)

## Registration-Processor
* [Registration-Processor APIs](https://github.com/mosip/mosip/wiki/Registration-Processor-APIs) 

## Registration
* [Registration APIs](https://github.com/mosip/mosip/wiki/Registration-APIs) 

# ABIS APIs

https://github.com/mosip/mosip/wiki/ABIS-APIs
