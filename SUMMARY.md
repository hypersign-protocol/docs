# Table of contents

* [💬 Welcome!](README.md)

## Hypersign KYC

* [Integrations](hypersign-kyc/integrations/README.md)
  * [Staging](hypersign-kyc/integrations/staging.md)
* [Concepts](hypersign-kyc/concepts/README.md)
  * [Facial Recognition](hypersign-kyc/concepts/facial-recognition.md)
  * [ID Verification (via OCR)](hypersign-kyc/concepts/id-verification-via-ocr.md)
  * [Reusable KYC](hypersign-kyc/concepts/reusable-kyc.md)
  * [Encrypted Data Vault](hypersign-kyc/concepts/encrypted-data-vault.md)
* [KYC Widget](hypersign-kyc/kyc-widget/README.md)
  * [Web](hypersign-kyc/kyc-widget/web.md)
* [Dashboard](hypersign-kyc/dashboard.md)

## Hypersign SSI

* [Introduction](hypersign-ssi/introduction.md)
* [🔗 API Reference](hypersign-ssi/api-doc/README.md)
  * [Authentication](hypersign-ssi/api-doc/authentication.md)
  * [DID](hypersign-ssi/api-doc/did.md)
  * [Schema](hypersign-ssi/api-doc/schema.md)
  * [Verifiable Credential](hypersign-ssi/api-doc/verifiable-credential.md)
  * [Verifiable Presentation](hypersign-ssi/api-doc/verifiable-presentation/README.md)
    * [Presentation Template](hypersign-ssi/api-doc/verifiable-presentation/presentation-template.md)
    * [Presentation](hypersign-ssi/api-doc/verifiable-presentation/presentation.md)
* [🎰 API Playground](hypersign-ssi/api-playground.md)
* [🏑 SSI Playground](hypersign-ssi/ssi-playground.md)

## Hypersign Developer Dashboard

* [Service](hypersign-developer-dashboard/developer-dashboard/README.md)
  * [Network Fee](hypersign-developer-dashboard/developer-dashboard/network-fee.md)
* [Teams & Access](hypersign-developer-dashboard/teams-and-access/README.md)
  * [Members](hypersign-developer-dashboard/teams-and-access/members.md)
  * [Teams](hypersign-developer-dashboard/teams-and-access/teams.md)
  * [Access List](hypersign-developer-dashboard/teams-and-access/access-list.md)
* [Security](hypersign-developer-dashboard/security/README.md)
  * [Multi factor Authentication (MFA)](hypersign-developer-dashboard/security/multi-factor-authentication-mfa.md)

## Hypersign Identity Network

* [Introduction](hypersign-identity-network/readme.md)
* [Validators & Delegators](hypersign-identity-network/validator/README.md)
  * [Installation of Node](hypersign-identity-network/validator/installation-of-node.md)
  * [Running a Testnet Validator Node](hypersign-identity-network/validator/running-a-testnet-validator-node.md)
* [Governance](hypersign-identity-network/governance/README.md)
  * [Proposals](hypersign-identity-network/governance/proposals/README.md)
    * [Blockchain Node Upgrade](hypersign-identity-network/governance/proposals/blockchain-node-upgrade.md)
    * [Community Pool Spend Proposal](hypersign-identity-network/governance/proposals/submitting-community-pool-spend-proposal.md)
    * [Blockchain Parameter Change Proposal](hypersign-identity-network/governance/proposals/submitting-blockchain-parameter-change-proposal.md)
    * [Text Proposal](hypersign-identity-network/governance/proposals/submitting-text-proposal.md)
  * [Delegation](hypersign-identity-network/governance/delegation.md)
