# Decentralized Identifier (DID)

Decentralised Identifiers are cryptographically-verifiable identifiers which are stored on a decentralised ledger, which enables users to own and manage their ID.

## Syntax of `did:hid` method

The `did:hid` method are as follows:

```
did                = "did:" method-name ":" [chain-namespace] ":" method-specific-id
method-name        = "hid"
chain-namespace    = ALPHA / DIGIT
method-specific-id = 45 * id-char
id-char            = ALPHA / DIGIT
```

**Description of ID segments**

- `did` - Document Identifier of DID Document
- `hid` - Method name
- `<chain-namespace>` - *(Optional)* Name of the blockchain where the VC status is registered. It is omitted for the document registered on mainnet chain
- `<method-specific-id>` - Multibase-encoded unique identifier of length 45

## Supported DID Method Operations

The `did:hid` method supports the following operations:

- **Transaction Based**:
  - Register a DID document
  - Update a DID document
  - Deactivate a DID document
- **Query Based**:
  - Query a DID Document
  - Query registered DID Documents

## Usage

### Register DID

**CLI Signature**

```
Usage:
  hid-noded tx ssi create-did [did-doc-string] [verification-method-id] [flags]

Params:
 - did-doc-string : Did Document String
 - verification-method-id : Id of verification Method Key

Flags:
 - ver-key : Private Key of the Signer
```

**Example**

```sh
hid-noded tx ssi create-did '{
"context": [
"https://www.w3.org/ns/did/v1",`
"https://w3id.org/security/v1",
"https://schema.org"
],
"id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
"controller": ["did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"],
"alsoKnownAs": ["did:hid:<chain-namespace>:1f49341a-de30993e6c52"],
"verificationMethod": [
{
"id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1",
"type": "Ed25519VerificationKey2020",
"controller": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
"publicKeyMultibase": "z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
}
],
"service": [{
"id":"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#vcs",
"type": "LinkedDomains",
"serviceEndpoint": "http://example.onion"
},
{
"id":"did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#file",
"type": "LinkedDomains",
"serviceEndpoint": "http://service.onion"
}
],
"authentication": [
"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1"
],
"assertionMethod": [
"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1"
]
}' did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1 --ver-key <base64-encoded-private-key> --from <key-name-or-address> --chain-id <Chain ID> --yes
```

### Query DID

**CLI Signature**

```
Usage:
  hid-noded q ssi did [didDoc-id] [flags]

Params:
 - didDoc-id : Did Document Id
```

**Example**

```
hid-noded q ssi did did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4
```

**REST**

1) Get the list of registered DID Documents

URL: `http://<REST-URL>/hypersign-protocol/hidnode/ssi/did`

Output:

```json
{
   "totalDidCount":"2",
   "didDocList":[
      {
         "didDocument":{
            "context":[
               "https://www.w3.org/ns/did/v1"
            ],
            "id":"did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf",
            "controller":[
               "did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"
            ],
            "alsoKnownAs":[
               "did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"
            ],
            "verificationMethod":[
               {
                  "id":"did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1",
                  "type":"Ed25519VerificationKey2020",
                  "controller":"did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf",
                  "publicKeyMultibase":"zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"
               }
            ],
            "authentication":[
               "did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1"
            ],
            "assertionMethod":[
               "did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1"
            ],
            "keyAgreement":[
               
            ],
            "capabilityInvocation":[
               
            ],
            "capabilityDelegation":[
               
            ],
            "service":[
               
            ]
         },
         "didDocumentMetadata":{
            "created":"2022-02-25T09:20:15Z",
            "updated":"2022-02-25T09:20:15Z",
            "deactivated":false,
            "versionId":"BC2B9B37AF99BC7BC5599124B2F2168066B1B2DDE8F8C06FD720B3DDF2803285"
         }
      },
      {
         "didDocument":{
            "context":[
               "https://www.w3.org/ns/did/v1"
            ],
            "id":"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
            "controller":[
               "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
            ],
            "alsoKnownAs":[
               "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
            ],
            "verificationMethod":[
               {
                  "id":"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1",
                  "type":"Ed25519VerificationKey2020",
                  "controller":"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
                  "publicKeyMultibase":"z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
               }
            ],
            "authentication":[
               "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1"
            ],
            "assertionMethod":[
               
            ],
            "keyAgreement":[
               
            ],
            "capabilityInvocation":[
               
            ],
            "capabilityDelegation":[
               
            ],
            "service":[
               {
                  "id":"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#vcs",
                  "type":"LinkedDomains",
                  "serviceEndpoint":"https://example.com/vc"
               },
               {
                  "id":"did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#file",
                  "type":"LinkedDomains",
                  "serviceEndpoint":"https://example.in/somefile"
               }
            ]
         },
         "didDocumentMetadata":{
            "created":"2022-02-25T09:20:11Z",
            "updated":"2022-02-25T09:20:11Z",
            "deactivated":false,
            "versionId":"72093DE93BE67801C160C7CA12DC844D63D9FB3922F3ECC94BBB27844DE568D1"
         }
      }
   ]
}
```

