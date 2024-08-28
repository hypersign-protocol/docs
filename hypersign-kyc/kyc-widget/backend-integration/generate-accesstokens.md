# Generate AccessTokens

You must have SSI service secret key and KYC service secret key with you before proceeding to this step.&#x20;

In order to use APIs of your services, you need `accessToken` generated using your API secret keys. Generate accessToken by calling service authentication APIs using API secret keys. You might want to **implement an API** in your backend which will call **Service Authentication API** to generate accessTokens for SSI and KYC service, so that your API secrets are not exposed in your frontend or anywhere else.

Let's call these accessToken as `kycAccessToken` and `ssiAccessToken` for KYC service and SSI service respectively.

{% content-ref url="../../../hypersign-ssi/api-doc/authentication.md" %}
[authentication.md](../../../hypersign-ssi/api-doc/authentication.md)
{% endcontent-ref %}

Once you have both `kycAccessToken` as well as `ssiAccessToken`you may now proceed to frontend integration of the KYC widget.

{% content-ref url="../frontend-integration/" %}
[frontend-integration](../frontend-integration/)
{% endcontent-ref %}
