---
description: A specification to store wallet address of multiple chain on Hypersign DID
---

# Blockchain Account Id

### [EIP-155](https://eips.ethereum.org/EIPS/eip-155) - Identifying a blockchain within Ethereum ecosystem



ChainID  was introduced in EIP-155 to prevent **replay attacks** between the main ETH and ETC chain since they both have same networkID `1`.  Its an additional way to tell the chains are apart. So, now due to EIP-155, ETH has a chainId `1` whereas ETC has a chainID of `61`.  (see [chainlist](https://chainid.network/) here)

**What is replay attack?**

In EVM ecosystem, same account address can be used in multiple chains. Hence it was possible to send same transactions on multiple chains - hence the term replay attack. For example, it is possible to issue a fund transferon a testchain and then perform same transfer on Mainnet. This vulnerability is because that the same account (corresponding to same private key) can exists in any EVM chains.

**Specification**

To fix this issue Ethereum allowed insertions of ChainID data in the signed transaction.

So earlier we generated transaction hash using these values:

```
(nonce, gasprice, startgas, to, value, data)
```

But now, we will generate transaction hash using these values:&#x20;

```
(nonce, gasprice, startgas, to, value, data, chainid, 0, 0)
```



### [CAIP-2](https://chainagnostic.org/CAIPs/caip-2) - Identifying a blockchain in any ecosystem&#x20;

> Its a way to identify different blockchains (e.g. Ethereum Mainnet, Cosmos hub, Bitcoin etc) in developer-friendly manner.&#x20;

We often need to reference a blockchain to state where some asset like token or smart contract is located. In Ethereum the EIP-155 chain ID is used most of the time but with Ethereum Chain ID, you can not reference other blockchains like Bitcoin or Cosmos.&#x20;

**Specification:**

```
chain_id:    namespace + ":" + reference
namespace:   [-a-z0-9]{3,8}                # Class of similar chains, e.g cosmos, eip155 etc
reference:   [-_a-zA-Z0-9]{1,32}           # A way to identify a blockchain within a given namespace
```

**E.g:**

```
# Ethereum mainnet
eip155:1

# Cosmos Hub (Tendermint + Cosmos SDK)
cosmos:cosmoshub-2
cosmos:cosmoshub-3
cosmos:hid-jagrat

# Litecoin
bip122:12a765e31ffd4059bada1e25190f6e98
```

### [CAIP-10](https://chainagnostic.org/CAIPs/caip-2) - Identifying a walletaddress in any ecosystem

> CAIP-10 extends CAIP-2 to the account level. This specification facilitate specifying <mark style="background-color:yellow;">**accounts**</mark> for any blockchains.  Its <mark style="background-color:yellow;">chain-agnostic</mark> protocol for [communication between dapps and wallets ](#user-content-fn-1)[^1]that was independent of any blockchain but provide the flexibility to be backwards compatible with existing applications.

It is useful for both decentralized applications (dApps) and wallets to communicate user accounts for multiple chains using string identifiers specific to each chain.



**Specification:**

The `account_id` is a case-sensitive string in the form

```
account_id:        chain_id + ":" + account_address
chain_id:          [-a-z0-9]{3,8}:[-_a-zA-Z0-9]{1,32} (See [CAIP-2][])
account_address:   [-.%a-zA-Z0-9]{1,128}
```

**E.g:**

```
# Ethereum mainnet (canonicalized with [EIP-55][] checksum)
eip155:1:0xab16a96D359eC26a11e2C2b3d8f8B8942d5Bfcdb

# Cosmos Hub
cosmos:cosmoshub-3:cosmos1t2uflqwqe0fsj0shcfkrvpukewcw40yjj6hdc0
cosmos:hid-jagrat:hid1yya5gl4v6sj3qn0l06ngz0uuxg995mm9ps087u

# Bitcoin mainnet
bip122:000000000019d6689c085ae165831e93:128Lkh3S7CkDTBZ8W7BbpsN3YYizJMp8p6

```

{% hint style="info" %}
**CAIP-2** describes blockchain Id whereas **CAIP-10** describes account Id
{% endhint %}

### BlockchainAccountId



`blockchainAccountId`  field or property of verification method in Hypersign DID, is used to specify a blockchain **account** id as per CAIP-10 specification.

```
  {
      "id": "did:hid:z6PWsg9vW5LL3dpnaQwv3mAi28Hn5YXQv3eu557uGhiTp#key-1",
      "type": "EcdsaSecp256k1RecoveryMethod2020",
      "controller": "did:hid:z6PWsg9vW5LL3dpnaQwv3mAi28Hn5YXQv3eu557uGhiTp",
      "blockchainAccountId": "eip155:1:0x749183517381758E186910DC47bcbE456458216E"
    }
```

[^1]: 
