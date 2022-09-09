# Submitting Community Pool Spend Proposal

## Proposal Structure

This proposal requires information to be passed in a JSON file as follows:

```json
{
  "title": "<Proposal Title>",
  "description": "<Description of Proposal>",
  "recipient": "<Grant Recipient's Blockchain Address>",
  "amount": "<Grant Amount>",
  "deposit": "<Deposit for proposal>"
}
```

Example:

```json
{
  "title": "Grant: Community Spend Proposal",
  "description": "Community Spend Proposal",
  "recipient": "hid10vxwt3k9hdtp38q9x27zlpe4fhq7fwqe3xc226",
  "amount": "10000000000uhid",
  "deposit": "100000000uhid"
}
```

## CLI

* Run the following to submit a community pool spend proposal:

```
hid-noded tx gov submit-proposal community-pool-spend "<path-to-proposal-json-file>" --from <key-name> --yes
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