# Running a Testnet Validator Node

### Hardware Requirements

* **Minimal**
  * 16 GB RAM
  * 300 GB SSD Storage
  * 1.4 GHz x2 CPU
* **Recommended**
  * 32 GB RAM
  * 600 GB SSD Storage
  * 2.0 GHx x4 CPU

### Prerequisites

* Golang 1.21 required. ([Installation Ref](https://go.dev/doc/install))
* git [Installation Ref](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* make [Installation Ref](https://linuxhint.com/install-make-ubuntu/)

### Installation

{% content-ref url="installation-of-node.md" %}
[installation-of-node.md](installation-of-node.md)
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

### Configure the Full Node

* Initialise the node with a moniker name.

```
hid-noded init <moniker-name> --chain-id prajna-1
```

Configuration files of the node are stored in the default location: `$HOME/.hid-node`. If you want to specify a different location, append the flag `--home <hid-node-home-directory>` to the above command. In this case, for every transaction based commands, you have to explicitly pass this flag.

* Replace `genesis.json` present in `<hid-node-home-directory>/config` with the Testnet genesis [here](https://github.com/hypersign-protocol/networks/blob/master/testnet/prajna/final\_genesis.json).
* Copy the final peers from [here](https://github.com/hypersign-protocol/networks/blob/master/testnet/prajna/final\_peers.txt). Open `<hid-node-home-directory>/config/config.toml` and the add the peers in the field `persistent_peers`.

### Run Full Node

`hid-noded` binary can be run in either of the following ways:

* In Terminal

```
hid-noded start
```

* As a system service
  * Change directory: `cd /etc/systemd/system`
  * Add the [hid-noded system service file](https://github.com/hypersign-protocol/hid-node/blob/main/contrib/hidnoded-standalone.service) to `/etc/systemd/system` directory.
  * Reload service files: `sudo systemctl daemon-reload`
  * To make sure your service starts on every reboot (Optional): `sudo systemctl enable hidnoded-standalone.service`
  * To start the service: `sudo systemctl start hidnoded-standalone.service`
  * To check the status of service: `sudo systemctl status hidnoded-standalone.service`
  * To restart the service: `sudo systemctl restart hidnoded-standalone.service`

### Important Points

If you haven't run any CometBFT based chains before, please note the following points before moving to the upcoming sections below:-

* RPC and gRPC ports can be modified in `<blockchain-config-dir>/config/config.toml`
* API port can be modified in `<blockchain-config-dir>/config/app.toml`
* There are primarily two types of commands:
  * Transaction based. It starts with `hid-noded tx ...`
  * Query based. It starts with `hid-noded q ...`
* Transaction based commands may/always require the following flags:
  * `--chain-id prajna-1`
  * `--fees 4000uhid`: The value of fees is arbitrary, but it should be sufficiently high enough for the transaction to go through. `4000uhid` is an appropriate value for almost every transaction
  * `--node <rpc-ip-or-dns:rpc-port>`: The node expects RPC to run on default port 26657. If your RPC port is different from default, you need to explicitly pass this flag. In case of default port, it can be skipped.
* Query based commands may require the following flag:
  * `--node <rpc-ip-or-dns:rpc-port>`: The node expects RPC to run on default port 26657. If your RPC port is different from default, you need to explicitly pass this flag. In case of default port, it can be skipped.
* Learn more about Cosmos SDK's modules and their respective commands from [here](https://docs.cosmos.network/v0.47/build/modules)

### Promotion of Full Node to Validator Node

* Perform these steps only when your node is completely **synced** with the testnet.
* Acquire some **$HID** tokens. Use the faucet channel of Hypersign Protocol's Discord Server from [here](https://discord.com/channels/777575858075861033/1186968387860049920)
* Perform the following validator creation transaction.

```
hid-noded tx staking create-validator \
--from <key-name> \
--amount 1000000uhid \
--pubkey "$(hid-noded comet show-validator)" \
--chain-id prajna-1 \
--moniker="<validator-name>" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.07 \
--min-self-delegation="1000000" \
--details="<enter details about your validator node or validation service>" \
--security-contact="<contain details>" \
--website="<your website>"
--fees="<Transaction fees in uhid. Example: 4000uhid>"
```

### Redeeming Staked Rewards

Having significant stake in the blockchain comes with reward in the form of tokens. The redemption of rewards needs to be done manually. Run the following to redeem rewards:

```
hid-noded tx distribution withdraw-rewards <validator-addr> --from <validator-wallet-address> --chain-id jagrat --fees <Transaction fees in uhid. Example: 4000uhid>
```

* `<validator-addr>` - Validator's Operator address. (Prefix is `hidvaloper`)
* `<validator-wallet-address>` - Validator's wallet address from which they have stake tokens. (Prefix `hid`)

If you also want to withdraw validator commission, append the `--commission` flag to the above command.

To check the outstanding validator rewards.

```
hid-noded q distribution validator-outstanding-rewards <validator-addr>
```

* `<validator-addr>` - Validator's Operator address. (Prefix is `hidvaloper`)

### Unjailing a validator node

In CometBFT-based blockchain, if a node is not active for a certain period of time or if the current self stake falls below the minimum self stake, it is temporarily moved out of the validator set. This situation is called Jailing of a validator. The validator remains in the jailed period for about 10 minutes.

The validator can only be unjailed manually through a transaction after the jailed period is over and if the current self stake is above the required self stake at the time the time of performing the following unjail transaction:

```
hid-noded tx slashing unjail --from <validator-associated-wallet-address> --chain-id jagrat --fees <amount-in-uhid>
```
