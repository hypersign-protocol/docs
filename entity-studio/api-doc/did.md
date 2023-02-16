---
description: Manage DID operation using DID APIs
---

# DID

Please [generate access token](authentication.md) before proceeding.  Once you generated the `access_token`, you can pass this token as bearer authorization token in the header for all APIs.&#x20;

### Create a DID

{% swagger src="../../.gitbook/assets/entity-api-json.json" path="/api/v1/did" method="post" %}
[entity-api-json.json](../../.gitbook/assets/entity-api-json.json)
{% endswagger %}

### Resolve a DID

{% swagger src="../../.gitbook/assets/entity-api-json.json" path="/api/v1/did/{did}" method="get" %}
[entity-api-json.json](../../.gitbook/assets/entity-api-json.json)
{% endswagger %}

### Fetch all DIDs for your apps

{% swagger src="../../.gitbook/assets/entity-api-json.json" path="/api/v1/did" method="get" %}
[entity-api-json.json](../../.gitbook/assets/entity-api-json.json)
{% endswagger %}

### Update a DID

{% swagger src="../../.gitbook/assets/entity-api-json.json" path="/api/v1/did" method="patch" %}
[entity-api-json.json](../../.gitbook/assets/entity-api-json.json)
{% endswagger %}

###
