---
description: Instructions to install hid-node binary
---

# Installation of Node

### Building from Source

* Clone the Github repository.

```bash
git clone https://github.com/hypersign-protocol/hid-node.git
```

* Checkout the tag and build the node. Look [here](https://github.com/hypersign-protocol/hid-node/tags) for a list of tags.

```bash
cd hid-node
git checkout v0.1.2 #v0.1.2 is the current testnet binary
make install
```

* Run the following to ensure that node binary is installed.

```bash
hid-noded version
```

### Download the binary

* Export the environment variables according to your Operating System and Architecture, and install the binary

<pre class="language-bash"><code class="lang-bash">export OS=&#x3C;operating-system>
<strong>export ARCH=&#x3C;system-architecture>
</strong>
<strong># Get the list of tags: https://github.com/hypersign-protocol/hid-node/tags
</strong># Exclude the `v` prefix while entering
<strong>export TAG=0.1.2  # Latest Testnet Tag
</strong>
<strong># Download the binary
</strong>wget https://github.com/hypersign-protocol/hid-node/releases/download/v${TAG}/hid-noded-${TAG}-${OS}-${ARCH}.tar.gz
</code></pre>

Refer the following table to obtain the environment variables for your system configuration.

| Operating System |   OS   |  ARCH |
| :--------------: | :----: | :---: |
|   Linux 64-bit   |  linux | amd64 |
|    Linux ARMv7   |  linux | arm64 |
|      Darwin      | darwin | arm64 |
