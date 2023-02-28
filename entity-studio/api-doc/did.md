---
description: Manage DID operation using DID APIs
---

# DID

Please [generate access token](authentication.md) before proceeding.  Once you generated the `access_token`, you can pass this token as _<mark style="background-color:yellow;">bearer authorization token</mark>_ in the header for all APIs.&#x20;

{% hint style="info" %}
**Note:** Some of these APIs are on-chain APIs which means they need network fee to successfully execute, so make sure that your application wallet address has $hid tokens. Read [network fee](../developer-dashboard/network-fee.md) section for more details.
{% endhint %}

{% hint style="info" %}
Entity Studio SSI API base URL: [https://api.entity.hypersign.id](https://api.entity.hypersign.id)
{% endhint %}

There are 3 steps involved in DID creation:&#x20;

* **Generate a DID Document**: Generate the data structure of the DID document.
* **Sign a DID Document (optional)**: Sign the DID Document using verification method.&#x20;
* **Register a DID Document (optional)** : Registers the signed DID Document on the blockchain network.&#x20;

{% hint style="info" %}
**Note**: You can choose not to register a DID on blockchain, in that case, the DID is concidered as private DID. We support `Ed25519VerificationKey2020` for private DIDs. Kindly read difference between [private and public DID](../../concepts/decentralized-identifier-did/private-and-public-did.md) in this section.&#x20;
{% endhint %}

### Create a DID

Generates the a new DID  and DID Document.&#x20;

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/did/create" method="post" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

### Request Body Parameters

* **Namespace:** DID name space. Possible value is `testnet` &#x20;

#### Optional Parameters

* **MethodSpecificId**: Custom Id string which you want to attach with the DID. Please read [did:hid method spec](https://docs.hypersign.id/concepts/decentralized-identifier-did/did-registry#syntax-of-did-hid-method) for details about possible format.
* **Options.keyTypes**: We support `Ed25519VerificationKey2020`, `EcdsaSecp256k1RecoveryMethod2020` verification method key types. So only these two are possible values. Read the full [specification here](../../concepts/specifications/supported-signature-algorithms.md).
* **Options.publicKey**: Please pass  the `options.publickey` property only for `Ed25519VerificationKey2020` verification method key type. For `EcdsaSecp256k1RecoveryMethod2020` , this property can be kept blank.  Its value would be publickey (in multi base format)
* **Options.walletAddress:** Please pass `options.walletAddress` for keyType `EcdsaSecp256k1RecoveryMethod2020`
* **Options.chainId:** ChainId in HEX format. For example for Etheruem main net, the chain id would be  `0x1`. This property is only required for keytype `EcdsaSecp256k1RecoveryMethod2020`&#x20;

{% hint style="info" %}
**Note**: If no optional parameters are provided then, did will be created of verification key method type `Ed25519VerificationKey2020`
{% endhint %}

{% hint style="info" %}
**Note:** If you want to create DID for blockchain wallet addresses like EVM wallets, Cosmos wallets, you should use keyType as . Read  `EcdsaSecp256k1RecoveryMethod2020`
{% endhint %}

### Register a DID

Registers a Signed DID Document in [DID registry](../../concepts/decentralized-identifier-did/did-registry.md). The Gas fee ([network fee](../developer-dashboard/network-fee.md)) for this DID registration will be done by applications' walletAddress.&#x20;

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/did/register" method="post" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

#### Request Parameters

* **didDocument :**  DID documented generated using `/api1/v1/did/create` API
* **verificationMethodId** :  Verification Method id of referred verification method in the didDocument

**Optional Parameters**

* **clientSpec :** Wallet specifications which are used to sign the didDocument string. Use `eth-personalSign` for Metamask and `cosmos-ADR036` for Keplr wallet. Learn more about client specifications [here](../../concepts/specifications/client-specification/).
* **signature:** If didDocument is signed using client wallets (Metamask or Keply) then pass the signature hex string.&#x20;

Note: Read how to use Metamask to create Hypersign DID.&#x20;

### Resolve a DID

Given a DID Id (example: `did:hid:testnet:0x123123123123`), this API will resolve the corresponding DID Document from the [DID registry](../../concepts/decentralized-identifier-did/did-registry.md) (or Hypersign Blockchain).&#x20;

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/did/resolve/{did}" method="get" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

### Fetch all DIDs for your apps

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/did" method="get" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

### Update a DID

Update a DIDDocument

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/did" method="patch" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

#### Request Parameters

* **didDocument :**  DID documented to be updated
* **verificationMethodId** :  Verification Method id of referred verification method in the didDocument
* **deactivate** : `true` is you want to deactivate this DID, `false` otherwise.&#x20;

**Optional Parameters**

* **clientSpec :** Wallet specifications which are used to sign the didDocument string. Use `eth-personalSign` for Metamask and `cosmos-ADR036` for Keplr wallet. Learn more about client specifications [here](../../concepts/specifications/client-specification/).
* **signature:** If didDocument is signed using client wallets (Metamask or Keply) then pass the signature hex string.&#x20;

###
