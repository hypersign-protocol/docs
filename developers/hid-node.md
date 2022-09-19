# HID Node

> In Progress

Hypersign Identity Network (HID Node) is built on top of Cosmos SDK. This documentation only covers the SSI module and the basic commands of Cosmos SDK modules. It is recommended to have a good understanding of Cosmos SDK. Please refer Cosmos SDK docs [here](https://docs.cosmos.network/v0.45/).

The knowledge of Protocol Buffers is also essential.

# Project Structure

Following is the high level folder structure of HID Node

```
├── app
├── cmd
├── docs
├── proto
│   └── ssi
│       └── v1
│           ├── credential.proto
│           ├── did.proto
│           ├── genesis.proto
│           ├── query.proto
│           ├── schema.proto
│           └── tx.proto
├── scripts
├── tests
├── testutil
├── third_party
│   └── proto
│       ├── gogoproto
│       │   └── gogo.proto
│       └── google
│           └── protobuf
│               └── descriptor.proto
└── x
    └── ssi
        ├── abci.go
        ├── client
        │   └── cli
        │       ├── query.go
        │       ├── query_ssi.go
        │       ├── tx.go
        │       ├── tx_ssi.go
        │       └── tx_utils.go
        ├── genesis.go
        ├── genesis_test.go
        ├── handler.go
        ├── keeper
        │   ├── credential.go
        │   ├── did.go
        │   ├── document_verification
        │   │   ├── common_checks.go
        │   │   ├── credential_verification.go
        │   │   ├── did_verification.go
        │   │   └── vars.go
        │   ├── grpc_query_credential.go
        │   ├── grpc_query_did.go
        │   ├── grpc_query.go
        │   ├── grpc_query_schema.go
        │   ├── keeper.go
        │   ├── msg_server_credential.go
        │   ├── msg_server_did.go
        │   ├── msg_server.go
        │   ├── msg_server_schema.go
        │   ├── schema.go
        │   └── signature_verification.go
        ├── module.go
        ├── tests
        ├── types
        └── utils
```

# Protobuf
The interaction between a client and HID Node happens through RPC, built using Protobuf. The proto files are defined under `proto/ssi/v1`. The are two RPC `service` namely `Msg` and `Query`, defined in `proto/ssi/v1/tx.proto` and `proto/ssi/v1/query.proto` respectively. List of HID Node RPCs are:

**Transaction Based**

- MsgCreateDID 
- MsgUpdateDID
- MsgDeactivateDID
- MsgCreateSchema
- MsgRegisterCredentialStatus    

**Query Based**

- QueryDidDocument
- QueryDidDocuments
- QuerySchema
- QuerySchemas
- QueryCredential
- QueryCredentials

The generation of Golang code is done by the script `scripts/protogenc.sh`. The generated files are present in `x/ssi/types`. 

## DID Document

The [DID-Core](https://www.w3.org/TR/did-core/) W3C Specification has been followed to frame the structure of a DID Document. It's proto representation is mentioned in `proto/ssi/v1/did.proto`. The message `DidDocumentState` is stored on chain.

```proto
// proto/ssi/v1/did.proto

message DidDocumentState {
  Did didDocument = 1;
  Metadata didDocumentMetadata = 2;
}
```

## Schema Document

The proto representation is mentioned in `proto/ssi/v1/schema.proto`. The message `Schema` is stored on chain.

```proto
// proto/ssi/v1/schema.proto

message Schema {
    string type = 1;
    string modelVersion = 2;
    string id = 3;
    string name = 4;
    string author = 5;
    string authored = 6;
    SchemaProperty schema = 7;
    SchemaProof proof = 8;
}
```

## Credential Status Document

The proto representation is mentioned in `proto/ssi/v1/credential.proto`. The message `Credential` is stored on chain.

```proto
// proto/ssi/v1/credential.proto

message Credential {
    Claim claim = 1;
    string issuer = 2;
    string issuanceDate = 3;
    string expirationDate = 4;
    string credentialHash = 5;
    CredentialProof proof = 6;
}
```

# `x/ssi` Module

In Cosmos SDK, every operations related to blockchain such as staking, delegation, token trasfer, etc are handled by different modules. They are defined in the `x` directory of Cosmos SDK (See [here](https://github.com/cosmos/cosmos-sdk/tree/main/x)). For instance, `x/bank` module handles the functionality of token transfer. `x/ssi` module lets you store documents such as Decentralised Identifiers (DID), Schema Document and Verifiable credential Status on chain.

**Quick Overview**

`x/ssi/client/cli`: CLI Client for sending SSI-based transactions to and querying data from Blockchain. 

`x/ssi/keeper`: Interaction with the state of blockchain

`x/ssi/genesis.go`: 
    - Initialising and Exporting of genesis variables of `x/ssi` module, such as `chain_namespace`. 
    - For public mainnet chain, `chain_namespace` should be empty. In case of testnet, the name of the testnet should be assigned. If you are running a private network, you can specify your own chain namepsace.

`x/ssi/modules.go`: Defines the interface for `ssi` module

## Keeper

Keepers provides an abstraction to interact with the state of the blockchain. The store is a data structure which persists the state. The `Get` and `Set` methods of the store are handled by the Keeper. There are Keeper functions defined for each of the RPCs. Transaction-based RPCs share a similar workflow, while Query-based share different workflow similarity among themeselves.

**Transaction Based Keepers**

Let's take the example of `MsgCreateDID`

The proto definition of RPC is as follows:

```proto
// proto/ssi/v1/tx.proto

service Msg {
    // ----
    rpc CreateDID(MsgCreateDID) returns (MsgCreateDIDResponse);
    // ---
}

message MsgCreateDID {
  Did didDocString = 1; // from proto/ssi/v1/did.proto
  repeated SignInfo signatures = 2; // from proto/ssi/v1/did.proto
  string creator = 3; // blockchain account address who will be signing the transaction
}

message MsgCreateDIDResponse {
  uint64 id = 1;
}
```

Pseudocode:

```go
// x/ssi/keeper/msg_server_did.go

func (k msgServer) CreateDID(goCtx context.Context, msg *types.MsgCreateDID) (*types.MsgCreateDIDResponse, error) {
    ctx <- unwrap SDK Context from `goCtx`

    // Get the document from `msg`
    didDocument <- get the DID Document from `msg` arg
    signature <- get the signature information from `msg` arg

    // Verfication of Document //
    err = ValidateDidDocumentElements(didDocument)
    if err != nil {
        return nil, err
    }

    err = CheckIfDidDocumentExistsOnChain(didDocument.Id)
    if err != nil {
        return nil, err
    }

    err = CheckValidityOfDidControllers(didDocument)
    if err != nil {
        return nil, err
    }

    err = CheckIfSignaturesAreValid(didDocument, signature)
    if err != nil {
        return nil, err
    }
    // ..................... //

    // Storing DID Document on Store //
    var metadata *types.Metadata = CreateMetadataForDIDDocument()

    // Forming The DID Document State to be stored on chain
    didDocumentState := types.DidDocumentState{
		DidDocument:         didDocument,
		DidDocumentMetadata: &metadata,
	}

    CreateDidDocumentInStore(ctx, didDocumentState)
    // ---------------------------- //
}
```

**Query Based Keepers**

Let's take the example of Query RPC `QueryDidDocument`

The proto definition of RPC is as follows:

```proto
service Query {
    // ---
    rpc QueryDidDocument(QueryDidDocumentRequest) returns (QueryDidDocumentResponse) {
        option (google.api.http).get = "/hypersign-protocol/hidnode/ssi/did/{didId}";
    }
    // ---
}

message QueryDidDocumentRequest {
  string didId = 1;
}

message QueryDidDocumentResponse {
  Did didDocument = 1;
  Metadata didDocumentMetadata = 2;
}
```

Pseudocode:

```go
// x/ssi/keeper/grpc_query_did.go

func (k Keeper) QueryDidDocument(goCtx context.Context, req *types.QueryDidDocumentRequest) (*types.QueryDidDocumentResponse, error) {
    ctx <- unwrap SDK Context from `goCtx`
    didId <- get did Id from `req`

    didDocumentState, err := GetDidDocumentFrom(didId)
    if err != nil {
        return nil, err
    }

    return &types.QueryDidDocumentResponse{
		DidDocument:         didDoc.GetDidDocument(),
		DidDocumentMetadata: didDoc.GetDidDocumentMetadata(),
	}, nil
}
```

## Store

The Store is a Key-Value structure responsible for persisting the state of chain. The store can have multiple subspaces, which acts as individual KV Stores. The identification of these subspaces, specifically meant for `x/ssi` module, are mentioned in `x/ssi/types/keys.go`.

### Substore Namespace

The following table describes the substores:

| Namespace | Key | Value |
| --------- | ----------- | ----------- |
| DidKey | DID Document Id | DID Document |
| DidCountKey | ```[]byte(DidCountKey)``` | Registered DID Documents Count |
| SchemaKey | Schema Document ID | Schema Document |
| SchemaCountKey | ```[]byte(SchemaCountKey)``` | Registered Schema Documents Count |
| CredKey     | Credential ID | CredentialStatus Document |
| CredCountKey | ```[]byte(CredCountKey)``` | Registered CredentialStatus Documents Count |
| DidNamespaceKey | ```[]byte(DidNamespaceKey)``` | Chain Namespace |

### Store Functions

The store functions comprise of operations such as addition to, change from and query by key from the Store. These are defined in the following files: 

```
x
└── ssi
    └── keeper
       ├── credential.go
       ├── did.go
       └── schema.go
```

Consider the `Get` and `Set` methods related to DID Document:

**Get**:

```go
// x/ssi/keeper/did.go

// Adding a aew DID Document to store
func (k Keeper) CreateDidDocumentInStore(ctx sdk.Context, didDoc *types.DidDocumentState) uint64 {
    // Get the registered Count
    count := k.GetDidCount(ctx)

    // Initialises the store of subspace DidKey
    store := prefix.NewStore(ctx.KVStore(k.storeKey), []byte(types.DidKey))

    // In DidKey store:
    // Key: DID Document Id
    // Value: DID Document
    id := didDoc.GetDidDocument().GetId()
    didDocBytes := k.cdc.MustMarshal(didDoc)

    // The KV pair is Set in Store in byte array form
    store.Set([]byte(id), didDocBytes)
    
    // Increment registered DID Document count by 1
    k.SetDidCount(ctx, count+1)
    return count
}
```

**Set**:

```go
// x/ssi/keeper/did.go

// Get the DID Document from Store
func (k Keeper) GetDid(ctx *sdk.Context, id string) (*types.DidDocumentState, error) {
    // Initialises the store of subspace DidKey
    store := prefix.NewStore(ctx.KVStore(k.storeKey), types.KeyPrefix(types.DidKey))

    var didDocState types.DidDocumentState
    // Fetch the DID Document from store (in byteArray form)
    var bytes = store.Get([]byte(id))
    // Unmarshal byteArray into DidDocumentState type
    if err := k.cdc.Unmarshal(bytes, &didDocState); err != nil {
        return nil, sdkerrors.Wrap(sdkerrors.ErrInvalidType, err.Error())
    }

    return &didDocState, nil
}
```

## Begin-Block

The status of every Registered Verifiable Credential (VC) is check at the beginning of each block. If the current block datetime is greater than the expiration datetime of a VC, the Status is set to `Expired`.

The BeginBlocker function is written in `x/ssi/abci.go`

```go
// x/ssi/abci.go

// BeginBlocker is called at the beginning of every block
func BeginBlocker(ctx sdk.Context, k keeper.Keeper) {
	// Set all the credential status that have passed their expiration date
	// to Expired
	if err := k.SetCredentialStatusToExpired(ctx); err != nil {
		panic(err)
	}
}


// x/ssi/keeper/credential.go

func (k Keeper) SetCredentialStatusToExpired(ctx sdk.Context) error {
	store := prefix.NewStore(ctx.KVStore(k.storeKey), []byte(types.CredKey))
	iterator := sdk.KVStorePrefixIterator(store, []byte{})
	defer iterator.Close()

	for ; iterator.Valid(); iterator.Next() {
		var cred types.Credential
		if err := k.cdc.Unmarshal(iterator.Value(), &cred); err != nil {
			return err
		}

		currentBlockTime := ctx.BlockTime()
		expirationDate, err := time.Parse(time.RFC3339, cred.GetExpirationDate())
		if err != nil {
			return err
		}

		// Set the Credential Status to Expired
		if currentBlockTime.After(expirationDate) {
			cred.Claim.CurrentStatus = "Expired"
			cred.Claim.StatusReason = "Credential Expired"
			cred.Proof.Updated = currentBlockTime.Format(time.RFC3339)

			updatedCredBytes := k.cdc.MustMarshal(&cred)
			store.Set([]byte(cred.Claim.Id), updatedCredBytes)
		}
	}
	return nil
}
```

# Features

## Key Management

Key Management is the first that a user need to do, when its about interacting with blockchain. `hid-node` supports the following ways to store and manage the public keys:

- `test`: Public Key information is stored in `${HOME}/.hid-node/keyring-test`. This approach is **not recommended** for production use
- `os`: Operating system specific credential sub-system stores the keys encrypted with a passphrase
- `file`: It is similar to `test` backend, with the exception that the keys are encrypted with a passphrase.

**Algorithm**

`secp256k1` algorithm is used in the generation of keys, and it is the only algorithm supported for wallet key generation.

**Address Format**

The addressing scheme used is `bech32` and the address prefix is `hid`

### Commands

- Run the following to generate a key

```
hid-noded keys add <name-of-the-key> --keyring-backed <os | test | file>
```

Save the 24-word mnemonic which is generated in the terminal

If you want to recover a wallet using a Bip39 Mnemonic, append the `--recover` flag to the above command

- List all the keys present in a keyring backend

```
hid-noded keys list --keyring-backed <os | test | file>
```

- Delete a key

```
hid-noded keys delete <name-of-the-key> --keyring-backend <os | test | file>
```

## Token transfer

The `x/bank` module facilitates the transfer of tokens between accounts. The base denomination used in the chain is `uhid`, where `u` represents the SI prefix `micro`. So, `1 HID` represents `1000000uhid`. `uhid` also acts as a governance token. The Coin Type is `118`

Run the following to transfer `uhid` between blockchain accounts

```
hid-noded tx bank send <source-hid-account> <destination-hid-account> <amount-in-uhid> --chain-id <Chain ID>
```

- `<source-hid-account>` - Source blockchain address
- `<destination-hid-account>` - Destination blockchain address
- `<amount-in-uhid>` - Amount to be transferred. Example - `1000uhid`

Check the balance of an address

```
hid-noded q bank balances <account-address>
```

## Staking

{% content-ref url="../validator/running-a-testnet-validator-node.md" %}
[running-a-testnet-validator-node.md](running-a-testnet-validator-node.md)
{% endcontent-ref %}

## Governance

{% content-ref url="../governance/introduction.md" %}
[introduction.md](introduction.md)
{% endcontent-ref %}

## PayTx: Pay fee on someone's behalf

If you want to perform any transaction on chain, you have to pay fees in order to execute it. Adding tokens to your wallet isn't a seamless experience, as you first have to trade your fiat currency with a crypto-currency in a centralised exchange, and then transfer those tokens to your non-custodial wallet, such as [Keplr](https://www.keplr.app/).

The `x/authz` and `x/feegrant` modules work together to enable accounts, having no balance, perform blockchain transactions and have the fee be paid by someone who have granted them authorization.

Performing PayTx transactions from [CosmJS](https://github.com/cosmos/cosmjs) will be available from the version `v0.29.0`.

Let's consider a scenario with two actors who will be present on the network:
- **User**: They don't possess any `uhid` tokens
- **Identity Provider (IdP)**: They possess abundant `uhid` tokens and will pay the fee for User's `MsgCreateDID` transaction.

Lets assume the following:

- `<user-addr>`: User's blockchain address
- `<idp-addr>`: Identity Provider's address

**Steps**

* Grant `User` authorization to perform `MsgCreateDID` transaction.

```
hid-noded tx authz grant <user-addr> generic --from <idp-addr> --msg-type "/hypersignprotocol.hidnode.ssi.MsgCreateDID"
```

List the authorizations

```
hid-noded q authz grants <idp-addr> <user-addr>
```

* Specify the amount of tokens `User` is allowed to spend in fees. Once this limit exhausts, `User` cannot perform the authorized transaction 

```
hid-noded tx feegrant grant <idp-addr> <user-addr> --spend-limit 1000uhid
```

List the fee allowances

```
hid-noded q feegrant grants <user-addr>
```

* Generate a `MsgCreateDID` transaction and store it in a json file `tx.json`

```
hid-noded tx ssi create-did '{
"context": [
"https://www.w3.org/ns/did/v1"
],
"id": "did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf",
"controller": ["did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"],
"verificationMethod": [
{
"id": "did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1",
"type": "Ed25519VerificationKey2020",
"controller": "did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf",
"publicKeyMultibase": "zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf"
}
],
"authentication": [
"did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1"
]
}' did:hs:zEYJrMxWigf9boyeJMTRN4Ern8DJMoCXaLK77pzQmxVjf#key-1 --ver-key <base64 encoded private key> --from <user-addr> --generate-only > tx.json
```

* Execute the `MsgCreateDID` transaction with fee paying account being **Identity Provider**

```
hid-noded tx authz exec tx.json --from <user-addr> --fee-account <idp-addr> --fees 50uhid
```

The `50uhid` is deduced from the **Identity Provider** account

## Cross-chain Token transfer

The cross-chain transfer of tokens between Cosmos-based chains is possible using Inter-Blockchain Communication (IBC) Protocol. Refer the IBC Documentation [here](https://ibc.cosmos.network/main/ibc/overview.html).

Run the following to transfer tokens between two accounts located on seperate chains

```sh
hid-noded tx ibc-transfer transfer <source-ibc-port> <source-ibc-channel> <destination-chain-wallet-address> <amount> --from <source-chain-wallet-address> 
```

# Architecture

## Modes of Operation

The `hid-node` can be run in three modes:

### Full Node

This node stores the complete state of blockchain. However, it does not actively participate in the validation process. Every connected node, by default, is a full node.

### Validator Node

It is a full node, which has a significant stake in the network and activately takes part in the validation process.

### Seed Node

It's purpose is to introduce newly connected nodes, to other nodes in the network, and disconnects after doing so.

In order to run in seed mode, set `pex = true` and `seed_mode = true` in `<hid-node config dir>/config/config.toml`

## Sentry Node Architecture

In order to mitigate DDoS or similar attacks on the validator node, it is recommended to spin a full node, which will be connected to the full node. This architecture is known as **Sentry Node Architecture**.

The Validator Node is isolated from the outside world, through private subnetting. The `Sentry` node is connected to the Validator Node. RPC Endpoint and Node ID of Sentry Node are exposed for everyone to connect with. Sentry Node can be thought of as a reverse proxy.

