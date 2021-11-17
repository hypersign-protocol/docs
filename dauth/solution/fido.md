---
description: Fast Identity Online
---

# FIDO

As per the official [FIDOAlliance.org](https://fidoalliance.org/what-is-fido/).

> FIDO Authentication enables password-only logins to be replaced with secure and fast login experiences across websites and apps.

FIDO uses digital signatures to solve password problems and also provided multiple ways to manage private keys. With the evolution of smartphones, a user/prover can use mobile phones as one of authenticators devices to store private keys and generate digital signatures.

The concept of **Authenticators** is introduced in the FIDO authentication standard.

> **Authenticator** represents the user facing portion of the FIDO protocol. During registration and authentication both, the user has to interact with authenticator to _confirm posession_ of the private key, stored in authenticator device.
>
> These authenticators are responsible for _protecting cryptographic key materials_ like private keys.

FIDO proposes various **types of Authenticators** like _smartphones_, _USB_, _NFC_, or special hardware chips like _Trusted Platform Module (TPM)_, _Secure Execution Environment (SSE)_ etc. Enterprises can use them depending on their need. Read more about Authenticator types in this [whitepaper published by FIDO Alliance.](https://media.fidoalliance.org/wp-content/uploads/2021/09/FIDO-White-Paper-Choosing-FIDO-Authenticators-for-Enterprise-Use-Cases.pdf)

## The answer to our "first" question

It looks like we have the answer to our first question - <mark style="color:green;">**"How does a prover/user manage private keys?"**</mark>.

> A user/prover can store private keys in authenticators devices / softwares securely and can obtain the private key when producing the digital signature.

What about the second question? - <mark style="color:blue;">**"How does a verifier get the public key of prover to verify the digital signature?"**</mark>. How does that work in FIDO?&#x20;

Before we get to the answer, we need to understand how FIDO works at a very high level, read the next section to know that.
