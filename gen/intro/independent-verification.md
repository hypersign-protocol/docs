# Independent Verification

Although service providers in the Hypersign ecosystem trust the Issuer, unlike legacy systems, _**the verifier need not to rely on the issuer or the IDP to be available online for verification of credentials**_ given by the user. This means that the verifier can verify the credential on its own. This makes Hypersign protocol unique among its competitors.

\
Blockchain plays an important role in the Hypersign ecosystem.&#x20;

> _**The Hypersign protocol uses blockchain for global tamper proof registry of public keys.**_&#x20;

Blockchain gives the ability to all actors to verify digital signatures of each other on their own. Take a look at the figure below to understand the complete flow.&#x20;

![](<../../.gitbook/assets/image (8).png>)

In order to verify digital signatures of the issuer and the user, the verifier queries the blockchain with respect to an identifier also called decentralised identifier aka DID, and fetches public keys. Now these public keys are used to verify digital signatures.&#x20;

> The procedure of independent verification helps to scale the overall system and reduce the trust from IDP
