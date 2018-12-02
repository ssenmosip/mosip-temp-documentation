Biometrics (Fingerprint, Iris and Face) will be a key component in MOSIP to identify and provide a unique identity to an Individual. The page details out the specifications for Biometrics data during data acquisition and verification.

# Finger Print
MOSIP will use both image and minutiae of Finger Print. 

## Finger Print Image Record (FIR)

### Registration
 * Image specification - ISO/IEC 19794 - 4
 * Image record format - CBEFF ISO 19795 - 1
 * Number of Fingers - maximum 10; minimum - 1
 * Format - JPEG2000 
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
