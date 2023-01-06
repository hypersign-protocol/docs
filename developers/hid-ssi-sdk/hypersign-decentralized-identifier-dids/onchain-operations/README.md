# Onchain Operations


### Initialize with offlineSigner 

**Create Instance of the class**
```js
const hypersignDid = new HypersignDID({
    offlineSigner,                    // OPTIONAL signer of type OfflineSigner
    nodeRestEndpoint: hidNodeEp.rest, // OPTIONAL RPC endpoint of the Hypersign blockchain, Default 'TEST'
    nodeRpcEndpoint: hidNodeEp.rpc,   // OPTIONAL REST endpoint of the Hypersign blockchain
    namespace: hidNodeEp.namespace,   // OPTIONAL namespace of did id, Default 'did:hid'
  });

// OR Just initalize with offlineSigner
const hypersignDid = new HypersignDID({
    offlineSigner
})
```
**Call `init()` to initalize the offlineSigner**

```js
await hypersignDid.init();
```
