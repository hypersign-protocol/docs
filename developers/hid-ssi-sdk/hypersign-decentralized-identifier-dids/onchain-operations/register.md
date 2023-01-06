# register()


Registers a DID and DIDDocument on blockchain

**API Definition**

```js
register(params: { 
  didDocument: object; 
  privateKeyMultibase: string; 
  verificationMethodId: string
}): Promise<object>;
```
**Usage**

```js
const result = await hypersignDID.register({ 
  didDocument, 
  privateKeyMultibase, 
  verificationMethodId
});
```
