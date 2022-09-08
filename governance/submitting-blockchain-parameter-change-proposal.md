# Submitting Blockchain Parameter Change Proposal

> In Progress

## Proposal Structure

This proposal requires information to be passed in JSON file as follows:

```json
{
    "title": "<Proposal Title>",
    "description": "<Description of Proposal>",
    "changes": [
      {
        "subspace": "<Module Name>",
        "key": "<Module's param name in UpperCamelCase>",
        "value": "<Proposed value>"
      }
    ],
    "deposit": "<Deposit (in uhid) for the proposal>"
}
```

Example:

```json
{
    "title": "Change in Validator Node Downtime Penalty",
    "description": "This proposal brings about change in the validator node downtime penalty to 0.365",
    "changes": [
      {
        "subspace": "slashing",
        "key": "SlashFractionDowntime",
        "value": "0.365000000000000000"
      }
    ],
    "deposit": "50000000uhid"
}
```

## CLI

* Run the following to submit a blockchain parameter change proposal:

```
hid-noded tx gov submit-proposal param-change "<path-of-proposal-json-file>" --from <key-name> --yes
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
