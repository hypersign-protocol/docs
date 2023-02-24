# Verifiable Credential

Please [generate access token](authentication.md) before proceeding.  Once you generated the `access_token`, you can pass this token as  _<mark style="background-color:yellow;">bearer authorization token</mark>_  in the header for all APIs.&#x20;

### Issue a verifiable credential

An issuer may issue a [verifiable credential](../../concepts/verifiable-credential-vc/) to a subject using this API. The credential document is signed by issuer's identity key and its status is registered on the blockchain.&#x20;

{% hint style="info" %}
Entity Studio SSI API base URL: [https://api.entity.hypersign.id](https://api.entity.hypersign.id)
{% endhint %}

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/credential/issue" method="post" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

{% hint style="info" %}
NOTE: A developer may choose to store the verifiable credential in application's data vault securely or they may not to. Pass `true` for request body property `persist` to store the credential document, `false` otherwise.
{% endhint %}

### Verify an issued verifiable credential document

A signed verifiable credential must has signature of the issuer. Any one may verify an issued credential document. The verification result state the following facts:

> * _This document was issued by intended issuer_
> * _This document have not been tampered_
> * _This document have not been revoked_

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/credential/verify" method="post" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

{% hint style="info" %}
NOTE: Verifying a credential document is different than verifying a [verifiable presentatio](verifiable-presentation/)n. Verification result of later, also states that "_Only intended subject holds this document and not one else_".&#x20;
{% endhint %}

### Fetch a verifiable credential and/or its status by Id

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/credential/{credentialId}" method="get" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

{% hint style="info" %}
Pass `false` value to parameter `retrieveCredential` to only retrieve status of  the credential
{% endhint %}

### Fetch list of verifiable credentials

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/credential" method="get" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

### Update credential status of a verifiable credential

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/credential/status/{credentialId}" method="patch" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}
