# Introduction

Zero-knowledge proofs involve two parties: a prover and a verifier.

* The **prover** makes an assertion that his or her proof is valid
* which the **verifier** must approve, without the prover leaking any “knowledge” other than the assertion itself.

> **How can the verifier validate an assertion without any knowledge of the content and minimal interaction with the prover?**

_This is where zero-knowledge proofs become useful !_

* Imagine frequent scenarios when one reveals private information to verify something about one’s identity
* When one applies for a credit card, he or she must give up his social security number
* When one checks in for a flight at the airport, he or she must reveal all the private information present on the passport, such as birthdate or passport number
* Even on a day-to-day basis, when a user logs on to a web or mobile application, the user must enter a password to the account and send this sensitive information to the server, trust that the application securely handles this information, and that the password is not intercepted over the network.

### 3 Essential Properties of ZKP

1. **Completeness**: Suppose a prover knows a secret number 𝑥  that solves a particular equation. Completeness guarantees that, if 𝑥  is indeed the solution, the verifier will be convinced of this without directly learning 𝑥 .
2. **Soundness**: Imagine a prover doesn’t actually know the secret number 𝑥  but tries to fool the verifier into believing they do. Soundness ensures that any false or misleading proof will be detected by the verifier.
3. **Zero knowledge**: Continuing with our secret number 𝑥 , zero-knowledge means the verifier can be convinced that the prover knows 𝑥  without learning anything about 𝑥 itself or how to solve the equation.
