# sign()

Sign a DID Document and generated proof 

**API Definition**

```js
sign(params: {
    didDocument: object;            // A DID Document to signed
    privateKeyMultibase: string;    // private key mulibase of type ED25519
    challenge: string;              // Random challenge
    domain: string;                 // Domain name
    did: string;                    // DID, if passed then DID will be resolved and `didDocument` parameter will not be used
    verificationMethodId: string    // Verification method identifier
  }): Promise<ISignedDIDDocument>;
```

**Usage**

```js
const params = {
      privateKey: privateKeyMultibase, 
      challenge: '1231231231', 
      domain: 'www.hypersign.id', 
      did: '', 
      didDocument: didDocument, 
      verificationMethodId: verificationMethodId, 
    };

const signedDocument = await hypersignDID.sign(params);
```

**Outputs**
```json
{
    "@context": [
      "https://www.w3.org/ns/did/v1",
      "https://w3id.org/security/suites/ed25519-2020/v1"
    ],
    "id": "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55",
    "controller": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55"
    ],
    "alsoKnownAs": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55"
    ],
    "verificationMethod": [
      {
        "id": "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1",
        "type": "Ed25519VerificationKey2020",
        "controller": "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55",
        "publicKeyMultibase": "z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55"
      }
    ],
    "authentication": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1"
    ],
    "assertionMethod": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1"
    ],
    "keyAgreement": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1"
    ],
    "capabilityInvocation": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1"
    ],
    "capabilityDelegation": [
      "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1"
    ],
    "service": [],
    "proof": {
      "type": "Ed25519Signature2020",
      "created": "2023-01-06T03:47:00Z",
      "verificationMethod": "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1",
      "proofPurpose": "authentication",
      "challenge": "1231231231",
      "domain": "www.hypersign.id",
      "proofValue": "z5aX3uHmzhX2kvx5kiSgs8d2RHfEh7akMUvU35wVKqpm9vqsbptSCL7Ak6rLE9DX3DC98buzruvQ6RJgmeC73gHxP"
    }
}
```
