# Proof Of Personhood (PoP)

Hypersign’s PoP leverages video KYC and [Zero-Knowledge Proofs (ZKPs)](../zero-knowledge-proof-zkp/) to verify if a specific account (or wallet address) belongs to a real human.

<figure><img src="../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

### How It Works?

1\. **Video Capture and Verification**

The process begins with a user submitting their video KYC through Hypersign's KYC Widget. Once the video is collected, it undergoes a series of AI-driven checks:

* **Liveness Detection**: The AI model uses liveness detection to confirm that the person is physically present in real-time, as opposed to a static image, video replay, or deepfake. This involves subtle movement analysis, such as blinking, head movements, and sometimes following prompts like changing gaze direction or smiling.
* **Anti-Spoofing Measures**: The AI model detects spoofing attempts, such as using photos, videos, or masks. Techniques like depth analysis and light reflection analysis differentiate between a real face and 2D images or video screens.

2\. **Credential Issuance**

Once all checks pass, the KYC issuer provides a Personhood Credential. This credential confirms that the user has passed all necessary verifications and includes a digital signature from the issuer. The user then stores the Proof of Personhood credential securely in their data vault.

3\. **Zero-Knowledge Proof (ZKP) Generation**

After receiving the credential, the user generates a [zero-knowledge proof (zk proof)](../zero-knowledge-proof-zkp/) of it. This proof, also known as the Proof of Personhood (PoP), is created by submitting the credential to a custom-built [zk circuit](../zero-knowledge-proof-zkp/circuits.md), where a groth16-based zk proof is generated. This proof maintains privacy while verifying personhood.

4\. **Proof of Personhood Token Generation**

Finally, the user submits the Proof of Personhood (PoP) to the issuer's smart contract, requesting a Hypersign KYC Token, which is a Soulbound Token signifying Proof of Personhood. The smart contract verifies the zk proof and mints a token directly to the user’s wallet, establishing a blockchain-backed verification of personhood.
