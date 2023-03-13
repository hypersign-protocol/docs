# Create and fund new account

### Check if hid-node binary is installed in your machine

Switch to a new terminal and type `hid-noded` command to check if hid node is installed in your machine or not.

```bash
➜  ~ hid-noded
Hypersign Identity Network (hid-noded) CLI

Usage:
  hid-noded [command]

Available Commands:
  add-genesis-account Add a genesis account to genesis.json
  collect-gentxs      Collect genesis txs and output a genesis.json file
  configure           Adjust node parameters
  debug               Tool for helping with debugging your application
  gentx               Generate a genesis tx carrying a self delegation
  ...
  ...
Flags:
  -h, --help                help for hid-noded
      --home string         directory for config and data (default "/Users/hermit/.hid-node")
      --log_format string   The logging format (json|plain) (default "plain")
      --log_level string    The logging level (trace|debug|info|warn|error|fatal|panic) (default "info")
      --trace               print out full stack trace on errors.
Use "hid-noded [command] --help" for more information about a command.
  export              Export state to JSON
```

{% hint style="info" %}
Make sure you are running hid network in your local machine before proceeding with this document.&#x20;
{% endhint %}

{% content-ref url="running-a-localnet.md" %}
[running-a-localnet.md](running-a-localnet.md)
{% endcontent-ref %}

### Create a new account

Type the following command to create a new account.

```bash
hid-noded keys add <account-name> --keyring-backend test
```

* **account-name :** Provide an alias for your new account

The command will spit out a new wallet address along with its mnemonics. This command also stores key material for this account locally in your computer which you can refer this using the `account-name` alias that you provided.&#x20;

Example:

```bash
➜  ~ hid-noded keys add my-account1 --keyring-backend test

- name: my-account1
  type: local
  address: hid1ysq78a7qypxmf5wdcnvn2sz7sswg9guh8vfxcr
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"Az3UboQVFxJtR8kGmrr7woZDiouB4uDcU7jIQpSiMJRB"}'
  mnemonic: ""


**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

know leisure elegant entry recycle crop already merry virus width slide bike model pupil sword cupboard flat spoon stool rebuild art float aisle gown
```

### Check balance

```bash
hid-noded q bank balances <address>
```

Example:

```bash
➜  ~ hid-noded q bank balances hid1qm40ngul9h0hrm4kjxdjktfekhvk4t0jjk7vft
balances:
- amount: "449999999999965859"
  denom: uhid
pagination:
  next_key: null
  total: "0"
```

### List all accounts&#x20;

Run the following command to list down all account stored in your hid node.&#x20;

```bash
hid-noded keys list --keyring-backend test
```

Example:

```bash
➜  ~ hid-noded keys list --keyring-backend test
- name: my-account1
  type: local
  address: hid1ysq78a7qypxmf5wdcnvn2sz7sswg9guh8vfxcr
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"Az3UboQVFxJtR8kGmrr7woZDiouB4uDcU7jIQpSiMJRB"}'
  mnemonic: ""
- name: node1
  type: local
  address: hid1qm40ngul9h0hrm4kjxdjktfekhvk4t0jjk7vft
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"AqVU3YfzrOUIMpJEacdJMPDn34g0HxqrsmrG55r8dwVX"}'
  mnemonic: ""
```

### Delete an account

You can use the following command to delete an account from your hid-node.&#x20;

```bash
hid-noded keys delete <account-name> --keyring-backend test
```

Example:

```bash
➜  ~ hid-noded keys delete my-account1 --keyring-backend test
Key reference will be deleted. Continue? [y/N]: y
Key deleted forever (uh oh!)
```
