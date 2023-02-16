# Submitting Text Proposal

## Proposal Structure

|      Field      |                Description                |
| :-------------: | :---------------------------------------: |
|    **title**    |           Title of the proposal           |
| **description** |        Description of the proposal        |
|     **type**    | Proposal type. That value would be `text` |
|   **deposit**   |          Deposit for the proposal         |

## CLI

* Run the following to submit a text proposal:

```
hid-noded tx gov submit-proposal --title "Proposal-title-1" --description "Lorem" --type text --deposit 10000001uhid  --broadcast-mode block --chain-id hidnode --from node1 --keyring-backend test -y
```
