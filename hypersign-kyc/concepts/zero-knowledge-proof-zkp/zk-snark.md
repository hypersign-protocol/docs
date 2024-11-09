# zk-SNARK

### Zero Knowledge Succinct Non-interactive Argument of Knowledge (zk-SNARK)

Zk-SNARKs are specifically [zero-knowledge proofs](introduction.md) that are:

* **Succinct:** _meaning they can be verified in the matter of milliseconds with a proof length of a few hundred bytes._
* **Non-interactive:** refers to fact that the prover can send a single message to the verifier, without having many back-and-forth interactions.&#x20;

> Apart from these 3 requirements for zkp, **completeness**, **soundness**, and **zero-knowledge**, zk-SNARK adds few more for efficiency for the proving system.

A notable advantage of zkSNARKs is their relatively small proof sizes and constant-time verification.

### Groth16

[Groth16](https://eprint.iacr.org/2016/260.pdf) is a widely-used, efficient ZK-SNARK protocol developed by Jens Groth in 2016 that minimizes proof size and verification time.

### Trusted Setup

Setting up the ZK-SNARK protocol requires the creation of a **Universal Common Reference String (CRS).** Also described as _public parameters_, the CRS enables secure communication between provers and verifiers.  This CRS must be generated in advance by a trusted party. But the security of a system based on zkSNARKs largely boils down to how the CRS was generated. Doing so without compromising the ideals of privacy-preserving blockchain-based systems: (security and decentralization) is very important. The generation of public parameters for zkSNARKs is called the **“setup ceremony”** because of its importance and the need for _multiple independent parties_ to contribute to the process.&#x20;

The preferred technique for setup ceremonies has been multi-party computation (MPC). Setup ceremony MPC schemes are interactive protocols involving multiple parties who _**contribute randomness**_ to iteratively construct the CRS. A typical ceremony consists of `N` number of players, the coordinator, and the verifier. The MPC protocols are always of a round-robin nature, where a player `Pi` receives a single message from player `Pi-1.`Payer `Pi` adds their input to _accumulated randomness_ before passing it onto Player `Pi+1`. In the end, the final result is the CRS.

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption><p>BGM17 MPC Protocol</p></figcaption></figure>

The CRS is generated in two phases:&#x20;

* The first phase referred to as “**Powers of Tau**”, produces generic setup parameters that can be used for all circuits of the scheme, up to a given size.
* The second phase converts the output of the Powers of Tau phase into an NP-relation-specific CRS.
