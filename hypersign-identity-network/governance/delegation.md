# Delegation

Users can stake their `$HID` tokens with Validators to earn incentives. Having stake in the network enables them to participate and vote on governance proposals. It is **highly recommended** to research about the background of a Validator before staking. If a validator happens to get slashed, delegated tokens are subject to slashing as well 

## Staking HID

Run the following command to stake `$HID` tokens on a validator

```
hid-noded tx staking delegate <Validator's Operator Address> <Amount to Stake in 'uhid'> --from <your wallet address> --chain-id <Chain ID of the network>
```

**Note**: Validator's Operator Address will have the prefix `hidvaloper`

## Withdraw Stake Rewards

To withdraw staked rewards earned through staking on a validator

```
hid-noded tx distribution withdraw-rewards <Validator's Operator Address> --from <your wallet address> --chain-id <Chain ID of the network>
```

**Note**: Partial reward withdrawal is not supported

## Stake Redelegation 

You can transfer partial/complete stake from one validator to another. To do this, run the following

```
hid-noded tx staking redelegate <Source Validator's Operator Address> <Destination Validator's Operator Address> <Amount of stake to be redelegated in 'uhid'> --from <your wallet address> --chain-id <Chain ID of the network>
```

## Unbond Stake

If you want to remove partial/complete stake from a validator, run the following:

```
hid-noded tx staking unbond <Validator's Operator Address> <Amount of tokens to unbond in 'uhid'> --from <your wallet address> --chain-id <Chain ID of the network>
```

**Note**: Unlike Stake Redelegation, it takes 7 days for tokens to move back in the wallet. 