# Webhook

Admin can setup webhook from their app's KYC dashboard. Login to Entity Developer Dashboard and navigate to the KYC app for you want to configure the Webhook.&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Webhook URL must be of HTTP method POST
{% endhint %}

Webhook works on "Fire & Forget" way. As soon as the KYC server verifies the KYC it simply executes the webhook with the following request body:

```javascript
{
   idToken: "",
   sessionId: ""
}
```

