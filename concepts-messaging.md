# Messaging

- [Introduction](#introduction)
- [Message action](#message-action)
- [Rejection action](#rejection-action)
  - [Basic Rejection Codes](#rejection-codes)
  - [Contract Rejection Codes](#rejection-contract-codes)
  - [Instrument Rejection Codes](#rejection-instrument-codes)
  - [Transfer Rejection Codes](#rejection-transfer-codes)
  - [Governance Rejection Codes](#rejection-governance-codes)
  - [Enforcement Rejection Codes](#rejection-enforcement-codes)
  - [Funding Rejection Codes](#rejection-funding-codes)
  - [Address Rejection Codes](#rejection-address-codes)
  - [Signature Rejection Codes](#rejection-signature-codes)

<a name="introduction"></a>

## Introduction

The Tokenized Protocol includes a rich and expressive set of messaging actions which allow issuers, operators and users the flexibility to correspond in a way that gives wallets, account management and audit software the ability to record a full set of transactional actions.
Messaging actions are split into two types, the Message action and Rejection action.

<a name="message-action"></a>

## Message action

Message actions are for general purpose messaging between users. The protocol has the means to support pre-defined message types allowing messaging to be used for many things including:

- Transaction templates
- Purchase Orders and Invoices
- Receipts
- Shipping notices
- Tags
- Transaction descriptions
- Quartlery/Yearly Reports (10K, 10Q, etc)
- Collateral Calls
- Encrypted messages
- Public (cleartext) messages
- And many other types

Message actions do not, generally, involve a smart contract and only serve to record communication data to the blockchain. The message action format is standardised to ensure that any wallets which follow the Tokenized Protocol will be able to identify, parse and categorize messages.
A message may be sent to many addresses at once by appending multiple outputs to the transaction which contains the Message action.

![Message action](https://raw.githubusercontent.com/tokenized/docs/master/images/message-action.svg?sanitize=true)
<span name="image-label">Message action</span>

There are 6 Message types currently defined in the Tokenized Protocol:

- Public message: Message #0002 - A generic public message or public announcement. Sent to an address(es). Can be used for an official issuer announcement.

- Private message: Message #0003 - A generic private message. Sent to another address(es). Encryption is to be used.

- Reverted Tx: Message#0004 - A message that contains a bitcoin transaction that was accepted by the network or an agent and then invalidated by a reorg, or zero conf double spend. This serves as on chain evidence of the sending party's signatures and approval for the given transaction.

- Offer message: Message #1001 - A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should have all, or nearly all, of the details required for the receiving party to accept the offer. The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror's payment/receipt details, etc.). The Offer message is different to a Signature Request message in that it is missing the offeree's payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction. If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message.

- Signature Request message: Message #1002 - Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.

- Settlement Request message: Message #1003 - A message that contains a multi-contract settlement that needs settlement data added by another contract. Sent to another contract to request data be added.

As the Tokenized Protocol matures, it is expected that many more message types will be introduced which enable new and exciting functionality to be handled simply and easily.

<a name="rejection-action"></a>

## Rejection action

The rejection action is the only message type sent by the smart contract. The Rejection action is used when a user has requested an action that is unable to be completed by the smart contract. All rejection messages include a rejection type, which links to a message telling the user why their request was rejected.

![Rejection action](https://raw.githubusercontent.com/tokenized/docs/master/images/rejection-action.svg?sanitize=true)
<span name="image-label">Rejection action</span>

The following rejection messages have been defined:

<a name="rejection-codes"></a>

### Basic Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 0</td><td>Success - No failure. This code should not be used in a reject message.</td></tr>
    <tr><td>Code 1</td><td>Message Malformed - The OP_RETURN message is malformed. It doesn't pass data validation or something about it isn't according to protocol.</td></tr>
    <tr><td>Code 2</td><td>Transaction Malformed - The Bitcoin tx is malformed. Incorrect inputs/outputs or something similar.</td></tr>
</table>

<a name="rejection-contract-codes"></a>

### Contract Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 10</td><td>Contract Already Exists - The contract already exists and can't be recreated.</td></tr>
    <tr><td>Code 11</td><td>Contract Is Not Dynamic - 'Sent when a CO is received, but the contract type is not "D" (Dynamic)'</td></tr>
    <tr><td>Code 12</td><td>Contract Instrument Quantity Reduction - Sent when a CA tries to reduce the number of instruments below the number of instruments the contract has.</td></tr>
    <tr><td>Code 13</td><td>Contract Fixed Quantity - Sent when the issuer attempted to increase the quantity of instruments in a contract beyond the fixed quantity permitted.</td></tr>
    <tr><td>Code 14</td><td>Contract Auth Flags Prohibit - The contract auth flags don't permit the action requested.</td></tr>
    <tr><td>Code 15</td><td>Contract Expired - The contract is expired so can no longer accept requests.</td></tr>
    <tr><td>Code 16</td><td>Contract Frozen - The contract is frozen and the request is not permitted while frozen.</td></tr>
    <tr><td>Code 17</td><td>Contract Revision Incorrect - The revision in a contract amendment is incorrect.</td></tr>
</table>

<a name="rejection-instrument-codes"></a>

### Instrument Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 20</td><td>Instrument Code Already Exists - The instrument code specified already exists and can't be reused.</td></tr>
    <tr><td>Code 21</td><td>Instrument Not Found - The instrument code is not found.</td></tr>
    <tr><td>Code 22</td><td>Instrument Auth Flags Prohibit - The instrument auth flags don't permit the action requested.</td></tr>
    <tr><td>Code 23</td><td>Instrument Frozen - The instrument is frozen and the request is not permitted while frozen.</td></tr>
    <tr><td>Code 24</td><td>Instrument Revision Incorrect - The revision in an instrument amendment is incorrect.</td></tr>
</table>

<a name="rejection-transfer-codes"></a>

### Transfer Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 30</td><td>Transfer To Self Prohibited - Transfers with the sender and receiver addresses the same are not permitted.</td></tr>
    <tr><td>Code 31</td><td>Transfer Expired - The transfer has expired.</td></tr>
    <tr><td>Code 32</td><td>Holdings Frozen - Holdings are frozen, so the request can't be completed.</td></tr>
</table>

<a name="rejection-governance-codes"></a>

### Governance Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 40</td><td>Holder Proposal Prohibited - Holders are not permitted to make proposals.</td></tr>
    <tr><td>Code 41</td><td>Proposal Conflicts - The proposal conflicts with an unapplied proposal.</td></tr>
    <tr><td>Code 42</td><td>Vote Not Found - The vote ID referenced is not found.</td></tr>
    <tr><td>Code 43</td><td>Vote Closed - The vote has closed and ballots are no longer permitted.</td></tr>
    <tr><td>Code 44</td><td>Ballot Already Counted - The ballot has already been counted for this address.</td></tr>
</table>

<a name="rejection-enforcement-codes"></a>

### Enforcement Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
</table>

<a name="rejection-funding-codes"></a>

### Funding Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 60</td><td>Insufficient Transaction Fee Funding - Insufficient bitcoin quantities for response transaction fees.</td></tr>
    <tr><td>Code 61</td><td>Insufficient Value - Insufficient bitcoin quantity in inputs to fund request.</td></tr>
    <tr><td>Code 62</td><td>InsuInsufficient Quantity - Insufficient token holdings to for request.</td></tr>
</table>

<a name="rejection-address-codes"></a>

### Address Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 70</td><td>Requestor Is Not Issuer - The requestor is not the issuer and is required to be for this request.</td></tr>
    <tr><td>Code 71</td><td>Requestor Is Not Operator - The requestor is not the operator and is required to be for this request.</td></tr>
    <tr><td>Code 72</td><td>Unauthorized Address - The address specified is not permitted for this request.</td></tr>
</table>

<a name="rejection-signature-codes"></a>

### Signature Rejection Codes

<table>
    <tr>
        <th style="width:15%">Code</th>
        <th>Description</th>
    </tr>
    <tr><td>Code 80</td><td>Invalid Signature - The signature provided is not valid. This is for signatures included within OP_RETURN data. Not bitcoin transaction signature scripts.</td></tr>
</table>
