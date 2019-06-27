
|Keywords| KeywordName/Purpose |Example|
|------|-----|-------|
|$TIMESTAMPZ$|To generate current timestamp with UTC format|2019-06-20T16:18:08.008Z|
|$TIMESTAMP$|To generate current timestamp with timezone format|2019-06-20T16:18:08.008+05:30|
|<li> $TIMESTAMP$HOUR+24 <li> $TIMESTAMP$HOUR-24 <li> $TIMESTAMP$MINUTE+23 <li> $TIMESTAMP$MINUTW-56 <li> $TIMESTAMP$SECOND+145 <li> $TIMESTAMP$SECOND-123|	To generate future or current timestamp	|


|$RANDOM:N:10$	|To generate random digit for the given number|<li> $RANDOM:N:10$ <li> $RANDOM:N:3$ <li> $RANDOM:N:14$|
|$UIN$|	To get random UIN number from uin.property file	|
| $UIN$:WITH:Deactivated#|	To get uin number from uin.property file where value contains Deactivated|	
|$VID$	|To get random VID from vid.property file where type as perpetual and status as ACTIVE 	|
|<li> $VID:WITH:Temporary$ <li> $VID:WITH:REVOKE$| To get random VID from vid.property file where value contains Temporary or Revoke	|
|$VID:WHERE:UIN:WITH:VALID$|	To get the VID from vid.property where uin.property value contains specified keyword after “WITH:”	|
|<li> $TestData:indvId_Vid_valid$ <li> $TestData:bio_finger_LeftIndex_subType$ <li> $TestData:bio_face_deviceCode$|	To get the random value form the list in the authenticationTestData.yml file.|	
|$input.bio-auth-request:AuthReq.transactionID$|	To get the already assigned for the filed.s|	<li> input.filename1: <li>   mappingName1: value1 <li>   mappingName2: value2 <li> ouput.filename2: <li>   mappingName3: $ input.filename: mappingName2$ <li> where mappingName3 has set as value2|
|<li>  $errors:RevokedVID:errorCode$ <li> $errors:InactiveVID:errorCode$	|Get error code for the mentioned key “RevokedVID” from the errorCodeMsg.yml file.|	
|<li> $errors:InactiveVID:errorMessage$ <li> $errors:RevokedVID:errorMessage$	| Get error message for the mentioned key “RevokedVID” from the errorCodeMsg.yml file.|
|<li> $idrepo~$input.bio-auth-request:AuthReq.individualId$~ DECODEFILE:individualBiometricsValue ~//BIR/BDBInfo[Type='Finger'][Subtype='Left IndexFinger']//following::BDB$ <li> $idrepo~$input.bio-auth-request:AuthReq.individualId$~ DECODEFILE:individualBiometricsValue ~//BIR/BDBInfo[Type='Face']//following::BDB$|	<li> To get biometric value for the UIN using cbeff File. It is combination of above listed keyword. <li> Where 
$idrepo -> keyword mandatory at start. <li> $input.bio-auth-request:AuthReq.individualId$ -> get the value from the previously mentioned field <li> individualBiometricsValue -> Mapping name in UINMapping/mapping.property <li> //BIR/BDBInfo[Type='Finger'][Subtype='Left IndexFinger']//following::BDB  -> cbeff xpath, where in this location biovalue will be saved for Left IndexFinger|	
|<li> $idrepo~$input.demo-auth-request:AuthReq.individualId$~valueaddressLine1:langcode:TestData:primary_lang_code$ <li>  $idrepo~$input.demo-auth-request:AuthReq.individualId$~valuecity:langcode:TestData:secondary_lang_code$	|<li> To get demographic data for the UIN and language. <li> **Where ** $idrepo -> keyword mandatory at start. <li>  $input.demo-auth-request:AuthReq.individualId$ ->  get the value from the previously mentioned field <li> valueaddressLine1 -> Mapping name in UINMapping/mapping.property <li> TestData:primary_lang_code -> keyword to get language code from the authenticationTestData.yml|
