# generateKeys()

Generate a new key pair of type `Ed25519VerificationKey2020`

**API Definition**

```javascript
generateKeys(params: { seed?: string }): Promise<{ privateKeyMultibase: string; publicKeyMultibase: string }>;
```

**Usage**

```javascript
const kp = await hypersignDID.generateKeys();

// OR pass a seed / mnemonic to generated deterministic key pair
const seed = Bip39.decode("three image merge verb tenant tree modify million hotel decade hurt alien loop illegal day judge beyond anxiety term there improve mad gossip car")
const kp = await hypersignDID.generateKeys({seed});
```

**Outputs**

```javascript
{
  privateKeyMultibase: 'zrv5GBX5VGiyxUS6iWyRHDWVYSkKEGk8Qsmuj9GBJQK8KMFPVrReX1rBKHoFqgf2HGwYqVzH92pwnqbxhDAJNqsa668',
  publicKeyMultibase: 'z6MkhHLrnL288X2dXRBVQ9KUDRi8LLUb6sb7zo1oUUjEqTVN'
}
```

// TODO: It should also outputs algorithm