2) Query the DID Document for an input DID id

URL: `http://<REST-URL>/hypersign-protocol/hidnode/ssi/did/did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4`

Output: 

```json
{
  "didDocument": {
    "context": [
      "https://www.w3.org/ns/did/v1"
    ],
    "id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
    "controller": [
      "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
    ],
    "alsoKnownAs": [
      "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
    ],
    "verificationMethod": [
      {
        "id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1",
        "type": "Ed25519VerificationKey2020",
        "controller": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
        "publicKeyMultibase": "z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
      }
    ],
    "authentication": [
      "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1"
    ],
    "assertionMethod": [],
    "keyAgreement": [],
    "capabilityInvocation": [],
    "capabilityDelegation": [],
    "service": [
      {
        "id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#vcs",
        "type": "LinkedDomains",
        "serviceEndpoint": "https://example.com/vc"
      },
      {
        "id": "did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#file",
        "type": "LinkedDomains",
        "serviceEndpoint": "https://example.in/somefile"
      }
    ]
  },
  "didDocumentMetadata": {
    "created": "2022-02-25T09:20:11Z",
    "updated": "2022-02-25T09:20:11Z",
    "deactivated": false,
    "versionId": "72093DE93BE67801C160C7CA12DC844D63D9FB3922F3ECC94BBB27844DE568D1"
  }
}
```

### Update DID

**CLI Signature**

```
Usage:
  hid-noded tx ssi update-did [did-doc-string] [version-id] [verification-method-id] [flags]

Params:
 - did-doc-string : Did Document string
 - version-id : Version ID of the DID Document to be updated. It is expected that version Id should match latest DID Document's version Id
 - verification-method-id : Id of verification Method Key

Flags:
 - --ver-key : Private Key of the Signer
```

**Example**

```sh
hid-noded tx ssi update-did '{
"context": [
"https://www.w3.org/ns/did/v1",
"https://w3id.org/security/v1",
"https://schema.org"
],
"id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
"controller": ["did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4","did:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"],
"alsoKnownAs": ["did:hid:<chain-namespace>:1f49341a-de30993e6c52"],
"verificationMethod": [
{
"id": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1",
"type": "Ed25519VerificationKey2020",
"controller": "did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4",
"publicKeyMultibase": "z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4"
}
],
"authentication": [
"did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1"
]
}' <version-id> did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1 --ver-key <private-key> --from <key-name-or-address> --chain-id <Chain ID> --yes
```

### Deactivate DID

**CLI Signature**

```
Usage:
  hid-noded tx ssi deactivate-did [did-id] [version-id] [verification-method-id] [flags]

Params:
 - did-id : DID Document ID
 - version-id : Version ID of the DID Document to be deactivated. It is expected that version Id should match latest DID Document's version Id
 - verification-method-id : Id of verification Method Key

Flags:
 - --ver-key : Private Key of the Signer
```

**Example**

```sh
hid-noded tx ssi deactivate-did 'did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4' <version-id> did:hid:<chain-namespace>:z8BXg2zjwBRTrjPs7uCnkFBKrL9bPD14HxEJMENxm3CJ4#key-1 --ver-key <private-key> --from <key-name-or-address> --chain-id <Chain Id> --yes
```
