# How Does FIDO Works?

### Registration

The registration process is fairly simple. User requests new registration flow from Relying Party (RP), also called Service Provider (SP). The RP connects with FIDO server (which could be self hosted or hosted by 3rd party Identity Provider (IDP)) to obtain a _challenge_ (think of, a random text) and sends that to the user.

The user generates private/public key pair, stores the _private key_ in the authenticator device and produces a _digital signature_ by signing the challenge. The user then sends the _digital signature _along with the corresponding _public key_ to RP which is then sent to the FIDO server.&#x20;

The FIDO server verifies the signature and _**stores the public key in its database**_.

![FIDO Registration Flow](<../../.gitbook/assets/image (38) (1).png>)

### Authentication

During authentication, a similar process happens. The user uses an authenticator to sign the challenge (produced during the new session by the FIDO server) and generate the digital signature. The user sends the digital signature as the response to RP which finally reaches the FIDO server.** **

The FIDO server verifies the signature of the challenge with a stored public key corresponding to user and device and sends a response to RP success or failure. &#x20;

![FIDO Authentication Flow](<../../.gitbook/assets/image (39).png>)

## The answer to our "second" question

I guess now we have the answer to our second question - <mark style="color:blue;">**"How does a verifier get the public key of prover to verify the digital signature?"**</mark>

> The FIDO server stores the public key in its database during the registration process and fetches it at the time of digital signature verification during authentication.



So, what's the issue here?&#x20;

