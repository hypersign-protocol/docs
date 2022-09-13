# HID Node

> In Progress

Hypersign Identity Network (HID Node) is built on top of Cosmos SDK. This documentation only covers the SSI module and the basic commands of other Cosmos Modules. It is recommended to have a good understanding of Cosmos SDK. Please refer Cosmos SDK docs [here](https://docs.cosmos.network/v0.45/).

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
The interaction between a client the HID Node happens through RPC, which is built using Protobuf. The proto files are defined under `proto/ssi/v1`. The are two RPC `service` namely `Msg` and `Query`, defined in `proto/ssi/v1/tx.proto` and `proto/ssi/v1/query.proto` respectively. List of HID Node RPCs are:

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

The generation of golang files of Protobuf files is done by the script `scripts/protogenc.sh`. The generated files are present in `x/ssi/types`. 

## Protobuf Description

### DID Document

The DID-Core W3C Specification has been followed to frame the structure of a DID. It's proto representation is mentioned in `proto/ssi/v1/did.proto`. The message `DidDocumentState` is the one which is store on chain.

```proto
// proto/ssi/v1/did.proto

message DidDocumentState {
  Did didDocument = 1;
  Metadata didDocumentMetadata = 2;
}
```

### Schema Document

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

### Credential Status Document

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

In Cosmos SDK, every operations related to blockchain such as staking, delegation, token trasfer, etc are composed in different modules. They are defined in the `x` directory of Cosmos SDK (Check [here](https://github.com/cosmos/cosmos-sdk/tree/main/x)). For instance, `x/bank` module handles the functionality of token transfer. `x/ssi` module lets you register documents such Decentralised Identifiers (DID), Schema Document and Verifiable credential Status on chain.

**Quick Overview**

`x/ssi/client/cli`: CLI Client for sending transactions to and query from Blockchain. Refer the detailed list of commands [here]() //TODO: Add link to SSI Page

`x/ssi/keeper`: Interaction with the state of blockchain

`x/ssi/genesis.go`: Initialises genesis variables for `x/ssi` module

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

# Common CLI Commands

Few points to consider:

- If `minimum-gas-price` in `${HOME}/.hid-node/config/app.toml` is set to `0uhid`, there isn't a need to pass the `--fees` parameter in transaction based commands.
- `--chain-id` has to be explicitly passed wherever necessary, and it should match with the chain-id value defined during the initialisation of `hid-node`.
- The default value for `--keyring-backend`, if not passed, is `os`. The other values are `test`, `file`, `kwallet`, `pass`, `memory`.

**Token Transfer**

```sh
hid-noded tx bank send <sender-wallet-address> <recipient-wallet-address> <amount-in-uhid>
```

```sh
hid-noded tx bank send hid1c0qs3eyu5pqqwr70j2klsrpuqhjd8xqqeuj22x hid1t7xv0j9xhlkpt3fsy5hzrnh7vmg6cduef3f8p8 10000000uhid
```

**Validator Creation.** Check [here](../validator/running-a-testnet-validator-node.md)

**Delegating $HID to a Validator**

```sh
hid-noded tx staking delegate <operator-address-of-validator> <amount> --from <delegator-address>
```

```sh
hid-noded tx staking delegate hidvaloper1c0qs3eyu5pqqwr70j2klsrpuqhjd8xqqx79qze 10000uhid from hid1t7xv0j9xhlkpt3fsy5hzrnh7vmg6cduef3f8p8
```

**Withdrawing Rewards (Non-Validator User)**

```sh
hid-noded tx distribution withdraw-rewards <validator-addr> --from <user-wallet-address>
```

```sh
hid-noded tx distribution withdraw-rewards hidvaloper1c0qs3eyu5pqqwr70j2klsrpuqhjd8xqqx79qze --from hid1c0qs3eyu5pqqwr70j2klsrpuqhjd8xqqeuj22x
```

**Withdrawing Rewards along with Commission (Validator)**

```sh
hid-noded tx distribution withdraw-rewards <validator-addr> --from <user-wallet-address>
```

```sh
hid-noded tx distribution withdraw-rewards hidvaloper1c0qs3eyu5pqqwr70j2klsrpuqhjd8xqqx79qze --from hid1t7xv0j9xhlkpt3fsy5hzrnh7vmg6cduef3f8p8 --commission
```

**`x/ssi` Transactions**
  - [Decentralised Identifier](../self-sovereign-identity-ssi/decentralized-identifier-did.md)
  - [Schema](../self-sovereign-identity-ssi/schema.md)
  - [Credential Status](../self-sovereign-identity-ssi/verifiable-credential-vc/credential-revocation-registry.md)

**Governance Proposal Submission** Check [here](../governance/introduction.md)

**Transfer tokens through IBC**

```sh
hid-noded tx ibc-transfer transfer transfer channel-0 <desitnation chain wallet address> <amount> --from <source chain wallet address> 
```

Suppose you want transfer `1000uhid` from Hypersign Identity Network to Osmosis

```
hid-noded tx ibc-transfer transfer transfer channel-0 <osmo1..> 1000uhid --from <hid1..>
```

Refer the IBC Documentation [here]((https://ibc.cosmos.network/main/ibc/overview.html)).
