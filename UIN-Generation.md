* **UIN Generation** _(UIG_FR_1)_

MOSIP generates a pool of UINs before the registration process and stores them. 
The number of UINs to be generated in a pool depends on a configuration to be done by the country depending on the peak registration requirements. UIN generation service will receive a request by Registration Processor to get a UIN. The service responds with an un-allocated UIN from the generated Pool. 
When the pool reaches a configured number of minimum UINs, MOSIP generates another pool of UIN. 


The UINs generated follow the following policies:


1. UIN should not contain any alphanumeric characters
1. UIN should not contain any repeating numbers for 2 or more than 2 digits
1. UIN should not contain any sequential number for 3 or more than 3 digits
1. UIN should not be generated sequentially
1. UIN should not have repeated block of numbers for 2 or more than 2 digits
1. The last digit in the number should be reserved for a checksum
1. The number should not contain '0' or '1' as the first digit.
1. First 5 digits should be different from the last 5 digits (E.g. 4345643456)
1. First 5 digits should be different to the last 5 digits reversed (E.g. 4345665434)
1. UIN should not be an ascending or descending cyclic figure (E.g. 4567890123, 6543210987)
1. UIN should be different from the repetition of the first two digits 5 times (E.g. 3434343434)
1. UIN should not contain three even adjacent digits (E.g. 3948613752)
1. UIN should not contain ADMIN defined restricted number.
