# OffChain Operations

### Initialize Instance of HypersignDID

```javascript
const hypersignDID = new HypersignDID();

// OR initialize by passing a namepace. Default 'did:hid'
// More complex way to initialize this class can be found in this documentation later
const namespace = 'did:hid';
const hypersignDID = new HypersignDID({ namespace });
```
