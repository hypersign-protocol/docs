# Submitting Text Proposal

> In Progress

## Proposal Structure

| Field | Description |
| :--------------: | :----: |
|   **title**   |  Title of the proposal |
|   **description**  |  Description of the proposal |
|   **type**      | Proposal type. That value would be `text` |
|   **deposit**      | Deposit for the proposal |

## CLI

* Run the following to submit a text proposal:

```
hid-noded tx gov submit-proposal --title "" --description "Lorem" --type text --deposit 10000001uhid  --broadcast-mode block --chain-id hidnode --from node1 --keyring-backend test -y
```

* Query the list of proposals

```
hid-noded q gov proposals
```

Proposal IDs start with `1`, which means that the first proposal submitted on chain, would have the proposal ID, and subsequent proposals will have their ID incremented by `1`.

* Run the following to vote on the proposal

```
hid-noded tx gov vote <Proposal ID> <Vote=(yes|no|abstain|no_with_veto)> \
--from <wallet-address> \
--chain-id <Chain ID>
```

* You can check the status of the proposal

```
hid-noded q gov proposal <Proposal ID>
```
