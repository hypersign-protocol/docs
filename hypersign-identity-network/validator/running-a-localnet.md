# Running a Localnet

If you are looking to simulate a single-node blockchain on a local environment, following are the steps

* Clone the hid-node repo&#x20;

```
git clone https://github.com/hypersign-protocol/hid-node.git
```

* Head over to cloned `hid-node` repo directory

```bash
cd hid-node
```

* Initialize the node config and setup a validator

<pre class="language-bash"><code class="lang-bash"><strong>chmod +x ./scripts/localnet-single-node/setup.sh 
</strong><strong>bash ./scripts/localnet-single-node/setup.sh
</strong></code></pre>

* Run the node

```
hid-noded start
```

* Now, you have a single node blockchain running with `chain-id` as `hidnode` and `chain_namespace` as "`devnet"`.
