# idToken

<mark style="color:green;">`GET`</mark> {kyc\_server\_base\_url}/api/v1/e-kyc/verification/user-consent

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
