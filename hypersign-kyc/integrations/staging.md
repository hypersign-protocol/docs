---
description: How to integrate Hypersign KYC in your test environment
---

# Staging

> Staging Widget Base URL : [https://hypersign-kyc-widget.netlify.app](https://hypersign-kyc-widget.netlify.app)

## Hypersign KYC Widget integration

The Hypersign KYC widget can be configured and incorporated in just a few minutes. You'll need to generate a **Widget URL** and insert it into a DOM element. Additionally, you can monitor events triggered by the widget on your webpage to showcase either success or failure. Once the user completes the KYC process successfully, you'll receive an `idToken`, which can be utilized to request the user's data/credentials from the KYC server.

### Forming Widget URL

The Widget URL has  three query params:

1. **`pr`**: Presentation Query Request (base64 encoded)
2. **`kycAccessToken`**: KYC Access Token
3. **`ssiAccessToken`**: SSI Access Token

The final Widget URL format would look something like this:

> [https://hypersign-kyc-widget.netlify.app](https://hypersign-kyc-widget.netlify.app)?kycAccessToken=${kycAccessToken}\&ssiAccessToken=${ssiAccessToken}\&pr=${base64EncodedPr}

Let's go ahead and get vaules for each of these query params. We will start with Presentation Query Request

#### 1. Presentation Request&#x20;

The Presentation Query request is a way to request user's credential from their data vault. The presentation query request is implemented based on [W3C Verifiable Presentation Request v0.2 Specification](https://w3c-ccg.github.io/vp-request-spec/) - that means its being widely adopted in the SSI ecosystem.&#x20;

Below is the sample presentation query request object:&#x20;

```json
{
    "query": [
        {
            "type": "QueryByExample",
            "credentialQuery": [
                {
                    "example": {
                        "type": "PersonhoodCredential",
                        "credentialSchema": {
                            "id": "sch:hid:testnet:z6Mkvtd73dDgg7HU8wLCmXbe2RAHPAU1Ex1VUXCFtPV7u36i:1.0"
                        }
                    },
                    "trustedIssuer": [
                        {
                            "required": true,
                            "issuer": "did:hid:testnet:zCyAz2wfKjAaWE4FW75KxpZh2wuo9kRAUZyV2xEe93cKr"
                        }
                    ]
                }
            ]
        },
        {
            "type": "QueryByExample",
            "credentialQuery": [
                {
                    "example": {
                        "type": "PassportCredential",
                        "credentialSchema": {
                            "id": "sch:hid:testnet:z6MkgMXXQL7YD7BufNLbjrwueoj4nmih9xujJ6aozJDmzFWx:1.0"
                        }
                    },
                    "trustedIssuer": [
                        {
                            "required": true,
                            "issuer": "did:hid:testnet:zCyAz2wfKjAaWE4FW75KxpZh2wuo9kRAUZyV2xEe93cKr"
                        }
                    ]
                }
            ]
        }
    ],
    "reason": "<Provide a vaild reason>",
    "issuerDID": "did:hid:testnet:3d11e40f-2250-4846-bd23-bfb58cf4eea5",
    "issuerDIDVerificationMethod": "did:hid:testnet:3d11e40f-2250-4846-bd23-bfb58cf4eea5#key-1",
    "domain": window.location.href,
    "logoUrl": "<Your Logo Url>"
}
```

1. **Reason**: Please furnish a legitimate justification for why you are seeking access to user data. This information will be displayed on the consent screen for users to review and authorize your app to access their data. Max `110` chars are supported.
2. **LogoUrl**: Provide a URL for the monologue that users can view on the consent screen. See the example widget consent screen for reference.&#x20;

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Once presentation query request object is ready, we need encode it in [base64](https://en.wikipedia.org/wiki/Base64) string so that we can pass it in Widget URL.&#x20;

```javascript
const presentationRequest = {
   "query": [...],
   "reason": "The verifier app need access of your data",
   "issuerDID": "did:hid:testnet:3d11e40f-2250-4846-bd23-bfb58cf4eea5",
   "issuerDIDVerificationMethod": "did:hid:testnet:3d11e40f-2250-4846-bd23-bfb58cf4eea5#key-1",
   "domain": window.location.href
   "logoUrl": "https://i.ibb.co/xmxv8kw/Screenshot-2024-03-12-at-3-18-37-PM.png"
}
// stringifying it
const presentationRequestStr = JSON.stringify(presentationRequest)
// converting it in base64 string
const base64EncodedPr = btoa(presentationRequestStr)
```

Here I am using [btoa](https://developer.mozilla.org/en-US/docs/Web/API/btoa) utility function in browser to convert stringified presentation request object to base64 string.&#x20;

#### 2. KYC Access Token

> Kindly contact Hypersign Admin.&#x20;

#### 3. SSI Access Token

> Kindly contact Hypersign Admin.

### Invoking the widget

You can invoke the Hypersign KYC widget through popup from your page

```javascript
const widgetUrl = `https://hypersign-kyc-widget.netlify.app
?kycAccessToken=${kycAccessToken}&ssiAccessToken=${ssiAccessToken}&pr=${base64EncodedPr}`

window.open(widgetUrl, 'Popup Window', 'width=850,height=870');
```

### Listening to events

You can listen to events thrown by the widget to get the result of verification.&#x20;

```javascript
window.addEventListener('message', function (event) {
    if (event.origin === 'https://hypersign-kyc-widget.netlify.app') {
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

Once you receive the `idToken`, you can query the KYC service to extract user data.&#x20;

**Staging KYC service Request:** &#x20;

KYC  service URL:

```html
https://ent-4c71874.api.cavach.hypersign.id/api/v1/e-kyc/verification/consent?idToken=${idToken}
```

Method:

`GET`

Headers:&#x20;

```
'Authorization': 'Bearer ' + ${kycAccessToken}
'content-type': 'application/json'
```

## Demo&#x20;

{% embed url="https://www.youtube.com/watch?v=3oMbGp66G1k" %}
Hypersign KYC Widget demo for Facial Recognition
{% endembed %}

> Try Demo Now:  [https://hypersign-kyc-demo.netlify.app/](https://hypersign-kyc-demo.netlify.app/)
