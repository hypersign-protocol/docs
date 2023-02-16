---
description: Manage DID operation using DID APIs
---

# DID

Please [generate access token](authentication.md) before proceeding.  Once you generated the `access_token`, you can pass this token as bearer authorization token in the header for all APIs.&#x20;



{% hint style="info" %}
**NOTE:** Some of these APIs are on-chain APIs which means they need network fee to successfully execute, so make sure that your application wallet address has $hid tokens. Read [network fee](../developer-dashboard/network-fee.md) section for more details.
{% endhint %}

### Create a DID

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/did" method="post" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

### Resolve a DID

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/did" method="get" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

### Fetch all DIDs for your apps

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/did" method="get" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

### Update a DID

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/did" method="patch" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

###
