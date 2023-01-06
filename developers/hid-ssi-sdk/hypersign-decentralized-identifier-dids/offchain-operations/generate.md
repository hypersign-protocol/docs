# generate()

Generates a new DID Document

**API Definition**

```javascript
generate(params: { publicKeyMultibase: string }): Promise<object>;
```

**Usage**

```javascript
const didDocument = await hypersignDID.generate({ publicKeyMultibase });
```

**Outputs**

```javascript
{
  '@context': [ 'https://www.w3.org/ns/did/v1' ],
  id: 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz',
  controller: [ 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz' ],
  alsoKnownAs: [ 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz' ],
  verificationMethod: [
    {
      id: 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz#key-1',
      type: 'Ed25519VerificationKey2020',
      controller: 'did:hid:testnet:z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz',
      publicKeyMultibase: 'z3q5pC5mgnyYAQvLniaMdNLA8WmCjgzLmJn6seCmDvEhz'
    }
  ],
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
}
```
