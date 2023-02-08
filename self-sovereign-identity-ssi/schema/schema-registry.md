# Schema Registry

## Hypersign Schema Registry

The Hypersign Schema comply [Verifiable Credentials JSON Schema 2022 data model](https://w3c-ccg.github.io/vc-json-schemas/#data\_model) specification and is stored on [Hypersign Identity Blockchain Network](https://explorer.hypersign.id/hypersign-testnet) as it is [adviced to store](https://w3c-ccg.github.io/vc-json-schemas/#storage) schema documents and made available as immutable objects.

## Syntax of Hypersign Schema ID

The syntax of Schema ID is as follows:

```
sch:hid:<chain-namespace>:<method-specific-id>:<version-number>
```

* `sch:hid` - Schema Method, where `sch` is the document identifier and `hid` is the method name
* `<chain-namespace>` - _(Optional)_ Name of the blockchain where the schema document is registered. It is omitted for the document registered on mainnet chain
* `<method-specific-id>` - Alpha-numeric string of minimum 32 character length
* `<version-number>` - Model version of schema. For instance, `1.0`, `1.1` and `2.1`

## Schema Operations

* **Transaction Based**
  * Register/Update a Schema Document
* **Query Based**
  * Query Schema Document(s)

## Usage

### Register/Update Schema

Both registration and update of Schema happens through the RPC `CreateSchema`

**CLI Signature**

```
Usage:
  hid-noded tx ssi create-schema [schema-doc] [schema-proof] [flags]

Params:
 - schema-doc : Schema Document
 - schema-proof : Schema Proof
```

**Example**

```
hid-noded tx ssi create-schema '{"type":"https://w3c-ccg.github.io/vc-json-schemas/schema/1.0/schema.json","modelVersion":"v1.0","id":"sch:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf:1.0","name":"HS credential template","author":"did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf","authored":"2022-04-10T04:07:12Z","schema":{"schema":"https://json-schema.org/draft-07/schema#","description":"test","type":"object","properties":"{myString:{type:string},myNumner:{type:number},myBool:{type:boolean}}","required":["myString","myNumner","myBool"],"additionalProperties":false}}' '{"type":"Ed25519VerificationKey2020","created":"2022-04-10T04:07:12Z","verificationMethod":"did:hid:devnet:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1","proofValue":"gLFhwYfObNJEOjNDaeYjprv7FpK0lIhZnFwgOsdRqRHOjQswfm3Hk9EehcYGePrFFwgy4lna73iA5J0BtjfCAw==","proofPurpose":"assertionMethod"}' --from <key-name-or-address> --chain-id <Chain ID> --yes
```

### Register/Update Schema

**CLI Signature**

```
Usage:
  hid-noded query ssi schema [schema-id]

Params:
 - schema-id : Schema ID
```

**Example**

```
hid-noded query ssi schema sch:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf:1.0
```

**REST**

1. Query a specific version of schema document for given schema id:

```
http://<REST-URL>/hypersign-protocol/hidnode/ssi/schema/sch:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf:1.0
```

1. Query all versions of a schema document:

```
http://<REST-URL>/hypersign-protocol/hidnode/ssi/schema/sch:hid:<chain-namespace>:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf
```

1. Query a list of registered schema documents:

```
http://<REST-URL>/hypersign-protocol/hidnode/ssi/schema
```
