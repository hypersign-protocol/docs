# Development

You may have noticed that by default, our KYC service was created in "**dev**" - Development mode.&#x20;

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

In "**dev**" mode following verifications are not performed by AI models integrated in the KYC service:&#x20;

1. Facial Authentication is not performed&#x20;
2. Uniqueness check is also not performed&#x20;
3. Document verification is also not performed&#x20;

Only data is captured and extracted from ID document. We suggest you to complete [full integration](../../kyc-widget/integrations/), test a couple of times and then go for production.&#x20;

{% content-ref url="production.md" %}
[production.md](production.md)
{% endcontent-ref %}
