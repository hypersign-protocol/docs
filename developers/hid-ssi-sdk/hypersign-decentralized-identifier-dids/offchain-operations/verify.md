# verify()


Verifies a signed DID Document.

**API Definition**

```js
verify(params: { 
  didDocument: object;            // Signed did documen
  verificationMethodId: string;   // The verification method
  challenge: string;              // Random challenge
  domain?: string                 // The domain name
}): Promise<object>;
```
**Usage**

```js
const result = await hypersignDID.verify({
      didDocument: signedDocument, 
      verificationMethodId, 
      challenge: '1231231231', 
      domain: 'www.hypersign.id',   
});
```

**Outputs**

```json
{
    "verified": true,
    "results": [
      {
        "proof": {
          "@context": [
            "https://www.w3.org/ns/did/v1",
            "https://w3id.org/security/suites/ed25519-2020/v1"
          ],
          "type": "Ed25519Signature2020",
          "created": "2023-01-06T03:43:39Z",
          "verificationMethod": "did:hid:testnet:zFDepBTjyjKFVmDnSxfLvfnJ97PpjdpDW2yXA8sPzuoTr#key-1",
          "proofPurpose": "authentication",
          "challenge": "1231231231",
          "domain": "www.adbv.com",
          "proofValue": "z5vqfue3RppWtSrPibxM2VUbeocUxHCqeENFx8QteyGhN1j7xXm6WuxutTeuQUgZByZbMkveVQCFjeE9Yxoo4S1d8"
        },
        "verified": true,
        "verificationMethod": {
          "id": "did:hid:testnet:zFDepBTjyjKFVmDnSxfLvfnJ97PpjdpDW2yXA8sPzuoTr#key-1",
          "type": "Ed25519VerificationKey2020",
          "publicKeyMultibase": "z6MktfurmhzR4rjxsid9eEJmWsr8vy6b3hTrizS5y9N1q2FE"
        },
        "purposeResult": {
          "valid": true,
          "controller": {
            "@context": "https://w3id.org/security/v2",
            "id": "did:hid:testnet:zFDepBTjyjKFVmDnSxfLvfnJ97PpjdpDW2yXA8sPzuoTr#key-1",
            "authentication": [
              "did:hid:testnet:zFDepBTjyjKFVmDnSxfLvfnJ97PpjdpDW2yXA8sPzuoTr#key-1"
            ]
          }
        }
      }
    ]
  }
```
