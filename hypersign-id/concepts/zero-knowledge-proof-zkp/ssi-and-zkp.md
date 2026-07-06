# SSI and ZKP

> The idea of using zero knowledge proofs to prove claims about aspects of an individual’s identity is a major use case for zk-SNARKs.

Questions like:

* “Are you over 21”?
* “Do you live in the US?”
* “Are you employed?”
* “Are you a real human being?”

Could be answered!

### The catch?

> _<mark style="color:orange;">**Identity usecase like KYC, simply verifying the ZK proof isn’t enough!**</mark>_

Suppose a verifier wants to confirm that a person is over 21 using zero-knowledge technology. In theory, anyone could generate a valid ZK proof of being over 21 with a credential (containing a date of birth field) issued by any random issuer—even if the circuit verifies the issuer’s digital signature.

> <mark style="color:yellow;">How can the verifier be 100% certain that the proof was actually generated using a date of birth field that comes from a verifiable credential issued specifically by the trusted issuer?</mark>

To answer this question, we need to design our [circuit](circuits.md) in such a way that it does the following this:&#x20;

1. Verifies if the issuer digital signature in the credential was correct?
2. Verifies if the credential was not revoked wrt current date?&#x20;
3. Verifies if user/holder's digital signature is correct?&#x20;
4. Verifies if user is above 21 (from the DOB field)?

Finally, exposes:&#x20;

* a) result of 4 (true/false),&#x20;
* b) issuer public key (or decentralised identity), &#x20;
* c) holder public key (or decentralised identity)&#x20;

as the public signal. Now send the _public signal_ and _zk proof_ both to the verifier.&#x20;

The verifier first checks that the exposed issuer’s public key (or DID) matches the trusted issuer’s identity, ensuring that the proof was indeed generated from a credential issued by a trusted source. Only then does it proceed to verify the ZK proof.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
