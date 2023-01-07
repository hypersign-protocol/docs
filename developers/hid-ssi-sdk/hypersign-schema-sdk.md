---
description: A Javascript  based SDK for Schema Operations
---

# Hypersign Schema SDK

The Hypersign Schema comply [Verifiable Credentials JSON Schema 2022 data model](https://w3c-ccg.github.io/vc-json-schemas/#data\_model) specification and is stored on [Hypersign Identity Blockchain Network](https://explorer.hypersign.id/hypersign-testnet) as it is [adviced to store](https://w3c-ccg.github.io/vc-json-schemas/#storage) schema documents and made available as immutable objects.

## What is Verifiable Credential Schema or Data Models?

As per the [Verifiable Credentials JSON Schema 2022](https://w3c-ccg.github.io/vc-json-schemas/#verifiable\_credentials\_data\_model) specification:

> The Credential Schema is a document that is used to guarantee the structure, and by extension the semantics, of the set of claims comprising a [Verifiable Credential](hypersign-schema-sdk.md). A shared Credential Schema allows all parties to reference data in a _"known way"_.

A schema can be viewed from four perspectives: the author, issuer, verifier and holder.

* **Author**: An author creates a schema and registers it in Hypersign blockchain as to provide a blueprint for a _Verifiable Credential_, specifying the shape and format of the data in such a credential.
* **Issuer**: Issuers utilize schemas to provide structure and meaning to the data they issue as _Verifiable Credentials_. By using schemas, issuers contribute to a credentialing ecosystem that promotes the usage and adoption of data standards.
* **Verifier**: Verifiers processes a _Verifiable Credentials_ and need to do so with knowledge of the terms and data the compromise the credentials. Credential Schemas aid a verifier in both requesting and processing credenetials that have been produced in a well-known format.
* **Holder**: Holders, or those who are the subject of credential issuance, can make sense of the data they control by evaluating it against a data schema. When data is requested from a holder which references a Credential Schema the holder has the capability to to present the data specifically requested by the verifier.

Note: Often, Issuer and Autor of schema may be same.

## HypersignSchema SDK

Is a javascript library to interact with Hypersign Blockchain and to perform onchain and offchain schema operations.

**NOTES**

* A DID registred on Hypersign blockchain in order to register a schema on Hypersign blockchain network.
* Schema can not be registred using private DIDs.

## Table of Contents

* [Install The Package](hypersign-schema-sdk.md#install-the-package)
* [Import The Package](hypersign-schema-sdk.md#import-the-package)
* [OffChain APIs](hypersign-schema-sdk.md#offchain-apis)
  * [Initialize Instance of HypersignSchema](hypersign-schema-sdk.md#initialize-instance-of-hypersignschema)
  * [generate()](hypersign-schema-sdk.md#generate)
  * [sign()](hypersign-schema-sdk.md#sign)
* [OnChain APIs](hypersign-schema-sdk.md#onchain-apis)
  * [Initialize Instance of HypersignSchema with offlineSigner](hypersign-schema-sdk.md#initialize-with-offlinesigner)
  * [register()](hypersign-schema-sdk.md#register)
  * [resolve()](hypersign-schema-sdk.md#resolve)
* [Security Concerns](hypersign-schema-sdk.md#security)

## Install The Package

```bash
npm i hid-ssi-sdk --save
```

## Import The Package

```javascript
import { HypersignSchema } from 'hid-ssi-sdk';
```

## Offchain APIs

### Initialize Instance of HypersignSchema

```javascript
const hypersignSchema = new HypersignSchema();

// OR initialize by passing a namepace. Default ''
// More complex way to initialize this class can be found in this documentation later
const namespace = 'testnet';
const hypersignSchema = new HypersignSchema({ namespace });
```

### `generate()`

Generates a new schema doc without proof

**API Definition**

```javascript
generate(params: {
    name: string;
    description?: string;
    author: string;
    fields?: Array<ISchemaFields>;
    additionalProperties: boolean;
  }): Promise<SchemaDocument>;
```

`ISchemaFields`

```javascript
interface ISchemaFields {
  type: string;
  format?: string;
  name: string;
  isRequired: boolean;
}
```

**Usage**

```javascript

const schemaBody = {
  name: 'testSchema',
  description: 'This is a test schema generation',
  author: 'did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R',
  fields: [{ name: 'name', type: 'integer', isRequired: false }],
  additionalProperties: false,
}
const schema = await hypersignSchema.generate(schemaBody);
```

**Output**

```json
{
  "type": "https://w3c-ccg.github.io/vc-json-schemas/v1/schema/1.0/schema.json",
  "modelVersion": "1.0",
  "id": "sch:hid:testnet:z57BBNTNqkFXpsFfSMLvfvBhhiSEicGK3nVvJMXRKcE3S:1.0",
  "name": "testSchema",
  "author": "did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R",
  "authored": "2023-01-07T07:24:06Z",
  "schema": {
    "schema": "http://json-schema.org/draft-07/schema",
    "description": "This is a test schema generation",
    "type": "object",
    "properties": "{\"name\":{\"type\":\"integer\"}}",
    "required": [],
    "additionalProperties": false
  }
}

```

### `sign()`

Signs a schema document and attaches proof

**API Definition**

```javascript
sign(params: { privateKeyMultibase: string; schema: SchemaDocument, verificationMethodId: string }): Promise<Schema>;
```

Note: The difference between `SchemaDocument` and `Schema` types is, `Schema` type is `SchemaDocument` with `proof` attached to it. see the example below.

**Usage**

```javascript

const signedSchema = await hypersignSchema.sign({ privateKeyMultibase: privateKeyMultibase, schema: schema, verificationMethodId: 'did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R#key-1' });
```

**Output**

```json
{
  "type": "https://w3c-ccg.github.io/vc-json-schemas/v1/schema/1.0/schema.json",
  "modelVersion": "1.0",
  "id": "sch:hid:testnet:z57BBNTNqkFXpsFfSMLvfvBhhiSEicGK3nVvJMXRKcE3S:1.0",
  "name": "testSchema",
  "author": "did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R",
  "authored": "2023-01-07T07:24:06Z",
  "schema": {
    "schema": "http://json-schema.org/draft-07/schema",
    "description": "This is a test schema generation",
    "type": "object",
    "properties": "{\"name\":{\"type\":\"integer\"}}",
    "required": [],
    "additionalProperties": false
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2023-01-07T07:24:07Z",
    "verificationMethod": "did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R#key-1",
    "proofPurpose": "assertion",
    "proofValue": "aozlK3ZSAHuP2x7is60jYXdhS8zc68bO2y9CVShgLNaXxTHdeLIIgqY5Ci6ji0nrC5Q4e+YiGtV/SNIFkvO4CQ=="
  }
}
```

## OnChain APIs

### Initialize with offlineSigner

**Create Instance of the class**

```javascript
const hypersignSchema = new HypersignSchema({
    offlineSigner,                    // OPTIONAL signer of type OfflineSigner
    nodeRestEndpoint: hidNodeEp.rest, // OPTIONAL RPC endpoint of the Hypersign blockchain, Default 'TEST'
    nodeRpcEndpoint: hidNodeEp.rpc,   // OPTIONAL REST endpoint of the Hypersign blockchain
    namespace: hidNodeEp.namespace,   // OPTIONAL namespace of did id, Default 'did:hid'
  });

// OR Just initalize with offlineSigner
const hypersignSchema = new HypersignSchema({
    offlineSigner
})
```

**Call `init()` to initalize the offlineSigner**

```javascript
await hypersignSchema.init();
```

### `register()`

Register a schema Document in Hypersign blockchain

**API Definition**

```javascript
register(params: { schema: Schema }): Promise<object>;
```

**Usage**

```javascript
const registeredSchema = await hypersignSchema.register({
      schema: signedSchema
});
```

**Output**

```json
{
  "code": 0,
  "height": 1449829,
  "rawLog": "[{\"events\":[{\"type\":\"message\",\"attributes\":[{\"key\":\"action\",\"value\":\"/hypersignprotocol.hidnode.ssi.MsgCreateSchema\"}]}]}]",
  "transactionHash": "A4909951861464DA4FF0E8CB101E128895E166891AF68909B7622B212CCEEDE2",
  "gasUsed": 90160,
  "gasWanted": 103216
}
```

### `resolve()`

Resolves a schema document with schemId from Hypersign blockchain

**API Definition**

```javascript
resolve(params: { schemaId: string }): Promise<Schema>;

```

**Usage**

```javascript
const result = await hypersignSchema.resolve({ schemaId: schema['id']});

```

**Output**

```json
{
  "type": "https://w3c-ccg.github.io/vc-json-schemas/v1/schema/1.0/schema.json",
  "modelVersion": "1.0",
  "id": "sch:hid:testnet:z57BBNTNqkFXpsFfSMLvfvBhhiSEicGK3nVvJMXRKcE3S:1.0",
  "name": "testSchema",
  "author": "did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R",
  "authored": "2023-01-07T07:24:06Z",
  "schema": {
    "schema": "http://json-schema.org/draft-07/schema",
    "description": "This is a test schema generation",
    "type": "object",
    "properties": "{\"name\":{\"type\":\"integer\"}}",
    "required": [],
    "additionalProperties": false
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2023-01-07T07:24:07Z",
    "verificationMethod": "did:hid:testnet:zAtZ8oBrVPvaKKou21KRnmzRtZaJpWxsgWuB9GNRLTQ6R#key-1",
    "proofPurpose": "assertion",
    "proofValue": "aozlK3ZSAHuP2x7is60jYXdhS8zc68bO2y9CVShgLNaXxTHdeLIIgqY5Ci6ji0nrC5Q4e+YiGtV/SNIFkvO4CQ=="
  }
}
```

## Security Concerns

// TODO
