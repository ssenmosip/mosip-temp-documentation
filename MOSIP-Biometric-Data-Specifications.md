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
<?xml version="1.0" encoding="UTF-8"?>
<BIR xmlns="http://docs.oasis-open.org/bias/ns/biaspatronformat-1.0/">
    <Version>
        <Major>2</Major>
        <Minor>1</Minor>
    </Version>
    <CBEFFVersion>
        <Major>2</Major>
        <Minor>1</Minor>
    </CBEFFVersion>
    <BIRInfo>
        <Integrity>false</Integrity>
    </BIRInfo>
    <BIR>
	   <!-- face -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>8</FormatType>
            <CreationDate>2018-12-18T12:18:35.662+05:30</CreationDate>
            <Type>Face</Type>
            <Subtype></Subtype>
            <Level>Intermediate</Level>
            <Purpose>Enroll</Purpose>
            <Quality>90</Quality>
        </BDBInfo>
        <BDB>RmFjZQ...==</BDB>
    </BIR>
    <BIR>
	   <!-- left slap -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>7</FormatType>
            <CreationDate>2018-12-18T12:18:35.667+05:30</CreationDate>
            <Type>Finger</Type>
            <Subtype>Left IndexFinger MiddleFinger RingFinger LittleFinger</Subtype>
            <Level>Raw</Level>
            <Purpose>Enroll</Purpose>
            <Quality>80</Quality>
        </BDBInfo>
        <BDB>UmlnH5...=</BDB>
    </BIR>
    <BIR>
	  <!-- right slap -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>7</FormatType>
            <CreationDate>2018-12-18T12:18:35.667+05:30</CreationDate>
            <Type>Finger</Type>
            <Subtype>Right IndexFinger MiddleFinger RingFinger LittleFinger</Subtype>
            <Level>Raw</Level>
            <Purpose>Enroll</Purpose>
            <Quality>80</Quality>
        </BDBInfo>
        <BDB>TGVdCB...=</BDB>
    </BIR>
    <BIR>
	   <!-- two thumbs -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>7</FormatType>
            <CreationDate>2018-12-18T12:18:35.667+05:30</CreationDate>
            <Type>Finger</Type>
            <Subtype>Left Right Thumb</Subtype>
            <Level>Raw</Level>
            <Purpose>Enroll</Purpose>
            <Quality>80</Quality>
        </BDBInfo>
        <BDB>GVmdAC...=</BDB>
    </BIR>
    <BIR>
	  <!-- right iris -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>9</FormatType>
            <CreationDate>2018-12-18T12:18:35.667+05:30</CreationDate>
            <Type>Iris</Type>
            <Subtype>Right</Subtype>
            <Level>Raw</Level>
            <Purpose>Enroll</Purpose>
            <Quality>80</Quality>
        </BDBInfo>
        <BDB>UmlnaH...=</BDB>
    </BIR>
    <BIR>
	   <!-- left iris -->
        <BIRInfo>
            <Integrity>false</Integrity>
        </BIRInfo>
        <BDBInfo>
            <FormatOwner>257</FormatOwner>
            <FormatType>9</FormatType>
            <CreationDate>2018-12-18T12:18:35.668+05:30</CreationDate>
            <Type>Iris</Type>
            <Subtype>Left</Subtype>
            <Level>Raw</Level>
            <Purpose>Enroll</Purpose>
            <Quality>80</Quality>
        </BDBInfo>
        <BDB>TGVmdS...=</BDB>
    </BIR>
</BIR>
```
# Data standards for Registration

## Finger Print

### Finger Print Image Record (FIR)
 * Image specification - ISO/IEC 19794 - 4 
 * File format - ???
 * Number of Fingers - maximum 10; minimum - 1
 * Format - JPEG2000 (lossless)
 * Quality - NIST Fingerprint Quality (NFIQ) value of 1, 2 and 3 is acceptable
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

### Finger Print Minutiae Record (FMR)
Only FIR is captured during registration

## IRIS
MOSIP will use Iris images only for registration

### IRIS Image Record (IIR)
 * Image specification - ISO/IEC 19794 - 6
 * File format - ???
 * Number of eyes - 2
 * Format - JPEG2000 (lossless) 
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

## Face
MOSIP will use face image for registration

### Face Image Data (FID)
 * Image specification - ISO/IEC 19794 - 5
 * Image details - Full frontal image, +/- 5 degrees rotation, 24 bit RGB, white background, 35 mm width, 45 mm height
 * Format - JPEG2000 or PNG (lossless) 
 * Transmission format - JPEG2000
 * Storage - JPEG2000 or PNG

# Data standards for Authentication
## Finger Print
Only minutiae based authentication is available in version 1

### Finger Print Minutiae Record (FMR)
 * Minutiae specification - ISO/IEC 19794 - 2
 * Record format - ???
 * Number of fingers - 1 or 2
 * Quality - NIST Fingerprint Quality (NFIQ) value of 1, 2 and 3 is acceptable
 * Transmission format - minutiae
 * Storage - minutiae

## IRIS
MOSIP will use Iris images only authentication

### IRIS Image Record (IIR)
 * Image specification - ISO/IEC 19794 - 6
 * Record format - ???
 * Number of eyes - 1 or 2
 * Transmission format - JPEG2000 (lossless)
 * Storage - JPEG2000 or PNG

## Face
Face authentication will come in a future release of MOSIP