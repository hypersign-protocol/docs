# Credential Revocation Registry

Storing Verifiable Credential on a distributed ledger could lead to privacy violation. However, we can store the status of a Verifiable Credential on-chain, with no private information attached to it. Issuers of a Verifiable Credential have the ability to revoke the credential and provide the reason behind it.

## Syntax of Verifiable Credential (VC) ID 

The syntax for Verifiable Credential ID is as follows:

```
vc:hid:<chain-namespace>:<method-specific-id>
```

- `vc:hid` - VC Method, where `vc` is the document identifier and `hid` is the method name
- `<chain-namespace>` - *(Optional)* Name of the blockchain where the VC status is registered. It is omitted for the document registered on mainnet chain
- `<method-specific-id>` - Multibase-encoded unique identifier of length 45

## VC Status Operations

- **Transaction Based**
  - Register/Update a VC Status Document
- **Query Based**
  - Query a VC Status Document
  - Query Registered VC Status Documents

## Supported VC Statuses

Following are the VC statuses supported by `hid-node`:

- **Live**
- **Suspended**
- **Revoked**
- **Expired**

**NOTE**: VC Statuses are **case sensetive**. `Live` is valid, while `live` is invalid

### Status Change Rules

- Unregistered VC Status Document should only have the status as `Live`
- `Suspended` status can be changed to `Revoked` and `Live`
- `Revoked` and `Expired` statuses cannot be changed

## Supported Hash Algorithm

Following are the supported hash algorithms for the attribute `credentialHash`:

- **SHA-256**

## Register/Update VC Status

Both registeration and update of VC Status happens through the RPC `RegisterCredentialStatus`.

**CLI Signature**

```
Usage:
  hid-noded tx ssi register-credential-status [credential-status] [proof]

Params:
 - credential-status : Credential Status Document
 - proof : Issuer's Signature Format
```

**`credential-status` Structure**

```json
{
    "claim": {
        "id": "vc:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
        "currentStatus": "Live",
        "statusReason": "Credential Active"
    },
    "issuer": "did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf",
    "issuanceDate": "2022-04-10T04:07:12Z",
    "expirationDate": "2023-02-22T13:45:55Z",
    "credentialHash": "< -- SHA-256 Hash of VC -->"
}
```

**`proof` Structure**

```json
{
    "type": "Ed25519VerificationKey2020",
    "created": "2022-04-10T04:07:12Z",
    "updated": "2022-04-10T04:07:12Z",
    "verificationMethod": "did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1",
    "proofValue": "<-- Base64 encoded signature -->",
    "proofPurpose": "assertion"
}
```

The field `proofValue` holds the signature that was produced by signing the `credential-status` document. 

**Example**

```sh
hid-noded tx ssi register-credential-status '{"claim":{"id":"vc:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4","currentStatus":"Live","statusReason":"Credential Active"},"issuer":"did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf","issuanceDate":"2022-04-10T04:07:12Z","expirationDate":"2023-02-22T13:45:55Z","credentialHash":"< -- SHA-256 Hash of VC -->"}' '{"type":"Ed25519VerificationKey2020","created":"2022-04-10T04:07:12Z","updated":"2022-04-10T04:07:12Z","verificationMethod":"did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1","proofValue":"<-- Base64 encoded signature -->","proofPurpose":"assertion"}' --from <hid-account>
```

## Query VC Status

**CLI Signature**

```
Usage:
  hid-noded q ssi credential-status [credential-id]
```

**Example**

```
hid-noded q ssi credential-status vc:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4
```

**REST**

1. Query credential status for an inpug credential id:

```
http://<REST-URL>/hypersign-protocol/hidnode/ssi/credential/{credId}
```

2. Query list of registered credential statuses:

```
http://<REST-URL>/hypersign-protocol/hidnode/ssi/credential
```