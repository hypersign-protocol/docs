---
description: FIDO Has A Trust Problem
---

# FIDO Does Not Fit Into Web3.0

From the perspective of Web3.0, FIDO has a trust problem and does not really fit for Web3.0 internet. Let me explain how. Remember the second question? - <mark style="color:blue;">\*\*"How does the verifier get the public key of prover to verify a digital signature?" \*\*</mark>

> The problem with digital signature is, no matter how secure the algorithm you use, the whole system fails if keys are not managed properly.

The FIDO server holds the public keys of all the users and is likely to become _**a huge registry of trusted public keys over a period of time**_. Especially when it comes to 3rd party centralised Identity Provider setting - which most of the relying parties would like to use because it offloads complexities of authentication to the IDP.

![](<../../../.gitbook/assets/image (40).png>)

The way FIDO servers are likely to become **centralised** **data silo** and we all know problems with centralised systems especially when it comes to identity management:

1. \*\*Becomes a honey pot for attackers \*\*- _One place where all keys are stored!_
2. **Pron to trust problems** - _Issuance and verification by the same system!_
3. **Pron to scalability problems** - _Single point of failure!_
4. **Tracking and Traceability are also possible** - \_the FIDO server can link users with the RP! \_

and so on.
