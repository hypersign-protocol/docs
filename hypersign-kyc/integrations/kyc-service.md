---
description: Setup KYC service for your app on developer dashboard
---

# KYC Service

Inorder to use Hypersign KYC, you need to setup your account on [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/) and setup your KYC service.

### Pre-requisite

Before you setup your KYC service, you need to setup your SSI service:

{% content-ref url="../../hypersign-ssi/setup-ssi-service/" %}
[setup-ssi-service](../../hypersign-ssi/setup-ssi-service/)
{% endcontent-ref %}

and create a issuer DID:&#x20;

{% content-ref url="../../hypersign-ssi/setup-ssi-service/create-your-first-did.md" %}
[create-your-first-did.md](../../hypersign-ssi/setup-ssi-service/create-your-first-did.md)
{% endcontent-ref %}

You will need Issuer DID to setup KYC service and Issuer DID can only be created once you have SSI service.&#x20;

### KYC Service Setup

Once you have setup your SSI service and created your issuer DID, now you are ready to setup your KYC service on the [Entity Developer Dashboard](https://entity.dashboard.hypersign.id/).&#x20;

Login  to Entity Developer Dashboard and click on **'+Create'** to create a new serivce just like you did for SSI service.&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Create KYC Service</p></figcaption></figure>

> _If you have not created SSI service before, you will see the above screen other wise you will see list of services you have on the home screen_

Enter relevant details about your service and choose **"KYC API Service"** in the "**Select Service**" dropdown.&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Also make sure you associate SSI service and link issuer DID which you had created in the previous steps. Once all details are filled in the form, click the **"Save"** button to create your KYC service.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

An API secret key is generated for this service. You can save copy and save this Secret key for later purpose. Additionally you can always generate a new secret key, if you happen to loose it.&#x20;

Now that your KYC service is created, you are ready to setup KYC widget configuration. Let's proceed to Widget configuration page.&#x20;

{% content-ref url="widget-configuration.md" %}
[widget-configuration.md](widget-configuration.md)
{% endcontent-ref %}
