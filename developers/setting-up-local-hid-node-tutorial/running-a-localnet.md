# Running one-node local hid network

If you are looking to simulate a single-node blockchain on a local environment, following are the steps

{% tabs %}
{% tab title="Linux" %}
#### Download hid-node binary compressed file&#x20;

```
wget https://github.com/hypersign-protocol/hid-node/releases/download/v0.1.7/hid-noded-0.1.7-linux-amd64.tar.gz
```

#### Extract the binary&#x20;

```bash
tar -xvzf hid-noded-0.1.7-linux-amd64.tar.gz
```

#### Move the hid-node binary to /usr/local/bin

<pre class="language-bash"><code class="lang-bash"><strong>sudo mv hid-noded-0.1.7-linux-amd64/hid-noded /usr/local/bin
</strong></code></pre>

#### Check the version

```bash
hid-noded version
```

#### Download and run the one-node network setup script

```bash
wget https://raw.githubusercontent.com/hypersign-protocol/hid-node/main/localnetsetup.sh && bash localnetsetup.sh
```

This script will setup validators and its cryptographic keys. It will also fund token in your genesis account.&#x20;

#### Finally Run the one-node network

```bash
hid-noded start
```

```bash
➜  /tmp hid-noded start
7:54PM INF starting node with ABCI Tendermint in-process
7:54PM INF service start impl=multiAppConn module=proxy msg={}
7:54PM INF service start connection=query impl=localClient module=abci-client msg={}
7:54PM INF service start connection=snapshot impl=localClient module=abci-client msg={}
7:54PM INF service start connection=mempool impl=localClient module=abci-client msg={}
7:54PM INF service start connection=consensus impl=localClient module=abci-client msg={}
7:54PM INF service start impl=EventBus module=events msg={}
7:54PM INF service start impl=PubSub module=pubsub msg={}
7:54PM INF service start impl=IndexerService module=txindex msg={}
```


{% endtab %}

{% tab title="Mac Os" %}
#### Download hid-node binary compressed file&#x20;

```bash
wget https://github.com/hypersign-protocol/hid-node/releases/download/v0.1.7/hid-noded-0.1.7-darwin-arm64.tar.gz
```

#### Extract the binary&#x20;

```bash
tar -xvzf hid-noded-0.1.7-darwin-arm64.tar.gz
```

#### Move the hid-node binary to /usr/local/bin

```bash
sudo mv hid-noded-0.1.7-darwin-arm64/hid-noded /usr/local/bin
```

#### Check the version

```bash
hid-noded version
```

#### Download and run the one-node network setup script

```bash
wget https://raw.githubusercontent.com/hypersign-protocol/hid-node/main/localnetsetup.sh && bash localnetsetup.sh
```

This script will setup validators and its cryptographic keys. It will also fund token in your genesis account.&#x20;

#### Finally Run the one-node network

```bash
hid-noded start
```
{% endtab %}
{% endtabs %}



