# deactivate()


Deactivates the DID document on blockchain

**API Definition**

```js
deactivate(params: {
    didDocument: object;
    privateKeyMultibase: string;
    verificationMethodId: string;
    versionId: string;
  }): Promise<object>;
```
**Usage**

```js
const result = await hypersignDID.deactivate({
      didDocument,
      privateKeyMultibase,
      verificationMethodId,
      versionId,  // VersionId when DID is registered on chain. See the didDocumentMetadata when DID resolves
});
```

**Outputs**
```js
{
  code: 0,
  height: 1432295,
  rawLog: '[{"events":[{"type":"message","attributes":[{"key":"action","value":"/hypersignprotocol.hidnode.ssi.MsgDeactivateDID"}]}]}]',
  transactionHash: 'E648A4E85B943C668E2BA24530B3C9D3364BBEA05E49F6F75A57CAC2EE72264C',
  gasUsed: 92728,
  gasWanted: 106555
}
```
