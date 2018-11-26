Multiple aspects of security like confidentiality, privacy, integrity of data are key in ensuring an Individual's identity is not compromised. Below are the security design principles MOSIP must follow

- Direct access to data stored in database is discouraged. Data can only be accessed via API's
- An Individual's Identity data at is always encrypted to ensure confidentiality of data
- Access controls must be implemented on all API's to ensure data privacy (who can see what)

### Data encryption

Database encryption


### Key management

### Authentication
In MOSIP Authentication largely falls into the below categories
- Authentication via web channel (for Pre-Registration web app, Admin web app and Resident services portal)
- Authentication via local system i.e., offline authentication (for Registration client)

### Authorization
In MOSIP Authorization falls into the below categories
- Authorization of API's accessed via web channel
- Authorization to access specific data (will be implemented in v2)
