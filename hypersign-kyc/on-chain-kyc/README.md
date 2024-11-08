---
icon: hive
description: >-
  Verify user's Identity in a privacy preserving way and grant access to your
  dApps
---

# On-Chain KYC

### Introduction

The on-chain KYC feature enables you to verify users' identities in a privacy-preserving manner, granting access to your dApps without compromising sensitive information. For example, if you need to verify a user’s identity before allowing access to your smart contract, this can be done in three key steps:

#### On-chain KYC Configuration

1. dApps [deploy the on-chain KYC contracts](contracts-deployment.md) via the Entity Studio dashboard on their preferred (supported) blockchains.
2. dApps [activate the on-chain KYC settings and configure zero-knowledge (zk) proof ](../integrations/widget-configuration.md)options within the widget configuration.

#### Token Minting

1. Users generate the required zk proofs from their identity credentials.
2. Users mint Soulbound Tokens (SBTs) tied to their zk proofs.

#### Token Verification

1. The dApp’s smart contract queries and verifies the user's SBT directly on-chain, confirming identity before granting access.

This process provides decentralised, privacy-respecting identity verification for secure dApp access.

{% content-ref url="supported-blockchains.md" %}
[supported-blockchains.md](supported-blockchains.md)
{% endcontent-ref %}

### Architecture

The architecture of on-chain KYC contracts is straightforward, consisting primarily of three smart contracts and a set of libraries. Initially, the Hypersign Admin deploys the **Hypersign KYC Factory** contract on the blockchain. This KYC Factory contract manages a registry of issuers and maintains the contract addresses of their respective KYC Issuer contracts.

For any dApp that wishes to implement an on-chain KYC system, they simply call the **Hypersign KYC Factory** contract to initiate the deployment of their dedicated **Hypersign KYC Issuer** contract. The contract serves two primary purposes: (a) Deploying the **Hypersign KYC Token** contract, and (b) Verifying zero-knowledge (zk) proofs to mint the **Hypersign KYC Token** for users. Once a dApp deploys its own **Hypersign KYC Issuer** contract, it needs to call the **Hypersign KYC Token** contract to instantiate its respective KYC token contract. Users then mint their on-chain ID—a  Soulbound Token (SBT)—through the **Hypersign KYC Issuer** contract, establishing their verified identity on-chain.

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

Finally, The **Hypersign KYC Token** contract is responsible for managing all on-chain identities for users. dApps that need to confirm a user’s completion of the KYC process can call this contract to verify their status.

{% hint style="info" %}
As a dApp, you do not need to worry about Hypersign KYC Factory Contract. You only need to deploy the KYC Issuer and KYC Token contract through Entity Studio Dashboard in just few button clicks.&#x20;
{% endhint %}

Let's go ahead and deploy these two contract through Entity studio dashboard:&#x20;

{% content-ref url="contracts-deployment.md" %}
[contracts-deployment.md](contracts-deployment.md)
{% endcontent-ref %}



