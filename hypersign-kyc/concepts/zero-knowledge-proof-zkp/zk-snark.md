# zk-SNARK

### Zero Knowledge Succinct Non-interactive Argument of Knowledge (zk-SNARK)

Zk-SNARKs are specifically [zero-knowledge proofs](introduction.md) that are:

* **Succinct:** meaning they can be verified in the matter of milliseconds with a proof length of a few hundred bytes_._
* **Non-interactive:** refers to fact that the prover can send a single message to the verifier, without having many back-and-forth interactions.&#x20;

> Apart from these 3 requirements for zkp, **completeness**, **soundness**, and **zero-knowledge**, zk-SNARK adds few more for efficiency for the proving system.

A notable advantage of zkSNARK's is their relatively _small proof sizes_ and _constant-time verification_.

### Groth16

[Groth16](https://eprint.iacr.org/2016/260.pdf) is a proving scheme, which is widely-used, efficient ZK-SNARK protocol developed by Jens Groth in 2016 that _minimizes_ proof size and verification time. It is a _circuit-specific_ preprocessing general-purpose zk-SNARK construction. It has become a de-facto standard used in several blockchain projects due to the constant size of its proof, and its appealing verifier time.

{% hint style="info" %}
Although, Groth16 required circuit-specific [trusted setup](zk-snark.md#trusted-setup), we decided not to go with Plonk because proof generation time in Plonk was very high (sometime in minutes) for our custom circuit.  Moreover, proofs are shorter in Groth16 hence better performance and less Gas consumption (?).
{% endhint %}

### BN128 elliptic curve

[Groth16](zk-snark.md#groth16) need to be instantiated with an elliptic curve. To work with Groth16 curves must be:

1. Be secure, for proof soundness
2. Be pairing-friendly, for proof verification
3. Have a highly 2-adic subgroup order, for efficient proof generation.

We had three objectives while choosing the curve,&#x20;

* a) Proofs generation should be fast (should generate proofs in seconds and not in minutes)
* b) Proofs should be decently secure (we are "okay" with 128bit security)
* c) Proofs should be compatible (proofs generated should be compatible with Ethereum as well as Cosmwasm contracts)

We decided to go with `BN128` since its fast and is natively supported in Ethereum 1.0, which provides precompiled contracts for efficient pairing operations on this curve. As far as Cosmwasm is concerned, we had to use [3rd party libraries](https://github.com/hypersign-protocol/hypersign-kyc-contracts/blob/main/packages/hypersign-zk-verifier/Cargo.toml) to give support for `BN128` based proofs since Cosmwasm do not natively support this curve (yet).

{% hint style="info" %}
The `BN254` curve belongs to the BN family and is colloquially called `BN128` in reference to the nominal security of the curve, or `BN254` in reference to the bit-length of the relevant prime field. So not to be confused, they both are same.&#x20;
{% endhint %}

### Trusted Setup

Setting up the ZK-SNARK protocol requires the creation of a **Universal Common Reference String (CRS).** Also described as _public parameters_, the CRS enables secure communication between provers and verifiers.  This CRS must be generated in advance by a trusted party. But the security of a system based on zkSNARKs largely boils down to how the CRS was generated. Doing so without compromising the ideals of privacy-preserving blockchain-based systems: (security and decentralization) is very important. The generation of public parameters for zkSNARKs is called the **“setup ceremony”** because of its importance and the need for _multiple independent parties_ to contribute to the process.&#x20;

The preferred technique for setup ceremonies has been multi-party computation (MPC). Setup ceremony MPC schemes are interactive protocols involving multiple parties who _**contribute randomness**_ to iteratively construct the CRS. A typical ceremony consists of `N` number of players, the coordinator, and the verifier. The MPC protocols are always of a round-robin nature, where a player `Pi` receives a single message from player `Pi-1.`Payer `Pi` adds their input to _accumulated randomness_ before passing it onto Player `Pi+1`. In the end, the final result is the CRS.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption><p>BGM17 MPC Protocol, Ref: <a href="https://zkproof.org/2021/06/30/setup-ceremonies/">https://zkproof.org/2021/06/30/setup-ceremonies/</a></p></figcaption></figure>

The CRS is generated in two phases:&#x20;

* The first phase (phase-1) referred to as “**Powers of Tau**”, produces generic setup parameters that can be used for all circuits of the scheme, up to a given size. This ceremony is _perpetual_ — that is, there is no limit to the number of participants required, and any zk-SNARK project can pick any point of the ceremony to begin their circuit-specific second phase (phase-2).
* The second phase (phase-2) converts the output of the "Powers of Tau" phase (phase-1) into an NP-relation-specific (circuit-specific) CRS.

How does PoT (phase-1) ceremony works?&#x20;

* Each participant will receive a _challenge_ file.
* They must generate a _response_ file in a secure and honest manner.&#x20;

> As long as one participant discards the toxic waste after this process, the entire ceremony can be trusted.

{% hint style="info" %}
We did not run our own PoT phase-1 ceremony, instead we used Ptau files (of power `19` or `512` max constraints) for BN128 curve with 54 contributions from iden3 [here](https://github.com/iden3/snarkjs?tab=readme-ov-file#7-prepare-phase-2).
{% endhint %}

<mark style="color:orange;">You might be wondering what exactly is this max-constraints?</mark>

* The Power of  Tau setup generates a series of powers of a secret value, `τ`, up to a specific limit, say `τ^N` . This maximum power `N` directly determines the maximum number of constraints that can be supported in circuits using these parameters.
* If the setup phase generates up to `τ^N`, it means that the final setup parameters can support up to **N constraints** in the ZK-SNARK circuit.
* iden3 ceremonies have gone as high as `τ^2^28`, which allows for up to **268 million constraints**.
* Higher values of `𝑁` increase the computational load of the setup ceremony but offer more flexibility for complex circuits in the future.

<mark style="color:orange;">and why did we choose 512 as our max constraints?</mark>&#x20;

Choosing the power `N` depends on circuits and its completxity. For example, for our custom KYC circuits we needed minimum power `19` to put in perspective zk-rollups may need millions of constraints hence they need to use higher power value.

