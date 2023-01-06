---
description: A Javascript  based SDK for DID Operations
---

# Hypersign DID SDK

Hypersign Decentralized Identifiers (Hypersign DID) comply [W3C DID specification](https://www.w3.org/TR/did-core/) and is built on top of [Hypersign Identity Blockchain Network](https://explorer.hypersign.id/hypersign-testnet). It implements [Hypersign DID scheme (`did:hid`)](https://docs.hypersign.id/self-sovereign-identity-ssi/decentralized-identifier-did).

Note: `did:hid` DID scheme is yet to be offcially registered on [W3C DID registry](https://www.w3.org/TR/did-spec-registries/).

## What is a DID?

As per [W3C DID v1.0 specification document](https://www.w3.org/TR/did-core/):

> Decentralized identifiers (DIDs) are a new type of identifier that enables verifiable, decentralized digital identity. A DID refers to any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) as determined by the controller of the DID.

In simple words, decentralised identifiers are cryptographically-verifiable identifiers which are stored on a decentralised ledger, which enables users to own and manage their digital identity.

## Hypersign DID SDK

Is a javascript library to interact with Hypersign DID and to perform onchain and offchain operations.

## Table of Contents

* [Install The Package](./#install-the-package)
* [Import The Package](./#import-the-package)
* [OffChain APIs](offchain-operations/)
  * [Initialize Instance of HypersignDID](./#initialize-instance-of-hypersigndid)
  * [generateKeys()](./#generatekeys)
  * [generate()](./#generate)
  * [sign()](./#sign)
  * [verify()](./#verify)
* [OnChain APIs](onchain-operations/)
  * [Initialize Instance of HypersignDID with offlineSigner](./#initialize-with-offlinesigner)
  * [register()](./#register)
  * [resolve()](./#resolve)
  * [update()](./#update)
  * [deactivate()](./#deactivate)



## Install The Package

```bash
npm i hid-ssi-sdk --save
```

## Import The Package

```js
import { HypersignDID } from 'hid-ssi-sdk';
```
