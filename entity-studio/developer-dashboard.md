---
description: >-
  Manage your application and API keys and start building your identity product
  on our infrastructure
---

# 📈 Developer Dashboard

### Register Application&#x20;

Navigate to [Entity Studio Developer dashboard ](https://entity.hypersign.id)and login. You will land on your dashboard.&#x20;

<figure><img src="../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p>Developer dashboard</p></figcaption></figure>

Upon login, click on **+Create** button to register an application.&#x20;

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption><p>App registration form</p></figcaption></figure>

Fill basic details like application name, description and allowed origins and hit **Save** button to register your brand new application.



### API Secret Key

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption><p>API secret Key</p></figcaption></figure>

Upon successful registration, an API secret key will be generated for your app. You may use this API secret key to generate access token to access all SSI APIs. Read more about it in [authentication](api-doc/authentication.md) section.&#x20;

{% hint style="warning" %}
<mark style="color:red;">Make sure to copy and save API secret key securely. If lost, this key can not be recovered. However, you can regenerate a new one.</mark>
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2023-02-16 at 1.01.50 AM.png" alt=""><figcaption><p>Regenerate a new API secret by clicking on this icon</p></figcaption></figure>



### Edit / View Application

Click on **Edit** icon of your application's card.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-02-16 at 4.01.33 PM.png" alt=""><figcaption></figcaption></figure>

Right slider will pop up. You can edit few details like name, description, CORS etc or view other fields.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-02-16 at 4.16.41 PM.png" alt=""><figcaption></figcaption></figure>

### Fields

**Encrypted Data Vault Id**

> TODO: Link to the security section

**Allowed Origins (CORS)**

> TODO: describe about CORS

**Wallet Address**

Read network fee section for detail

{% content-ref url="developer-dashboard/network-fee.md" %}
[network-fee.md](developer-dashboard/network-fee.md)
{% endcontent-ref %}



\----





Now that you have generated your API secret Key you can either go through our [API documentation](api-doc/) and start coding or jump into the [SSI API playground](api-playground.md) to play around with SSI APIs right before coding. Optionally, if you want  to get hands with concepts of the Self sovereign identiy (SSI), you can checkout [SSI playground](ssi-playground.md) for that.&#x20;

###
