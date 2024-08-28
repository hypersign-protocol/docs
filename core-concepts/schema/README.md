---
icon: database
---

# Schema

## What is Verifiable Credential Schema or Data Models?

As per the [Verifiable Credentials JSON Schema 2022](https://w3c-ccg.github.io/vc-json-schemas/#verifiable\_credentials\_data\_model) specification:

> The Credential Schema is a document that is used to guarantee the structure, and by extension the semantics, of the set of claims comprising a [Verifiable Credential](../../hypersign-identity-network/developers/hid-ssi-sdk/hypersign-schema-sdk.md). A shared Credential Schema allows all parties to reference data in a _"known way"_.

A schema can be viewed from four perspectives: the author, issuer, verifier and holder.

* **Author**: An author creates a schema and registers it in Hypersign blockchain as to provide a blueprint for a _Verifiable Credential_, specifying the shape and format of the data in such a credential.
* **Issuer**: Issuers utilize schemas to provide structure and meaning to the data they issue as _Verifiable Credentials_. By using schemas, issuers contribute to a credentialing ecosystem that promotes the usage and adoption of data standards.
* **Verifier**: Verifiers processes a _Verifiable Credentials_ and need to do so with knowledge of the terms and data the compromise the credentials. Credential Schemas aid a verifier in both requesting and processing credenetials that have been produced in a well-known format.
* **Holder**: Holders, or those who are the subject of credential issuance, can make sense of the data they control by evaluating it against a data schema. When data is requested from a holder which references a Credential Schema the holder has the capability to to present the data specifically requested by the verifier.

Note: Often, Issuer and Author of schema may be same.
