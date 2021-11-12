# Introduction

Hypersign is a decentralised identity and access management infrastructure for the enterprise. It leverages technologies such as public key infrastructure (PKI) and blockchain to provide passwordless authentication as well as authorization and verification services which integrate within minutes and is compatible with legacy IAM systems at an affordable price-point.

The Hypersign works on the concept of Issuance-verification paradigm where we essentially have three stakeholders.

![](<../../.gitbook/assets/image (7).png>)

* Users:  Access services and hold their own personal data \[End Users].
* Issuer: The one who verifies user-data and issues credentials based on user-data. I.e identity provider.
* Verifier: The one who verifies credentials. I.e service provider.

The Hypersign protocol distributes the responsibility of issuance, holding and verification among stakeholders. In the above figure, the user gives personal-data to the issuer, which verifies and issues a cryptographically signed document (_verifiable credential_) to the user.

The _verifiable credential _contains user-data along with the digital signature of the issuer.  At this stage the issuer need not to store user-data and can act as a stateless server. Optionally, Issuer can store data in encrypted form for recovery or future access. \


The end-user can store the verifiable credential in any user-agent such as a mobile device or cloud agent which only they have access to. This gives the end-user the ability to control their own personal data. \


The user can now present this credential to the service provider, in a peer-to-peer fashion without notifying the identity provider or the issuer, whenever they want to use a service. _**This gives the end user a sense of privacy that he is not being tracked or traced**_.  Before sharing the verifiable credential, the end-user also attaches his digital signature on the document.  \


The verifier or service provider can obtain user-data from the verifiable credential and can verify digital signatures of the user and the identity provider. _**The multi-signature mechanism is to ensure that not just the right issuer but also the right owner of the document.**_ Furthermore, the digital signatures also ensure the integrity of the document. The credential presented by the end-user can be verified by the service provider independently - _without making a verification request to the issuer or IDP_. This helps SP to scale the system as it need not to require the IDP to be available online at the time of verification.
