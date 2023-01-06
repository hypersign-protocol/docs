# update()


Updates the DID document on blockchain

**API Definition**

```js
update(params: {
    didDocument: object;
    privateKeyMultibase: string;
    verificationMethodId: string;
    versionId: string;
  }): Promise<object>;
```

**Usage**

```js
const result = await hypersignDID.update({
  didDocument,
  privateKeyMultibase,
  verificationMethodId,
  versionId, // VersionId when DID is registered on chain. See the didDocumentMetadata when DID resolves
});
```

**Outputs**

```js
{
  code: 0,
  height: 1432293,
  rawLog: '[{"events":[{"type":"message","attributes":[{"key":"action","value":"/hypersignprotocol.hidnode.ssi.MsgUpdateDID"}]}]}]',
  transactionHash: 'A2E2E8104EBECD36BBBD9D41823AB2EEBDEA463D83CEB9FA54AA4D4017012B2D',
  gasUsed: 103684,
  gasWanted: 120751
}
```
