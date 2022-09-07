---
description: Digital signatures come to rescue
---

# Solution

> _\*\*The only way to solve the password problem is, by completely eliminating it from the ecosystem. OTP was a good attempt but it is far from the perfect solution. \*\*_

### Digital Signatures

Digital Signature comes to the rescue. The concept of digital signatures is very old and is vastly being used in securing websites (the SSL). It is based on a pair of keys, a **private/secret key** - which is only known to the user and a **public key** - which is known to everyone.

A user generates a digital signature using the private key he holds and the signature can be verified by a verifier using the corresponding public key without sharing any critical piece of information by the user. Read more about the digital signature on Wikipedia.

The concept of the digital signature can be applied to authentication also. Where a user can produce a digital signature to the server and the server can verify the signature using user's public key without having to share any shared secret information like a password. However, there is one small problem.

> It is very hard to remember private key as private keys are very long random string.

The major challenge of using digital signatures is the **key management**.

#### That leads us to two questions:

> 1. <mark style="color:green;">**How can a prover manage private keys?**</mark>
> 2. <mark style="color:blue;">**How can a verifier get the public key of the prover to verify the signature?**</mark>
