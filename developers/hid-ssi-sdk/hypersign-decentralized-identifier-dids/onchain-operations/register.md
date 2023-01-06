# register()

Registers a DID and DIDDocument on blockchain

**API Definition**

```javascript
register(params: { 
  didDocument: object; 
  privateKeyMultibase: string; 
  verificationMethodId: string
}): Promise<object>;
```

**Usage**

```javascript
const result = await hypersignDID.register({ 
  didDocument, 
  privateKeyMultibase, 
  verificationMethodId
});
```

**Outputs**

```javascript
{
  code: 0,
  height: 1432291,
  rawLog: '[{"events":[{"type":"message","attributes":[{"key":"action","value":"/hypersignprotocol.hidnode.ssi.MsgCreateDID"}]}]}]',
  transactionHash: 'E4B985104BC233E4EC4A7F9A6B501812B92D059677D6543C024E6B7936BC5BC3',
  gasUsed: 99152,
  gasWanted: 114906
}
```
