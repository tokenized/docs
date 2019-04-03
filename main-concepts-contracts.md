# Contracts

Tokenized contracts allow for entities to store and manage contracts on the Bitcoin (BSV) network in a standardized way that allows for interoperability with other contracting parties and the use of Bitcoin's digital signature algorithms to create a more robust way of creating and managing agreements.  The Bitcoin network allows for a global, public, immutable, and reliable ledger which is extremely valuable for storing, managing and timestamping contracts.

A Tokenized contract references (hash) or stores all of the terms and conditions, in prose, associated with a binding legal contract.  Depending on the jurisdiction, additional clauses may have to be added to the contract to recongnise the Tokenized protocol and on-chain actions as meaningful and binding to the contracting parties of the contract.  For this reason, building contracts using Tokenized requires the same level of foresight, preparation and expertise as that required for the creation of any other traditional contract.

There are two types of contracts supported by the Tokenized system:

1. [Static Contracts](#static-contracts)
2. [Smart Contracts](#smart-contracts)

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-decision-tree.svg?sanitize=true" alt="Decision Tree - Static vs Dynamic Contracts">

<a name="static-contracts"></a>
## Static Contracts

A static contract is a legal contract similar to that which one would enter into today for the undertaking of a scope of work, to enter into a non-disclosure agreement, or to manage the sale of an off-chain asset that has not been tokenized.

The static contract framework simply provides an easy and low-cost way for inscribing the details of these contracts onto the public ledger which provides the contracting parties with benefits of the Bitcoin network. Static contracts require only a single action to be established and do not require a Tokenized smart contract to operate.  Each of the contracting parties simply sends a small amount of Bitcoin back to themselves all on the same transaction that has the static contract formation action in it, to allow for their signatures (intention) to be recorded to the contract.

<a name="smart-contracts"></a>
## Smart Contracts

A smart contract (aka dynamic contract) is a contract which is managed by an autonomous agent (off-chain daemon) using the Tokenized protocol. The smart contract operates on behalf of the issuer for all administrative tasks associated with maintaining and updating the contract's on-chain records.  The smart contract is responsible for monitoring the state of the contract and for controlling actions that affect the terms and state of the contract with respect to the terms and state of the contract, at the time the request action was received.  The smart contract can also work with other autonomous agents working on behalf of the issuer or other contracting parties to fully automate all the various processes and tasks associated with the formation and performance of a contract.

The smart contract can only respond to instructions it receives as Tokenized transactions into its own wallet. All responses from the smart contract are sent onto the blockchain as per the order of operations needed for the action taking place.

The Tokenized Smart Contract is written in Go and is fully open source. Details of the smart contract can be found in the [Tokenized Smart Contract Github repository](https://github.com/tokenized).

## contract operator

An issuer can operate their own smart contract, or they can have a technical specialist operate the smart contract on their behalf. This technical specialist is called a 'contract operator'.  The contract operator is identified by their public address which is specified in the Contract Offer action.

The contract operator has permission to act on the behalf of the issuer for the inititation of different actions.  issuers may prefer to outsource this work for various reasons and it is likely they will get a better price and higher reliability/performance than they would if they tried to operate it themselves.
