# Frontend Integration

### Pre-requisites

Generate your access tokens before proceeding:

{% content-ref url="../backend-integration/generate-accesstokens.md" %}
[generate-accesstokens.md](../backend-integration/generate-accesstokens.md)
{% endcontent-ref %}

Optionally, generate KYC `sessionId` as well.&#x20;

{% content-ref url="../backend-integration/generate-kyc-session-id.md" %}
[generate-kyc-session-id.md](../backend-integration/generate-kyc-session-id.md)
{% endcontent-ref %}

### Widget Integration

You'll need to generate a **Widget URL** and insert it into a DOM element. Additionally, you can monitor events triggered by the widget on your webpage to showcase either success or failure. Once the user completes the KYC process successfully, you'll receive an `idToken`, which can be utilised to request the user's data/credentials from the KYC server.

### Forming Widget URL

The Widget URL has  three query params:

1. **`kycAccessToken`**: KYC Access Token
2. **`ssiAccessToken`**: SSI Access Token
3. **`sessionId`**: KYC Session Id

The final Widget URL format would look something like this:

> ```
> https://verify.hypersign.id
> ?kycAccessToken=${kycAccessToken}&ssiAccessToken=${ssiAccessToken}&sessionId=${sessionId}
> ```

### Invoking the widget

You can invoke the Hypersign KYC widget through popup from your page

```javascript
const widgetUrl = `https://verify.hypersign.id
?kycAccessToken=${kycAccessToken}&ssiAccessToken=${ssiAccessToken}&sessionId=${sessionId}`

window.open(widgetUrl, 'Popup Window', 'width=850,height=900');
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
