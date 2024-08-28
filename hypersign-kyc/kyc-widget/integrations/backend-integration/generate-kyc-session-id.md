# Generate KYC Session Id

### Pre-Requisite

{% content-ref url="generate-accesstokens.md" %}
[generate-accesstokens.md](generate-accesstokens.md)
{% endcontent-ref %}

### KYC Session Id

To generate a new KYC Session Id, first, get your KYC Service **Tenant URL** from your KYC service tile.

<figure><img src="../../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

and call <mark style="color:green;">**POST**</mark> `/api/v1/e-kyc/verification/session` API to generate a new KYC session for your user. Make sure to pass `kycAccessToken` in the header.&#x20;

