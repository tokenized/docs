# Transactions

- [Introduction](#introduction)
- [Building a Transaction](#building-transaction)
- [Payload Breakdown](#payload-breakdown)

<a name="introduction"></a>
## Introduction

All Tokenized transactions are normal Bitcoin transactions that use P2PKH (or P2PSH) addresses in the inputs and outputs.  The main feature that defines a Tokenized transaction is an `OP_RETURN` output that contains a Tokenized action. Bitcoin (BSV) is always used to pay network fees and all inputs and outputs require dust amounts of Bitcoin, at a minimum, to be valid.  The protocol also identifies roles (smart contract, issuer, token senders/receivers, etc.) by the position (index of the inputs and outputs) of public address(es) in the transaction.  

All user and issuer driven actions are initiated by sending a request to the smart contract, via the blockchain, to perform a certain action. If the request is valid, the smart contract will respond by sending a response transaction containing updated information about the contract or asset (new balances, updated revision data, etc).  Response actions will always be addressed to either the issuer or user address(es) or some satoshis will be sent back to the smart contract address.  The smart contract sends change back to itself in what are known as contract-wide actions that affect the contract or asset as a whole.

Some transactions (eg. [Static Contract](../protocol/actions#static-contracts), [Transfer](../protocol/actions#action-transfer) action) require multiple inputs that are signed by different parties to be recognised by the contract. If the smart contract finds that the transaction is valid -- within contract & protocol rules, adequate balance and the correct fees included -- it will process the request, and send a response transaction to the blockchain as confirmation.

Transactions that impact balances or the contract state always include a timestamp to ensure that even in the event of a block re-organisation that the contract actions can be restored in the correct order.

<a name="building-transaction"></a>
## Building a Transaction

Tokenized transactions are built by compiling the token data as a list of fields and appending them to each other as a hexadecimal string. There are many [different data formats](../protocol/field-types) used by each protocol action.

### Assembling OP_RETURN Packet

To assemble an `OP_RETURN` packet, the first byte is always the `OP_RETURN` opcode (`0x6a`).

The second byte is a `PUSHDATA` instruction. The `PUSHDATA` instruction can be variable depending on the number of bytes in the data packet being pushed into the output. It is possible to perform multiple pushes in a single `OP_RETURN` output, allowing the output to have multiple fields of different lengths. There are always 2 pushdata operations in a Tokenized operation. The first carries the "Tokenized" protocol identifer (**tokenized.com**), and the second carries the remainder of the data in the packet. This can be up to 99kB of data with the current BitcoinSV network capability, but as the Bitcoin protocol is returned to the Version 0.1 platform the removal of restrictions will allow contracts up to ~4GB to be built.

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

### Protocol Identifier

The first push is 13 bytes long and contains only the Tokenized protocol identifier which is the string **tokenized.com**.

### Action Payload

The action payload is dependent on the action type and may include token specific information as required. It is important that the client and wallet must both know exactly what is expected in the remainder of the packet through a combination of the action prefix and version. If the packet does not conform to the contract agent's expectation of the operation being requested, it will respond with a rejection message.

## Example

The following example shows a high-level overview of a transfer of tokens to highlight key components of the structure of Tokenized transactions.  The example shows one person, Mary, sending 15,000 tokens to Bill using the most basic form of a Transfer action.  The smart contract, upon validation of the Transfer action, responds with a Settlement action to complete the transfer of tokens.
