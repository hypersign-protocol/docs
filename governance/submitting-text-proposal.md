# Submitting Text Proposal

> In Progress

## Proposal Structure

| Field | Description |
| :--------------: | :----: |
|   **title**   |  Title of the proposal |
|   **description**  |  Description of the proposal |
|   **type**      | Proposal type. That value would be `text` |
|   **deposit**      | Deposit for the proposal (in `uhid`) |

## CLI

Run the following to submit text proposal:

```
hid-noded tx gov submit-proposal --title "" --description "Lorem" --type text --deposit 10000001uhid  --broadcast-mode block --chain-id hidnode --from node1 --keyring-backend test -y
```

