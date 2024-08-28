---
description: Generate access token using API secret Key
---

# Service Authentication

Register your service on [Entity Studio Developer Dashboard](../../hypersign-developer-dashboard/developer-dashboard/) and generate your API secret Key before proceeding.&#x20;

Once the API secret key is generated, you can use the API below to generate a new access token. Just pass your API secret Key in `X-Api-Secret-Key` header to generate access token. The `access_token` is required to access all SSI APIs. Read the next section for more details.&#x20;

{% hint style="info" %}
Entity Studio SSI API base URL: [https://api.entity.dashboard.hypersign.id/](https://api.entity.dashboard.hypersign.id/)
{% endhint %}

{% swagger src="../../.gitbook/assets/api-json.json" path="/api/v1/app/oauth" method="post" %}
[api-json.json](../../.gitbook/assets/api-json.json)
{% endswagger %}

Once you generated the `access_token`, you can pass this token as _<mark style="background-color:yellow;">bearer authorization token</mark>_ in the header for all APIs.&#x20;

