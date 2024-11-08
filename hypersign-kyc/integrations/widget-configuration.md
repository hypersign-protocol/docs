# Widget Configuration

[Hypersign KYC widget](../kyc-widget/) is web based application to capture user's data. It is used to capture, user facial detail, ID document, user consent etc. In order to use KYC Widget in your frontend, you first need to configure it in the [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/). Widget configuration enable you to do custom configurations of KYC widget for your users.&#x20;

Logon to [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/). and proceed to "**Know Your Customer**" tab of your services and click on your KYC service tile.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Your KYC service dashboard opens up.  Now navigate to "**Widget Configuration**" page by clicking on "**Widget**" menu item in the side nav bar.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### Facial Recognition

The first configuration is Facial recogination which is already enabled. So no need to do anything here.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

This feature, if enabled, will ask user to open their camera and record a video on KYC widget to prove he/she is a human. Once the data is collected and verified, KYC server issues a "**Personhood Credential**" to the user which acts as a proof that "_he/she is indeed a real human and not bot_".

{% hint style="info" %}
Check list of all supported credentials and proofs types here.
{% endhint %}

### ID Document Verification

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Now enable ID document verification setting and select document type as "**Passport**". The feature, if enabled, the KYC widget will ask users to provide ID document. The ID document is captured, data extracted and sent to the KYC service. KYC service does the following things with the data:

1. **Document Verification:** Checks if document was tampered or not in correct format. In some cases, it also verifies if digital signature attached with the document is correct or not.&#x20;
2. **OCR:** Extracts relevant data from the ID document.
3. **Facial Authentication:** Matches user's image in the ID document with the user's photo taken during the facial recognition step
4. **Uniqueness Check:** Checks if the user unique in the system - restricting same user not using same ID document with multiple accounts.&#x20;

Upon successful verifications of all, the KYC service issues him/her "**Passport Credential**", which is technically a [verifiable credential](../../hypersign-ssi/api-doc/verifiable-credential.md), to the user.&#x20;

{% hint style="info" %}
Check list of all supported credentials and proofs types here.
{% endhint %}

### User Consent

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Configure user consent page by providing a valid reason for "why you are collecting user's data". Read more about user consent here:

{% content-ref url="../kyc-widget/data-capture/capture-user-consent.md" %}
[capture-user-consent.md](../kyc-widget/data-capture/capture-user-consent.md)
{% endcontent-ref %}

### Zero Knowledge Proof (zk-proof)

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Enable zk-proof configuration if do not want to collect user's personal data but the proof of facts. We have following proofs available.

1. [**Proof Of KYC (PoK)**](../concepts/zk-proof-types/proof-of-kyc-pok.md):  Proves that user has finished his/her KYC. &#x20;
2. [**Proof Of Personhood (PoP)**](../concepts/zk-proof-types/proof-of-personhood-pop.md): Proves that user is not a bot
3. [**Proof Of Age (PoA)**](../concepts/zk-proof-types/proof-of-age-poa.md): Proves user is above the specified age (age need to be specified in text box)

Configure one of more proofs and click on **Update Configuration** button to save your settings.&#x20;

### On-Chain KYC

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

You might want to provide service to  users based on verification in your Dapp. For that your smart contracts wants to verify user's Identity before allowing to access other features of the smart contract. Since users cannot send his personal data to a contract because of obvious privacy issues with public blockchains, user first generates zk-proofs of their ID claims and only sends proofs to contracts, preserving privacy while enabling secure verification.  Make sure to [create On-Chain KYC configuration](../on-chain-kyc/contracts-deployment.md) in one of the supported blockchain before enabling this setting.

{% content-ref url="../on-chain-kyc/contracts-deployment.md" %}
[contracts-deployment.md](../on-chain-kyc/contracts-deployment.md)
{% endcontent-ref %}

{% hint style="info" %}
Make sure to enable zk-proof configuration before enabling On-Chain KYC configuration.
{% endhint %}

### Trusted Issuer

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Select one or more trusted issuers, with the default being 'self' - your own KYC service. This pertains to [**Reusable KYC**](../concepts/reusable-kyc.md). If configured, users who already possess KYC credentials issued by these trusted issuers in their [data vault](../kyc-widget/data-capture/data-vault-setup.md) will not need to repeat the KYC steps in the widget. They can simply authorise the sharing of their existing credentials with your app, streamlining user onboarding for your application and providing a smoother experience for your users.&#x20;

***

Now that your widget configuration is finished, you are ready to integrate Hypersign KYC in your application.&#x20;

{% content-ref url="../kyc-widget/integrations/" %}
[integrations](../kyc-widget/integrations/)
{% endcontent-ref %}
