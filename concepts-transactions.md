# Transactions

- [Introduction](#introduction)
- [Building a Transaction](#building-a-transaction)
  - [OP_RETURN Script](#op_return-script)
    - [Envelope Header](#envelope-header)
    - [Action Payload](#action-payload)
- [Sample Code](#sample-code)
- [Example](#example)

<a name="introduction"></a>

## Introduction

All Tokenized transactions are normal Bitcoin transactions that use P2PKH addresses. The main feature that defines a Tokenized transaction is an `OP_RETURN` output that contains a Tokenized action. Bitcoin (BSV) is always used to pay network fees and all outputs, except `OP_RETURN`, require dust amounts of Bitcoin, at a minimum, to be valid. The protocol also identifies roles (smart contract, administration, token senders/receivers, etc.) by the position (index of the inputs and outputs) of public address(es) in the transaction.

All user and administration driven actions are initiated by sending a request to the smart contract, via the blockchain, to perform a certain action. If the request is valid, the smart contract will respond by sending a response transaction containing updated information about the contract or instrument (new balances, updated revision data, etc). Response actions will always be addressed to either the contract, administration, operator, or user address(es). As well as contract related and other fees being sent to the appropriate addresses. The smart contract sends back to itself in what are known as contract-wide actions that affect the contract or instrument as a whole.

Some transactions (eg. [Static Contract](../protocol/actions#static-contracts), [Transfer](../protocol/actions#action-transfer) action) may require multiple inputs that are signed by different parties to be recognised by the contract.

Transactions that [impact balances](../concepts/tokens#token-balances) or the contract state always include a timestamp to ensure that even in the event of a block re-organisation that the contract actions can be restored in the correct order.

<a name="building-a-transaction"></a>

## Building a Transaction

Tokenized transaction messages are built by serializing the data (converting to binary) according to the protocol specification. There are many [different data formats](../protocol/actions#field-types) used by each protocol action.

<a name="op_return-script"></a>

### OP_RETURN Script

Tokenized assembles OP_RETURN scripts using the [Envelope](https://github.com/tokenized/envelope) protocol version 1 with a protocol identifier of `TKN`, or `test.TKN` for test mode. The [Data Structure](https://github.com/tokenized/envelope#data-structure) section further describes the format of the OP_RETURN script.

<a name="envelope-header"></a>

#### Envelope Header

* `OP_FALSE OP_RETURN` to specify that it is unspendable and only contains data so that no satoshis need to be included in the output.
* `0x02bd01` for the Envelope protocol identifier and version. `0x02` specifies it is a 2 byte push data, then the two bytes are `0xbd` for bitcoin data (Envelope protocol), and `0x01` for version 1.
* The number of protocol IDs, represented by a bitcoin script number, which is normally 1 for Tokenized, represented as the op code OP_1.
* `TKN` or `test.TKN` to specify the Tokenized protocol, depending if test mode is activated.
* The number of push datas used to represent the Tokenized action payload, represented by a bitcoin script number. It will normally be 3, represented by the op code `OP_3`.

<a name="action-payload"></a>

#### Action Payload

The first push data of the Envelope payload is used to specify the version of the Tokenized protocol.

The second push data of the Envelope payload is used to specify the Tokenized action type of the message (i.e. ASCII value 'C1' for Contract Offer).

The third push data of the Envelope is the Tokenized "action" payload. The action payload contains the [action contents](../protocol/actions#all-actions).

The action payload is dependent on the action type and may include token specific information as required. It is encoded using [protobuf](https://developers.google.com/protocol-buffers/) If the payload does not conform to the contract agent's expectation of the operation being requested, it will respond with a rejection message.

<a name="sample-code"></a>

## Sample Code

Here is some sample golang code that uses our reference golang protocol implementation to create a Tokenized `OP_RETURN` output.

```
import (
  "github.com/tokenized/smart-contract/pkg/protocol"
  "github.com/tokenized/smart-contract/pkg/wire"
)

// Create Offer message
offerData := actions.ContractOffer{
  ContractName: "Test Name",
  Issuer: actions.EntityField{Administration: []actions.AdministratorField{
    actions.AdministratorField{Type: 1, Name: "John Smith"},
  }},
  VotingSystems: []*actions.VotingSystemField{&actions.VotingSystemField{Name: "Relative 50", VoteType: "R", ThresholdPercentage: 50, HolderProposalFee: 50000}},
}

// Define permissions for contract fields
permissions := make([]protocol.Permission, actions.ContractFieldCount)
for i, _ := range permissions {
  permissions[i].Permitted = false      // administration can't update field without proposal
  permissions[i].AdministrationProposal = false // administration can update field with a proposal
  permissions[i].HolderProposal = false // Holder's can initiate proposals to update field

  permissions[i].VotingSystemsAllowed = make([]bool, len(offerData.VotingSystems))
  permissions[i].VotingSystemsAllowed[0] = true // Enable this voting system for proposals on this field.
}

var err error
offerData.ContractAuthFlags, err = protocol.WriteAuthFlags(permissions)
if err != nil {
  return errors.Wrap(err, "Failed to serialize contract auth flags")
}

// Build offer transaction
offerTx := wire.NewMsgTx(1)

// Add input spending P2PKH output containing administration's locking script.
...

// Add P2PKH output to contract agent's locking script.
...

// Add Tokenized OP_RETURN message output.
script, err := protocol.Serialize(&offerData, isTest)
if err != nil {
  return errors.Wrap(err, "Failed to serialize OP_RETURN")
}
offerTx.TxOut = append(offerTx.TxOut, wire.NewTxOut(0, script))
```

<a name="example"></a>

## Example

The following example shows a high-level overview of a transfer of tokens to highlight key components of the structure of Tokenized transactions. The example shows one person, Mary, sending 15,000 tokens to Bill using the most basic form of a Transfer action. The smart contract, upon validation of the Transfer action, responds with a Settlement action to complete the transfer of tokens.

![Transaction Overview](https://raw.githubusercontent.com/tokenized/docs/master/images/transactions-overview.svg?sanitize=true)
<span name="image-label">Transaction Overview</span>
