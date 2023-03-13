# Network Fee

Every application is associate with a wallet address (account address on Hypersign Blockchain) and the private key for that wallet address is managed by Entity Studio API server for the application via an encrypted data vault (read security section for more details).&#x20;

Since many SSI APIs are on-chain activities, `$hid` token is required to pay for transaction fee for those on-chain activities.&#x20;

### Application Wallet

Go to the developer dashboard and click on **Edit** icon of your application's card.  Right slider will be opened where you can see details of your wallet.&#x20;

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption><p>Wallet created for the application</p></figcaption></figure>

{% hint style="info" %}
Initially balance of this wallet is 0, all on-chain API requests will fail.  You can request hid testnet tokens from our Faucet
{% endhint %}

{% content-ref url="../../hypersign-identity-network/faucet-testnet.md" %}
[faucet-testnet.md](../../hypersign-identity-network/faucet-testnet.md)
{% endcontent-ref %}