* [Faucet (testnet)](hypersign-identity-network/faucet.md)
* [Developers](hypersign-identity-network/developers/README.md)
  * [HID-Node Codebase](hypersign-identity-network/developers/hid-node.md)
  * [⚙️ Setup Local hid-network Tutorial](hypersign-identity-network/developers/setting-up-local-hid-node-tutorial/README.md)
    * [Running one-node local hid network](hypersign-identity-network/developers/setting-up-local-hid-node-tutorial/running-a-localnet.md)
    * [Create and fund new account](hypersign-identity-network/developers/setting-up-local-hid-node-tutorial/create-and-fund-new-account.md)
    * [Transfer funds](hypersign-identity-network/developers/setting-up-local-hid-node-tutorial/transfer-funds.md)
    * [Connect Keplr to local hid network](hypersign-identity-network/developers/setting-up-local-hid-node-tutorial/connect-keplr-to-local-hid-network.md)
  * [Hypersign SSI Toolkit](hypersign-identity-network/developers/hid-ssi-sdk/README.md)
    * [Hypersign DID SDK](hypersign-identity-network/developers/hid-ssi-sdk/hypersign-decentralized-identifier-dids.md)
    * [Hypersign Schema SDK](hypersign-identity-network/developers/hid-ssi-sdk/hypersign-schema-sdk.md)
    * [Hypersign Verifiable Credential SDK](hypersign-identity-network/developers/hid-ssi-sdk/hypersign-verifiable-credential-sdk.md)
    * [Hypersign Verifiable Presentation SDK](hypersign-identity-network/developers/hid-ssi-sdk/hypersign-verifiable-presentation-sdk.md)
    * [OfflineSigner](hypersign-identity-network/developers/hid-ssi-sdk/offlinesigner.md)
* [Blockchain & ID Explorer](https://explorer.hypersign.id/hypersign-prajna-testnet)

## Core Concepts

* [Introduction](core-concepts/introduction.md)
* [Decentralized Identifier (DID)](core-concepts/decentralized-identifier-did/README.md)
  * [DID Registry](core-concepts/decentralized-identifier-did/did-registry.md)
  * [Private and Public DID](core-concepts/decentralized-identifier-did/private-and-public-did.md)
  * [DID Authentication](core-concepts/decentralized-identifier-did/did-authentication.md)
  * [DID Communication (DIDComm)](core-concepts/decentralized-identifier-did/did-communication-didcomm.md)
  * [Adding multiple controller to DID](core-concepts/decentralized-identifier-did/adding-multiple-controller-to-did.md)
  * [Adding multiple verification methods](core-concepts/decentralized-identifier-did/adding-multiple-verification-methods.md)
  * [Verification Method vs Recovery Signature](core-concepts/decentralized-identifier-did/verification-method-vs-recovery-signature.md)
  * [Blockchain Account Id](core-concepts/decentralized-identifier-did/blockchain-account-id.md)
  * [DID Threshold](core-concepts/decentralized-identifier-did/did-threshold.md)
  * [Verifiable Condition](core-concepts/decentralized-identifier-did/verifiable-condition.md)
  * [Verification Relationships](core-concepts/decentralized-identifier-did/verification-relationships/README.md)
    * [Authorization Capabilities (zCap)](core-concepts/decentralized-identifier-did/verification-relationships/authorization-capabilities-zcap.md)
* [Schema](core-concepts/schema/README.md)
  * [Schema Registry](core-concepts/schema/schema-registry.md)
  * [Schema.org](core-concepts/schema/schema.org.md)
* [Verifiable Credential (VC)](core-concepts/verifiable-credential-vc/README.md)
  * [Credential Revocation Registry](core-concepts/verifiable-credential-vc/credential-revocation-registry.md)
  * [Issuing a Credential to Multiple Subjects](core-concepts/verifiable-credential-vc/issuing-a-credential-to-multiple-subjects.md)
  * [Bearer Credential](core-concepts/verifiable-credential-vc/bearer-credential.md)
  * [Single-Use Credential](core-concepts/verifiable-credential-vc/single-use-credential.md)
* [Verifiable Presentation (VP)](core-concepts/verifiable-presentation-vp.md)
* [Specifications](core-concepts/specifications/README.md)
  * [Supported Signature Algorithms](core-concepts/specifications/supported-signature-algorithms.md)
  * [Client Specification](core-concepts/specifications/client-specification/README.md)
    * [EVM based chains](core-concepts/specifications/client-specification/evm-based-chains.md)
    * [Cosmos based chains](core-concepts/specifications/client-specification/cosmos-based-chains.md)

## Ecosystem

* [Forum](https://discord.gg/2hbU9Tsw)
* [Github](https://github.com/hypersign-protocol/)
* [HID Explorer](https://explorer.hypersign.id/hypersign-prajna-testnet)
* [Eiko](https://eiko.zone)
* [MetaAuth](https://metaauth.id)

***

* [Privacy Policy](privacy-policy.md)
