# Running a Testnet Validator Node

### Hardware Requirements

* **Minimal**
  * 4 GB RAM
  * 250 GB SSD Storage
  * 1.4 GHz x2 CPU
* **Recommended**
  * 8 GB RAM
  * 500 GB SSD Storage
  * 2.0 GHx x4 CPU

### Prerequisites

* Golang 1.18+ required. ([Installation Ref](https://go.dev/doc/install))
* git [Installation Ref](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* make [Installation Ref](https://linuxhint.com/install-make-ubuntu/)

### Installation

{% content-ref url="roadmap.md" %}
[roadmap.md](roadmap.md)
{% endcontent-ref %}

### Generate Wallet

* Run the following to generate a wallet. Save the mnemonic displayed on the output, which can be used for scenarios where you would like to import your wallet address.

```
hid-noded keys add <key-name>
```

* If you already have a [BIP39](https://github.com/bitcoin/bips/tree/master/bip-0039) mnemonic, you can import your wallet by running the following. Enter the mnemonic string in the prompt and the wallet will be imported.

```
hid-noded keys add <key-name> --recover
```

### Configure and Run the Full Node

* Initialise the node with a moniker name.

```
hid-noded init <moniker-name> --chain-id jagrat
```

Configuration files of the node are stored in the default location: `$HOME/.hid-node`. If you want to specify a different location, append the flag `--home <hid-node-home-directory>` to the above command.

* Replace `genesis.json` present in `<hid-node-home-directory>/config` with the Testnet genesis [here](https://github.com/hypersign-protocol/launch/blob/main/testnet/jagrat/final\_genesis.json).
* Copy the final peers from [here](https://github.com/hypersign-protocol/launch/blob/main/testnet/jagrat/final\_peers.txt). Open `<hid-node-home-directory>/config/config.toml` and the add the peers in the field `persistent_peers`.
* Set the `minimum-gas-price` in `<hid-node-home-directory>/config/app.toml`.
* Run the node

```
hid-noded start --home <hid-node-home-directory>
```

* In a separate terminal window, check if the node is running.

```
hid-noded status
```

### Promotion of Full Node to Validator Node

* Acquire some **$HID** tokens. (TODO: Mention the approach to acquire tokens: faucet or Discord group)
* Perform a validator creation transaction.

```
hid-noded tx staking create-validator \
--from <key-name> \
--amount 1000000000000uhid \
--pubkey "$(hid-noded tendermint show-validator)" \
--chain-id jagrat \
--moniker="<validator-name>" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.07 \
--min-self-delegation="500000000000" \
--details="XXXXXXXX" \
--security-contact="XXXXXXXX" \
--website="XXXXXXXX"
```