Multi modal biometrics (Fingerprint, Iris, Face...) will be a key component in MOSIP to identify and provide a unique identity to an Individual. The page details out the specifications for Biometrics data during data acquisition and verification.

MOSIP will use CBEFF ISO 19795 - 1 format to store and transfer biometrics data.

# Finger Print
MOSIP will use both image and minutiae of Finger Print. 

## Finger Print Image Record (FIR)

### Registration
 * Image specification - ISO/IEC 19794 - 4 
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