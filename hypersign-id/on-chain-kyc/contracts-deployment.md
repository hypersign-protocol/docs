# Contracts Deployment

Please read [introduction](./#introduction) before proceeding with the contract deployments on this page. &#x20;

Head over to Entity Studio dashboard, choose your KYC service and click on **OnChain KYC**  under setting tab in left nav bar.&#x20;

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Click on **Deploy OnChain KYC** button to start the process of contract deployments.&#x20;

### Deploy Hypersign KYC Issuer Contract

Step 1 is to deploy your KYC Issuer contract through the right slider window. Select blockchain of your choice then select a DID which you want to associate with this contract.  Finally, connect your wallet and click on "**Deploy KYC Contract**" button.&#x20;

{% hint style="info" %}
If you do not have any DID yet, kindly refer to [this](../../hypersign-ssi/setup-ssi-service/create-your-first-did.md) documentation.
{% endhint %}

{% content-ref url="supported-blockchains.md" %}
[supported-blockchains.md](supported-blockchains.md)
{% endcontent-ref %}

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

You need to authorise the transaction to instantiate your KYC issuer contract through wallet. If everything works, you will see your KYC contract address in the slider.&#x20;

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Click on "**Next**" button to deploy your KYC token contract in the next step.

### Deploy Hypersign KYC Token Contract (SBT)

Same as before, authorize the transaction through your wallet to deploy your brand new KYC token contract.&#x20;

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Once the transaction is successfull, you will see KYC token contract address in the slider.&#x20;

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

And your configuration is completed. Please note the configuration ID (2nd column) in the configuration record, we would need to set this configuration ID in the widget configuration.&#x20;

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

Now that we have deployed our contracts, let's go ahead and enable this [on chain kyc configuration](../integrations/widget-configuration.md#on-chain-kyc) in the widget setting page:&#x20;

{% content-ref url="../integrations/widget-configuration.md" %}
[widget-configuration.md](../integrations/widget-configuration.md)
{% endcontent-ref %}
