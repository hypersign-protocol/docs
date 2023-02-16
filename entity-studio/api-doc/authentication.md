---
description: Generate access token using API secret Key
---

# Authentication

Register your application on [Entity Studio Developer Dashboard](../developer-dashboard.md) and generate your API secret Key before proceeding.&#x20;

Once the API secret key is generated, you can use the API below to generate a new access token. Just pass the appId and API secret Key in the body to generate access token. The `access_token` is required to access all SSI APIs. Read the next section for more details.&#x20;

{% swagger src="../../.gitbook/assets/entity-api-json.json" path="/api/v1/app/oauth" method="post" %}
[entity-api-json.json](../../.gitbook/assets/entity-api-json.json)
{% endswagger %}

