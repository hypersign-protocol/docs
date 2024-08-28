---
description: How to integrate Hypersign KYC in your test environment
---

# Staging

> Staging Widget Base URL : [https://verify.hypersign.id](https://verify.hypersign.id)

> Staging KYC Server Base URL: [https://ent-4c71874.api.cavach.hypersign.id](https://ent-4c71874.api.cavach.hypersign.id)

## Hypersign KYC Widget integration

The Hypersign KYC widget can be configured and incorporated in just a few minutes. You'll need to generate a **Widget URL** and insert it into a DOM element. Additionally, you can monitor events triggered by the widget on your webpage to showcase either success or failure. Once the user completes the KYC process successfully, you'll receive an `idToken`, which can be utilised to request the user's data/credentials from the KYC server.

### Forming Widget URL

The Widget URL has  three query params:

1. **`kycAccessToken`**: KYC Access Token
2. **`ssiAccessToken`**: SSI Access Token

The final Widget URL format would look something like this:

> [https://verify.hypersign.id?kycAccessToken=${kycAccessToken}\&ssiAccessToken=${ssiAccessToken}](https://verify.hypersign.id/?kycAccessToken=${kycAccessToken}\&ssiAccessToken=${ssiAccessToken}\&session=${sessionId})

#### 1. KYC Access Token

> Kindly contact Hypersign Admin.&#x20;

#### 2. SSI Access Token

> Kindly contact Hypersign Admin.

### Invoking the widget

You can invoke the Hypersign KYC widget through popup from your page

```javascript
const widgetUrl = `https://verify.hypersign.id
?kycAccessToken=${kycAccessToken}&ssiAccessToken=${ssiAccessToken}`

window.open(widgetUrl, 'Popup Window', 'width=850,height=870');
```

### Listening to events

You can listen to events thrown by the widget to get the result of verification.&#x20;

```javascript
window.addEventListener('message', function (event) {
    if (event.origin === 'https://verify.hypersign.id') {
        console.log('Received message from popup:', event.data);
        // make sure to parse the data before use
        const data = JSON.parse(event.data)
        
        // we send these 3 vaules: 
        // status = success / fail, 
        // idToken = you will use this token to extract user's data
        // message = a simple message (if any)
        const { status, idToken, message} = data;
        if (status === 'success') {
            console.log('Successfully finished the KYC')
        }
        else if (status === 'fail') {
            console.log('Failed to finish KYC')
        }
    }
});
```

### Extracting User Data

Once you receive the `idToken`, you can query the KYC service to extract user data.  &#x20;

## User Data Request

<mark style="color:green;">`GET`</mark> {kyc\_server\_base\_url}/api/v1/e-kyc/verification/user-consent

> kyc\_server\_base\_url:  [https://ent-4c71874.api.cavach.hypersign.id](https://ent-4c71874.api.cavach.hypersign.id/)

**Headers**

| Name          | Value                       |
| ------------- | --------------------------- |
| Content-Type  | `application/json`          |
| Authorization | `Bearer <`kycAccessToken`>` |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "@context": [
  ],
  "type": ["VerifiablePresentation"],
  "VerifiableCredntial": [
      {
        ... 
      }
  ]
}
```
{% endtab %}
{% endtabs %}

```html
https://ent-4c71874.api.cavach.hypersign.id/api/v1/e-kyc/verification/user-consent?idToken=${idToken}
```

## Demo&#x20;

{% embed url="https://www.youtube.com/watch?v=3oMbGp66G1k" %}
Hypersign KYC Widget demo for Facial Recognition
{% endembed %}

> Try LIVE Demo Now:  [https://hypersign-kyc-demo.netlify.app/](https://hypersign-kyc-demo.netlify.app/)
