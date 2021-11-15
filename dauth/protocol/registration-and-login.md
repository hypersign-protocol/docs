# Registration & Login

Once actors are on board and verifiable credentials are issued, a user is now ready to authenticate himself and avail service from the service provider.

The service provider requests from the user the minimum data it needs to let them access the application. This request can be made via several different protocols, called ‘DIDComm’, depending on the requirement. For simplicity, we use QRCode based communication. In the QR, the SP provides its DID, a challenge, a callback API, supported credential type and data model.

A user chooses the required credential from the available list of credentials which he might have collected from different identity providers and selects the information needed for the provider. Users also have the ability to share partial data with SP. This helps to reduce excess data leakage. Before presenting the verifiable credential to the SP, the end user also signs the credential. Take a look at the co-signed credential document in the figure below.

Upon receiving the co-signed credential, the provider parses the credential document and fetches public keys of issuers and owners using their DIDs mentioned in the document from the Hypersign Blockchain Network. Finally, it verifies signatures and upon successful verification it generates an authorization token based on user data available in the credential document and gives access to the end user. Take a look at the detail flow in the figure below.

![](<../../.gitbook/assets/image (2).png>)
