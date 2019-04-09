# Contract Types

- [Introduction](#introduction)
- [Smart Contracts](#smart-contracts)
    - [Contract Operator](#contract-operator)
- [Static Contracts](#static-contracts)

<a name="introduction"></a>
## Introduction

Tokenized contracts allow for entities to store and manage contracts on the Bitcoin (BSV) network in a standardized way that allows for interoperability with other contracting parties and the use of Bitcoin's digital signature algorithms to create a more robust way of creating and managing agreements.  The Bitcoin network allows for a global, public, immutable, and reliable ledger which is extremely valuable for storing, managing and timestamping contracts.

A Tokenized contract references (hash) or stores all of the terms and conditions, in prose, associated with a binding legal contract.  Depending on the jurisdiction, additional clauses may have to be added to the contract to recongnise the Tokenized protocol and on-chain actions as meaningful and binding to the contracting parties of the contract.  For this reason, building contracts using Tokenized requires the same level of foresight, preparation and expertise as that required for the creation of any other traditional contract.

There are two types of contracts supported by the Tokenized system:

* [Smart Contracts](#smart-contracts)
* [Static Contracts](#static-contracts)

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-decision-tree.svg?sanitize=true" alt="Decision Tree - Static vs Dynamic Contracts">

<a name="smart-contracts"></a>
## Smart Contracts

A smart contract (aka dynamic contract) is a contract which is managed by an autonomous agent (off-chain daemon) using the Tokenized protocol. The smart contract operates on behalf of the issuer for all administrative tasks associated with maintaining and updating the contract's on-chain records.  The smart contract is responsible for monitoring the state of the contract and for controlling actions that affect the terms and state of the contract with respect to the terms and state of the contract, at the time the request action was received.  The smart contract can also work with other autonomous agents working on behalf of the issuer or other contracting parties to fully automate all the various processes and tasks associated with the formation and performance of a contract.

The smart contract can only respond to instructions it receives as Tokenized transactions into its own wallet. All responses from the smart contract are sent onto the blockchain as per the order of operations needed for the action taking place.

The Tokenized Smart Contract is written in Go and is fully open source. Details of the smart contract can be found in the [Tokenized Smart Contract Github repository](https://github.com/tokenized).

<a name="contract-operator"></a>
### Contract Operator

An issuer can operate their own smart contract, or they can have a technical specialist operate the smart contract on their behalf. This technical specialist is called a 'contract operator'.  The contract operator is identified by their public address which is specified in the Contract Offer action.

The contract operator has permission to act on the behalf of the issuer for the inititation of different actions.  issuers may prefer to outsource this work for various reasons and it is likely they will get a better price and higher reliability/performance than they would if they tried to operate it themselves.

#### Tokenized Contract Formation
A Tokenized contract is formed when a token issuer presents a valid 'Contract Offer' action to a smart contract. The smart contract checks only that the rules proposed in the offer are compliant with its logic, but the legal and regulatory aspects of dealing with the assets being created must be pre-determined and managed by the issuer to ensure the contract operates within all applicable laws and regulations.

#### 1. Contract Offer
To create a Contract Offer, the Contract issuer must prepare an action that contains all of the required information such as:
* Contract name
* Governing Law
* Jurisdiction
* Contract rules, voting systems
* Detail of the issuing entity/entities including key personnel, addresses etc.
Included with the offer is either a hash and a URL linking to a contract file, or when possible, the entire contract file itself as a Markdown formatted file or PDF.
The Contract Offer action must be signed by both the issuer and the smart contract Operator, so the issuer first builds a template transaction which it sends to the smart contract Operator:
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action-template.svg?sanitize=true" alt="A contract offer action template" align="middle">
If the contract meets the smart contract Operator's requirements, they will add an input from their own wallet, add the change outputs they need and sign the Contract Offer using SIGHASH_ALL before sending it back to the issuer. Once the issuer has reviewed the smart contract Operator's changes, they can sign their own input (or inputs) using SIGHASH_ALL and send the transaction onto the network.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action-final.svg?sanitize=true" alt="Final contract offer action" align="middle">

#### 2. Contract Formation
When the smart contract receives the Offer action it unpacks the information and evaluates it. If the smart contract decides there are no issues, it builds a 'Contract Formation' action in response which is sent onto the network. The Contract Formation action contains a complete repeat of all of the information in the Contract Offer action as an acknowledgement that the smart contract has accepted the setup as valid.
The contract also adds two additional fields
1. Timestamp - The time at which the smart contract built the Contract Formation action
2. Version field - Set to zero for a new contract. Increments by 1 each time the contract is updated
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action.svg?sanitize=true" alt="Contract Formation action" align="middle">

### Tokenized Contract Amendment
The amendment of a Tokenized contract can be simple when the rules or conditions being changed are able to be amended without needing a vote. This is called a Unilateral Amendment, and is comprised of just 2 actions.
1. Contract Amendment
2. Contract Formation

Where a Contract Amendment seeks to make changes that require a vote through referendum or initiative, there is no longer a Unlateral Amendment since the rules of the vote determine the outcome of the Contract Amendment.

#### 1. Contract Amendment
If the issuer wants to change the issuer address (e.g. in the event of a contract being sold) or to change the Operator address (to move to a new service provider) there are flags for these options. The smart contract receives the new addresses for these contracts from signed inputs paying into the transaction carrying the Contract Amendment action.
Following on from these flags is the new contract revision, which is incremented by 1 each time the contract is updated. A Contract Amendment request that has a version number that isn't in sequence will be rejected.
Subsequent to these fields, amendments to the contract are contained in an array of objects, each of which has the following information:
* The field index of the contract element being changed
* The element of the field (for to identify the index number of the element within an array - complex types only)
* The Sub Field Index (to identify the field within the object in the array - complex types only)
* An instruction on whether to add or delete an element (for arrays)
* The new data being placed into the specified index
For amendments that require a vote to be passed, the TXID of a Result action showing a positive vote outcome for the change must be added as the final data item in the Contract Amendment action.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-amendment-action.svg?sanitize=true" alt="Contract Amendment action" align="middle">

#### 2. Contract Formation
When the contract sees the Contract Amendment action land in its wallet, it evaluates the action and looks to ensure that the modifications are valid. 
If the contract determines that the amendment is valid, it issues a full Contract Formation action including the full details of the contract, the updated version number and a new timestamp.
From this moment, all transaction requests to the contract must abide by the amended rules.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action-amendment.svg?sanitize=true" alt="Updated Contract Formation action" align="middle">

<a name="static-contracts"></a>
## Static Contracts

A static contract is a legal contract similar to that which one would enter into today for the undertaking of a scope of work, to enter into a non-disclosure agreement, or to manage the sale of an off-chain asset that has not been tokenized.

The static contract framework simply provides an easy and low-cost way for inscribing the details of these contracts onto the public ledger which provides the contracting parties with benefits of the Bitcoin network. Static contracts require only a single action to be established and do not require a Tokenized smart contract to operate.  Each of the contracting parties simply sends a small amount of Bitcoin back to themselves all on the same transaction that has the static contract formation action in it, to allow for their signatures (intention) to be recorded to the contract.
