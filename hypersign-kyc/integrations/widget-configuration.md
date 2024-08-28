# Widget Configuration

[Hypersign KYC widget](../kyc-widget/) is web based application to capture user's data. It is used to capture, user facial detail, ID document, user consent etc. In order to use KYC Widget in your frontend, you first need to configure it in the [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/).

Logon to [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/). and proceed to "**Know Your Customer**" tab of your services and click on your KYC service tile.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Your KYC service dashboard opens up.  Now navigate to "**Widget Configuration**" page by clicking on "**Widget**" menu item in the side nav bar.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

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

### Trusted Issuer

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



