# Blockchain Node Upgrade

## Proposal Structure

|        Field       |                 Description                |
| :----------------: | :----------------------------------------: |
|      **name**      |             Name of the Upgrade            |
|      **title**     |            Title of the proposal           |
|   **description**  |         Description of the proposal        |
| **upgrade-height** | Height at which node upgrade should happen |
|     **deposit**    |    Deposit for the proposal (in `uhid`)    |

## Submitting Node Upgrade Proposal

* Run the following to submit a blockchain node upgrade proposal:

```
hid-noded tx gov submit-proposal software-upgrade <Proposal Name> \
--title "<Proposal Title>" \
--description "<Proposal Description>" \
--upgrade-height "<Blockchain Height at which the upgrade should occur>" \
--deposit "<Deposit for the proposal>" \
--chain-id <Chain ID> \
--from <wallet-address> \
--yes
```

## Steps for Node Upgrade

If the Software Upgrade proposal is `Passed`, then following steps are needed to be performed in order to upgrade your node.

* Download and Install the **latest** binary.
* Create the following directory structure

```
mkdir -p <hid-node Config Directory>/cosmovisor/upgrades/<Proposal Name>/bin
```

> Note: Make sure that `<Proposal Name>` matches exactly with Upgrade Proposal's name. Please note that `Proposal Name` is different from `Proposal Title`.

* Copy the latest binary to the newly created directory

```
cp <Update Binary Location> <Binary Config Directory>/cosmovisor/upgrades/<Proposal Name>/bin
```

* At the the proposed height, the upgrade would take place automatically.
