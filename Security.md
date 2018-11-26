Multiple aspects of security like confidentiality, privacy, integrity of data are key in ensuring an Individual's identity is not compromised. Below are the security design principles MOSIP must follow

- Direct access to data stored in database is discouraged. Data can only be accessed via API's
- An Individual's Identity data at is always encrypted to ensure confidentiality of data
- Access controls must be implemented on all API's to ensure data privacy (who can see what)

### Database encryption
As a principle, MOSIP will not use any mechanism in-built in a database for encryption. All sensitive data to be stored in a DB is encrypted/decrypted outside the DB.

- All data will be encrypted using a symmetric key algorithm. MOSIP will support AES 256 algorithm by default
- Each record will be encrypted using its own symmetric key and same key will not be used to encrypt multiple records
- The symmetric key itself is encrypted using a master public key. The corresponding private must be managed in a HSM
- HSM will store an asymmetric key pair for each application/service and will be rotated periodically as per configuration
- The encrypted symmetric key is appended to the data itself and not stored separately

![Db encryption/decryption flow](_images/arch_diagrams/DB_encryption.png)

### Key management

### Authentication
In MOSIP Authentication largely falls into the below categories
- Authentication via web channel (for Pre-Registration web app, Admin web app and Resident services portal)
- Authentication via local system i.e., offline authentication (for Registration client)

### Authorization
In MOSIP Authorization falls into the below categories
- Authorization of API's accessed via web channel
- Authorization to access specific data (will be implemented in v2)
