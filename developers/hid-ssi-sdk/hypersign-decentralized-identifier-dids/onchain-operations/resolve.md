# resolve()

Resolves a DID document from blockchain provided the DID.

**API Definition**

```javascript
resolve(params: { 
  did: string; 
  ed25519verificationkey2020?: boolean 
}): Promise<object>;
```

**Usage**

```javascript
const result = await hypersignDID.resolve({
      did,
});
```

**Outputs**

```javascript
{
  didDocument: {
    '@context': [ 'https://www.w3.org/ns/did/v1' ],
    id: 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz',
    controller: [ 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz' ],
    alsoKnownAs: [ 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz' ],
    verificationMethod: [ {
        id: "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55#key-1",
        type: "Ed25519VerificationKey2020",
        controller: "did:hid:testnet:z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55",
        publicKeyMultibase: "z2rkgwQaXwDAXtKFkbNE74fanZGVsDTCcNzWFjwPidB55"
      } ],
    authentication: [
      'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1'
    ],
    assertionMethod: [
      'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1'
    ],
    keyAgreement: [
      'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1'
    ],
    capabilityInvocation: [
      'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1'
    ],
    capabilityDelegation: [
      'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1'
    ],
    service: []
  },
  didDocumentMetadata: {
    created: '2023-01-06T03:27:13Z',
    updated: '2023-01-06T03:27:13Z',
    deactivated: false,
    versionId: 'E4B985104BC233E4EC4A7F9A6B501812B92D059677D6543C024E6B7936BC5BC3'
  }
}
```
