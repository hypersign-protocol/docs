---
description: Instructions to install hid-node binary
---

# Installation of Node

### Building from Source

* Clone the Github repository.

```bash
git clone https://github.com/hypersign-protocol/hid-node.git
```

* Checkout the tag that the network is currently running on and build the node.

```bash
cd hid-node
git checkout v0.2.0
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
</strong><strong>export TAG=0.2.0
</strong>
<strong># Download the binary
</strong>wget https://github.com/hypersign-protocol/hid-node/releases/download/v${TAG}/hid-noded-${TAG}-${OS}-${ARCH}.tar.gz
</code></pre>

Refer the following table to obtain the environment variables for your system configuration.

| Operating System |   OS   |  ARCH |
| :--------------: | :----: | :---: |
|   Linux 64-bit   |  linux | amd64 |
|    Linux ARMv7   |  linux | arm64 |
|       MacOS      | darwin | amd64 |
