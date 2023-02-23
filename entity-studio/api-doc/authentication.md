---
description: Generate access token using API secret Key
---

# Authentication

Register your application on [Entity Studio Developer Dashboard](../developer-dashboard.md) and generate your API secret Key before proceeding.&#x20;

Once the API secret key is generated, you can use the API below to generate a new access token. Just pass your API secret Key in `X-Api-Secret-Key` header to generate access token. The `access_token` is required to access all SSI APIs. Read the next section for more details.&#x20;



{% hint style="info" %}
Entity Studio SSI API base URL: [https://api.entity.hypersign.id](https://api.entity.hypersign.id)
{% endhint %}

{% swagger src="../../.gitbook/assets/api-json (1).json" path="/api/v1/app/oauth" method="post" %}
[api-json (1).json](<../../.gitbook/assets/api-json (1).json>)
{% endswagger %}

