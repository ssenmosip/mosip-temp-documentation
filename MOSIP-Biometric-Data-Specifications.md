Multi modal biometrics (Fingerprint, Iris, Face...) will be a key component in MOSIP to identify and provide a unique identity to an Individual. The page details out the specifications for Biometrics data during data acquisition and verification.

- MOSIP will use CBEFF ISO 19795 - 1 format to store and transfer biometrics data
- MOSIP will use XML data format of CBEFF to store the biometrics data
- MOSIP will use OASIS patron format ISO/IEC JTC 1 SC 37 – biometrics , 
  Patron identified – 257, patron format identifier 7 (Please refer https://www.ibia.org/cbeff/iso/bir-header-identifiers 
  for details)
- All the biometrics data captured for an Individual is stored in a single XML file
- The biometrics data itself inside the CBEFF file will be in the respective ISO format encoded as base64 binary

# CBEFF XML format sample
Please refer to http://docs.oasis-open.org/bias/soap-profile/v1.0/errata02/os/cbeff.xsd for the XML schema of CBEFF XML format.
Below is a sample of CBEFF XML for all fingers, iris and face.

```
<?xml version='1.0' encoding="utf-8"?>
<bir xmlns="urn:oid:1.1.19785.0.257.1.7.0">
	<version major="1" minor="0" />
	<cbeff-version major="2" minor="0" />
	<bir-info integrity="false" />
	<bir>     <!-- left iris -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="9" type="iris"
			subtype="left" creation-date="20100308T113005Z" />
		<bdb> SUlSADEwMQA...=     </bdb>
	</bir>
	<bir>     <!-- right iris -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="9" type="iris"
			subtype="right" creation-date="20100308T113025Z" />
		<bdb> SUlSADEwMQA...=     </bdb>
	</bir>
	<bir>     <!-- first attempt of the right slap -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="7" type="finger"
			subtype="right pointer finger middle-finger ringfinger little-finger"
			creation-date="20100308T113115Z" />
		<bdb> RklSADEwMQA...=     </bdb>
	</bir>
	<bir>      <!-- second attempt of the right slap -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="7" type="finger"
			subtype="right pointer-finger middle-finger ringfinger little-finger"
			creation-date="20100308T113145Z" />
		<bdb> RklSADEwMQA...=     </bdb>
	</bir>
	<bir>     <!-- two thumbs -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="7" type="finger"
			subtype="left right thumb" creation-date="20100308T113235Z" />
		<bdb> RklSADEwMQA...=     </bdb>
	</bir>
	<bir>     <!-- left slap -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="7" type="finger"
			subtype="left pointer-finger middle-finger ringfinger little-finger"
			creation-date="20100308T113355Z" />
		<bdb> RklSADEwMQA...=     </bdb>
	</bir>
	<bir>     <!-- face -->
		<bir-info integrity="false" />
		<bdb-info format-owner="257" format-type="8" type="face"
			creation-date="20100308T113145Z" />
		<bdb> RkFDADEwMQA...=     </bdb>
	</bir>
</bir>

```

# Finger Print
MOSIP will use both image and minutiae of Finger Print. 

## Finger Print Image Record (FIR)

### Registration
 * Image specification - ISO/IEC 19794 - 4 
 * File format - ???
 * Number of Fingers - maximum 10; minimum - 1
 * Format - JPEG2000 (lossless)
 * Quality - NIST Fingerprint Quality (NFIQ) value of 1, 2 and 3 is acceptable
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

### Authentication (only minutiae based authentication is available in version 1)


## Finger Print Minutiae Record (FMR)

### Registration (Only FIR is captured during registration)

### Authentication 
 * Minutiae specification - ISO/IEC 19794 - 2
 * Record format - ???
 * Number of fingers - 1
 * Quality - NIST Fingerprint Quality (NFIQ) value of 1, 2 and 3 is acceptable
 * Transmission format - minutiae
 * Storage - minutiae

# IRIS
MOSIP will use Iris images only for registration and authentication

## IRIS Image Record (IIR)

### Registration
 * Image specification - ISO/IEC 19794 - 6
 * File format - ???
 * Number of eyes - 2
 * Format - JPEG2000 (lossless) 
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

### Authentication 
 * Image specification - ISO/IEC 19794 - 6
 * Record format - ???
 * Number of fingers - 1 or 2
 * Transmission format - JPEG2000 (lossless)
 * Storage - JPEG2000 or PNG

# Face
MOSIP will use face image for registration (Face authentication will come in a future release of MOSIP)

## Face Image Data (FID)

### Registration
 * Image specification - ISO/IEC 19794 - 5
 * Image details - Full frontal image, +/- 5 degrees rotation, 24 bit RGB, white background, 35 mm width, 45 mm height
 * Format - JPEG2000 or PNG (lossless) 
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

### Authentication (Future version)