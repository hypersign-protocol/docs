# Credential Issuance

Once all actors are onboard, the next step is Credential Issuance. In this step, a user requests the verifiable credential from an Identity Provider by providing his data. The user data can be anything from email, phone numbers to address, geolocation, IP, and so on. Take a look at one simple example, user-data in the figure alongside.

The IDP verifies this data and issues a cryptographically signed credential also called ‘Verifiable Credential’ \[VC]. The VC contains verified user data, some metadata such as issuance date, expiration date and a proof object which contains signature of the issuer along with the algorithm used to produce the signature.

![](<../../.gitbook/assets/image (3).png>)
