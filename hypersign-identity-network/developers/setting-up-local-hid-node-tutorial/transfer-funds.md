# Transfer funds

{% hint style="info" %}
Make sure you are running hid network in your local machine before proceeding with this document.&#x20;
{% endhint %}

{% content-ref url="running-a-localnet.md" %}
[running-a-localnet.md](running-a-localnet.md)
{% endcontent-ref %}

When you run the hid-node, a validator account get setup and it keep getting reward. So, lets first find out that account and use that account as a source account or sender account.&#x20;

List all accounts.

```bash
➜  ~ hid-noded keys list --keyring-backend test
- name: my-account1
  type: local
  address: hid1kdql8dwr2njma3g6fyfr9tavw20l84w45wpgaq
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A7Hk/VV1J2l+VEh10DUxtemzR3y5UB8bwXt0DGg79BsE"}'
  mnemonic: ""
- name: node1
  type: local
  address: hid1qm40ngul9h0hrm4kjxdjktfekhvk4t0jjk7vft
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"AqVU3YfzrOUIMpJEacdJMPDn34g0HxqrsmrG55r8dwVX"}'
  mnemonic: ""
```

`node1` is the first account which has balance and be used as a sender of the the transaction.&#x20;

### Send amount from one account to other

Create a new account called `my-account1`and lets send balance from account `node1` to `my-account1` and then finnally check balances.

```bash
hid-noded tx bank send <source-addr> <destination-addr> <amount> --keyring-backend test --chain-id hidnode
```

* **source-addr**: senders account address
* **destination-addr**: receiver account address
* **amount:** amount in uhid. This value must be suffix with text _'uhid'._

{% hint style="info" %}
1 hid = 10^6 uhid
{% endhint %}

Example:

```bash
➜  ~ hid-noded tx bank send hid1qm40ngul9h0hrm4kjxdjktfekhvk4t0jjk7vft hid1kdql8dwr2njma3g6fyfr9tavw20l84w45wpgaq 100000000uhid --keyring-backend test --chain-id hidnode
{"body":{"messages":[{"@type":"/cosmos.bank.v1beta1.MsgSend","from_address":"hid1qm40ngul9h0hrm4kjxdjktfekhvk4t0jjk7vft","to_address":"hid1kdql8dwr2njma3g6fyfr9tavw20l84w45wpgaq","amount":[{"denom":"uhid","amount":"100000000"}]}],"memo":"","timeout_height":"0","extension_options":[],"non_critical_extension_options":[]},"auth_info":{"signer_infos":[],"fee":{"amount":[],"gas_limit":"200000","payer":"","granter":""}},"signatures":[]}

confirm transaction before signing and broadcasting [y/N]: y
code: 0
codespace: ""
data: ""
events: []
gas_used: "0"
gas_wanted: "0"
height: "0"
info: ""
logs: []
raw_log: '[]'
timestamp: ""
tx: null
txhash: 94F01A41D22E44ABD2D44B553D428B5D1C5AE10078F5E01BD3AA446AD2EC9A71
```

Now you can check the balance of receiver account.&#x20;

```
➜  ~ hid-noded q bank balances hid1kdql8dwr2njma3g6fyfr9tavw20l84w45wpgaq
balances:
- amount: "100000000"
  denom: uhid
pagination:
  next_key: null
  total: "0"
```
