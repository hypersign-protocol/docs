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

### Configure the Full Node

* Initialise the node with a moniker name.

```
hid-noded init <moniker-name> --chain-id jagrat
```

Configuration files of the node are stored in the default location: `$HOME/.hid-node`. If you want to specify a different location, append the flag `--home <hid-node-home-directory>` to the above command.

* Replace `genesis.json` present in `<hid-node-home-directory>/config` with the Testnet genesis [here](https://github.com/hypersign-protocol/networks/blob/master/testnet/jagrat/final_genesis.json).
* Copy the final peers from [here](https://github.com/hypersign-protocol/networks/blob/master/testnet/jagrat/final_peers.txt). Open `<hid-node-home-directory>/config/config.toml` and the add the peers in the field `persistent_peers`.
* Set the `minimum-gas-price` in `<hid-node-home-directory>/config/app.toml` to `0.02uhid`.

### Set-up Full Node
> Cosmovisor is a tool which will enable automatic upgrade of a blockchain, once a software upgrade governance proposal is passed. More information on Cosmovisor here.

* Download and Install Cosmovisor

```
wget https://github.com/cosmos/cosmos-sdk/releases/download/cosmovisor%2Fv1.2.0/cosmovisor-v1.2.0-linux-amd64.tar.gz && tar -C /usr/local/bin/ -xzf cosmovisor-v1.2.0-linux-amd64.tar.gz
```

* Export the following environment variables which are needed by `cosmovisor`

```
export DAEMON_NAME=hid-noded
export DAEMON_PATH=$(which hid-noded)
export DAEMON_HOME=<Blockchain Config Path Directory>/.hid-node  # Example: $HOME/.hid-node
```

* Create a `cosmovisor` and copy the existing blockchain binary to the following location

```
mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
cp $DAEMON_PATH $DAEMON_HOME/cosmovisor/genesis/bin
```

### Run Full Node

You can run cosmovisor in either of the following ways:

**Standalone**

* Start node using Cosmovisor

```
cosmovisor run start
```
> Note: `cosmovisor` looks for the environment variable `DAEMON_NAME` and `DAEMON_HOME`. Make sure to run the above command in the same terminal window where the said environment variables are set.

**As a system service**

- Change directory: `cd /etc/systemd/system`
- Add the [Cosmovisor system service file](https://github.com/hypersign-protocol/hid-node/blob/main/contrib/hidnoded-cosmovisor.service) to `/etc/systemd/system` directory.
- Open the system service file and make necessary changes in line 7, in case your `hid-node` config path is different.
- Reload service files: `sudo systemctl daemon-reload`
- To enable your service on every reboot: `sudo systemctl enable hidnoded-cosmovisor.service`
- To start the service: `sudo systemctl start hidnoded-cosmovisor.service`
- To check the status of service: `sudo systemctl status hidnoded-cosmovisor.service`
- To restart the service: `sudo systemctl restart hidnoded-cosmovisor.service`

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

### Redeem Stake Rewards

Having significant stake in the blockchain comes with reward in the form of tokens. The redemption of rewards needs to be done manually. Run the following to redeem rewards:

```
hid-noded tx distribution withdraw-rewards <validator-addr> --from <validator-wallet-address>
```
- `<validator-addr>` - Validator's Operator address. (Prefix is `hidvaloper`)
- `<validator-wallet-address>` - Validator's wallet address from which they have stake tokens. (Prefix `hid`)

If you also want to withdraw validator commission, append the `--commission` flag to the above command.

To check the outstanding validator rewards.

```
hid-noded q distribution validator-outstanding-rewards <validator-addr>
```
- `<validator-addr>` - Validator's Operator address. (Prefix is `hidvaloper`)
