# Transactions

- [Introduction](#introduction)
- [Building a Transaction](#building-transaction)
  - [Assembling OP_RETURN Packet](#assemble-opreturn)
  - [Using PUSHDATA](#using-pushdata)
- [Payload Breakdown](#payload-breakdown)
  - [Protocol Identifier](#protocol-identifier)
  - [Action Payload](#action-payload)
- [Sample Code](#sample-code)
  - [BitDB](#bitdb)
- [Example](#example)

<a name="introduction"></a>
## Introduction

All Tokenized transactions are normal Bitcoin transactions that use P2PKH addresses.  The main feature that defines a Tokenized transaction is an `OP_RETURN` output that contains a Tokenized action. Bitcoin (BSV) is always used to pay network fees and all outputs, except `OP_RETURN`, require dust amounts of Bitcoin, at a minimum, to be valid.  The protocol also identifies roles (smart contract, administration, token senders/receivers, etc.) by the position (index of the inputs and outputs) of public address(es) in the transaction.

All user and administration driven actions are initiated by sending a request to the smart contract, via the blockchain, to perform a certain action. If the request is valid, the smart contract will respond by sending a response transaction containing updated information about the contract or asset (new balances, updated revision data, etc). Response actions will always be addressed to either the contract, administration, operator, or user address(es). As well as contract related and other fees being sent to the appropriate addresses.  The smart contract sends back to itself in what are known as contract-wide actions that affect the contract or asset as a whole.

Some transactions (eg. [Static Contract](../protocol/actions#static-contracts), [Transfer](../protocol/actions#action-transfer) action) may require multiple inputs that are signed by different parties to be recognised by the contract.

Transactions that [impact balances](../concepts/tokens#token-balances) or the contract state always include a timestamp to ensure that even in the event of a block re-organisation that the contract actions can be restored in the correct order.

<a name="building-transaction"></a>
## Building a Transaction

Tokenized transaction messages are built by serializing the data (converting to binary) according to the protocol specification. There are many [different data formats](../protocol/field-types) used by each protocol action.

<a name="assemble-opreturn"></a>
### Assembling OP_RETURN Packet

To assemble an `OP_RETURN` packet, the first byte is always the `OP_RETURN` opcode (`0x6a`).

The second byte is a `PUSHDATA` instruction. The `PUSHDATA` instruction can be variable depending on the number of bytes in the data packet being pushed into the output. It is possible to perform multiple pushes in a single `OP_RETURN` output, allowing the output to have multiple fields of different lengths. There are always 2 pushdata operations in a Tokenized operation. The first carries the "Tokenized" protocol identifer `tokenized`, and the second carries the remainder of the data in the packet. This can be up to 99kB of data with the current BitcoinSV network capability, but as the Bitcoin protocol is returned to the Version 0.1 platform the removal of restrictions will allow contracts up to 4GB to be built.

<a name="using-pushdata"></a>
### Using PUSHDATA

For packets with less than 75 bytes of data, the pushdata instruction is simply a single byte containing the length of the packet. e.g. `0x6a 0x03 0x010203` is a `OP_RETURN` followed by a `PUSHDATA` instruction to push 3 bytes, and then 3 bytes of information.

For packets containing 76 - 255 bytes of data, the pushdata instruction is the `OP_PUSHDATA1` opcode (`0x4c`) followed by a single byte unsigned integer containing the number of bytes to push in the instruction. For example:

```
0x6a 0x4C 0xD2 <210 bytes of ascii data>
```

This is `OP_RETURN` followed by `OP_PUSHDATA1` followed by `0xD2` which is a hexadecimal representation of 210, then an uninterrupted 210 byte long string of hexadecimal data.

For packets containing 256 - 65,535 bytes of data, `OP_PUSHDATA2` (`0x4d`) is used, followed by a 2 byte representation of the length of the data packet following.

For packets containing 65,536 - 4,294,967,295 bytes of data, `OP_PUSHDATA4` (`0x4e`) is used, followed by a 4 byte represenation of the length of the data packet following.

<a name="payload-breakdown"></a>
## Payload Breakdown

A Tokenized action output is always created with 2 separate push operations. The `OP_RETURN` output is broken down as follows:

<a name="protocol-identifier"></a>
### Protocol Identifier

The first push is 13 bytes long and contains only the Tokenized Protocol identifier which is the string `tokenized`.  For testing on Bitcoin SV's mainnet, `test.tokenized` can be used as the protocol identifier for test actions/messages.

<a name="action-payload"></a>
### Action Payload

The next push is the complete action payload. The action payload contains the [header information](../protocol/actions#header-fields) and the [action contents](../protocol/actions#all-actions). The header is a requirement that specifies information on how to format the rest of the data, including the protocol version and action code.

The action payload is dependent on the action type and may include token specific information as required. It is important that the client and wallet must both know exactly what is expected in the remainder of the packet through a combination of the action code and version. If the packet does not conform to the contract agent's expectation of the operation being requested, it will respond with a rejection message.

<a name="sample-code"></a>
## Sample Code

Here is some sample golang code that uses our reference golang protocol implementation to create a Tokenized `OP_RETURN` output.

```
import (
	"github.com/tokenized/smart-contract/pkg/protocol"
	"github.com/tokenized/smart-contract/pkg/wire"
)

// Create Offer message
offerData := protocol.ContractOffer{
	ContractName: "Test Name",
	Issuer: protocol.Entity{Administration: []protocol.Administrator{
		protocol.Administrator{Type: 1, Name: "John Smith"},
	}},
	VotingSystems: []protocol.VotingSystem{protocol.VotingSystem{Name: "Relative 50", VoteType: 'R', ThresholdPercentage: 50, HolderProposalFee: 50000}},
}

// Define permissions for contract fields
permissions := make([]protocol.Permission, 21)
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
offerTx := wire.NewMsgTx(2)

// Add input spending P2PKH output to administration's identifying public key hash
...

// Add P2PKH output to contract's public key hash
...

// Add Tokenized OP_RETURN message output.
script, err := protocol.Serialize(&offerData)
if err != nil {
	return errors.Wrap(err, "Failed to serialize OP_RETURN")
}
offerTx.TxOut = append(offerTx.TxOut, wire.NewTxOut(0, script))
```

<a name="bitdb"></a>
### BitDB

This BitDB query can be used to query transactions containing Tokenized messages.
```
{
  "v": 3,
  "q": {
    "find": {
      "out.b0": { "op": 106 },
      "out.s1": "tokenized"
    },
    "limit": 10
  }
}
```

This BitDB query can be used to query transactions containing Tokenized messages with a specific action code. The example is for Contract Offer (C1) actions. Just swap out the C1 for other action codes as needed.
```
{
  "v": 3,
  "q": {
    "find": {
      "out.b0": { "op": 106 },
      "out.s1": "tokenized",
	  "out.s2": { "$regex": "^.C1"}
    },
    "limit": 10
  }
}
```

This BitDB query is for all requests to a specific contract.
```
{
  "v": 3,
  "q": {
    "find": {
      "out.b0": { "op": 106 },
      "out.s1": "tokenized",
      "out.e.a": "<ContractAddress>"
    },
    "limit": 10
  }
}
```

This BitDB query is for all responses from a specific contract.
```
{
  "v": 3,
  "q": {
    "find": {
      "out.b0": { "op": 106 },
      "out.s1": "tokenized",
      "in.e.a": "<ContractAddress>"
    },
    "limit": 10
  }
}
```

<a name="example"></a>
## Example

The following example shows a high-level overview of a transfer of tokens to highlight key components of the structure of Tokenized transactions.  The example shows one person, Mary, sending 15,000 tokens to Bill using the most basic form of a Transfer action.  The smart contract, upon validation of the Transfer action, responds with a Settlement action to complete the transfer of tokens.

![Transaction Overview](https://raw.githubusercontent.com/tokenized/docs/master/images/transactions-overview.svg?sanitize=true "Transaction Overview") {.frame .centered .padded}
