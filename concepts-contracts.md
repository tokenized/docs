# Contracts

- [Introduction](#introduction)
- [Smart Contracts](#smart-contracts)
    - [Contract Operator](#contract-operator)
    - [Creating a Contract](#contract-create)
    - [Updating a Contract](#contract-update)
    - [Contract Address Change](#contract-address-change)
- [Static Contracts](#static-contracts)
- [Contract Law](#contract-law)
    - [Contract Formation](#contract-formation)
    - [Agreement](#agreement)
    - [Consideration](#consideration)
    - [Capacity](#capacity)
    - [Intention](#intention)
    - [Certainty](#certainty)

<a name="introduction"></a>
## Introduction

Tokenized contracts allow for entities to form, store and manage contracts on the Bitcoin (BSV) network in a standardized way that allows for interoperability with other contracting parties and the use of Bitcoin's digital signature algorithms to create a more robust way of creating and managing agreements.  The Bitcoin network allows for a global, public, immutable, and reliable ledger which is extremely valuable for storing, managing and timestamping contracts.

A Tokenized contract references (hash) or stores all of the terms and conditions, in prose, associated with a binding legal contract. Depending on the jurisdiction, additional clauses may have to be added to the contract to recognise the Tokenized Protocol and on-chain actions as meaningful and binding to the contracting parties of the contract.  For this reason, building contracts using Tokenized requires the same level of foresight, preparation and expertise as that required for the creation of any other traditional contract.

There are two types of contracts supported by the Tokenized system. [Smart contracts](#smart-contracts) that are hosted by the issuer or third party provider (called a contract operator), and [static contracts](#static-contracts) which are recorded to the blockchain and require no further on-going maintenance.

![Decision Tree - Static vs Dynamic Contracts](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-decision-tree.svg?sanitize=true "Contract Formation: Decision Tree") {.frame .centered .padded}

<a name="smart-contracts"></a>
## Smart Contracts

A smart contract is a dynamic contract that is managed by an autonomous agent (off-chain daemon) using the Tokenized Protocol. The smart contract operates on behalf of the issuer for all administrative tasks associated with maintaining and updating the contract's on-chain records.  The smart contract service is responsible for monitoring data that effect the state of the smart contract and for incorporating those changes into the contract.  The smart contract can also work with other autonomous agents working on behalf of the issuer or other contracting parties to fully automate all the various processes and tasks associated with the formation and performance of a contract.

The smart contract can only respond to instructions it receives as Tokenized transactions into its own wallet. All responses from the smart contract are sent onto the blockchain as per the order of operations needed for the action taking place.

The Tokenized Smart Contract is written in Go and is fully open source. Details of the smart contract can be found in the [Tokenized Smart Contract Github repository](https://github.com/tokenized).

<a name="contract-operator"></a>
### Contract Operator

An issuer can operate their own smart contract, or they can have a technical specialist operate the smart contract on their behalf. This technical specialist is called a 'contract operator'.  The contract operator is identified by their public address which is specified in the Contract Offer action.

The contract operator has permission to act on behalf of the issuer for the inititation of different actions.  Issuers will likely prefer to outsource this work for various reasons and it is likely they will get a much better price and higher reliability/performance/security than they would if they tried to operate it themselves.  An analogy would be outsourcing the operation of an email agent to Gmail or Hotmail.

<a name="contract-create"></a>
### Creating a Contract

A Tokenized contract is formed when the administration of a token issuer presents a valid [Contract Offer](../protocol/actions#action-contract-offer) action to a smart contract. The smart contract checks only that the rules proposed in the offer are compliant with its logic, but the legal and regulatory aspects of dealing with the assets being created must be pre-determined and managed by the administration to ensure the contract operates within all applicable laws and regulations.

#### Contract Offer

To create a [Contract Offer](../protocol/actions#action-contract-offer), the Contract administration must prepare an action that contains all of the required information such as:

- Contract name
- Governing Law
- Jurisdiction
- Contract rules, voting systems
- Detail of the issuing entity/entities including key personnel, addresses etc.

The Contract Offer action must be signed by both the administration and the smart contract operator, so the administration first builds a template transaction which it sends to the smart contract operator:

![A contract offer action template](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action-template.svg?sanitize=true "Contract Offer Action Template") {.frame .centered .padded}

If the contract meets the smart contract operator's requirements, they will add an input from their own wallet, add the change outputs they need and sign the Contract Offer using `SIGHASH_ALL` before sending it back to the administration. Once the administration has reviewed the smart contract operator's changes, they can sign their own input (or inputs) using `SIGHASH_ALL` and send the transaction onto the network.

![Final contract offer action](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action.svg?sanitize=true "Contract Offer Action Transaction") {.frame .centered .padded}

#### Contract Formation

When the smart contract receives the Offer action it unpacks the information and evaluates it. If the smart contract decides there are no issues, it builds a [Contract Formation](../protocol/actions#action-contract-formation) action in response which is sent onto the network. The Contract Formation action contains a complete repeat of all of the information in the Contract Offer action as an acknowledgement that the smart contract has accepted the setup as valid.

The contract also adds two additional fields

- **Timestamp** - The time at which the smart contract built the Contract Formation action
- **ContractRevision** - Set to zero for a new contract. Increments by 1 each time the contract is updated

![Contract Formation action](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action.svg?sanitize=true "Contract Formation Action Transaction") {.frame .centered .padded}

<a name="contract-update"></a>
### Updating a Contract

The amendment of a Tokenized contract can be simple when the rules or conditions being changed are able to be amended without needing a vote. This is called a unilateral amendment and is comprised of the [Contract Amendment](../protocol/actions#action-contract-amendment) and [Contract Formation](../protocol/actions#action-contract-formation) actions.

Where a Contract Amendment seeks to make changes that require a vote through a referendum or an initiative, there is no longer a unilateral amendment since the rules of the vote determine the outcome of the Contract Amendment.

#### Contract Amendment

If the issuer wants to change the issuer address (e.g. in the event of a contract being sold) or to change the operator address (to move to a new service provider) there are flags for these options. The smart contract receives the new addresses for these contracts from signed inputs paying into the transaction carrying the [Contract Amendment](../protocol/actions#action-contract-amendment) action.

Following on from these flags is the new contract revision, which is incremented by 1 each time the contract is updated. A Contract Amendment request that has a version number that isn't in sequence will be rejected.
Subsequent to these fields, amendments to the contract are contained in an array of objects, each of which has the following information:

- The field index of the contract element being changed
- The element of the field (for to identify the index number of the element within an array - complex types only)
- The Sub Field Index (to identify the field within the object in the array - complex types only)
- An instruction on whether to add or delete an element (for arrays)
- The new data being placed into the specified index

For amendments that require a vote to be passed, the TXID of a Result action showing a positive vote outcome for the change must be added as the final data item in the Contract Amendment action.

![Contract Amendment action](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-amendment-action.svg?sanitize=true "Contract Amendment Action Transaction") {.frame .centered .padded}

#### Contract Formation

When the contract sees the [Contract Amendment](../protocol/actions#action-contract-amendment) action land in its wallet, it evaluates the action and looks to ensure that the modifications are valid.
If the contract determines that the amendment is valid, it issues a full [Contract Formation](../protocol/actions#action-contract-formation) action including the full details of the contract, the updated version number and a new timestamp.

From this moment, all transaction requests to the contract must abide by the amended rules.

![Updated Contract Formation action](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action-amendment.svg?sanitize=true "Contract Formation Action Transaction") {.frame .centered .padded}

<a name="contract-address-change"></a>
### Contract Address Change

It is very important when hosting a smart contract that the private key is not compromised. If it is, then someone could break the rules of the contract, steal tokens, and just generally wreak havoc on all participants.

In the worst case scenario, in which the private key of the contract is compromised, there is a recovery option. This requires changing the contract private key and thereby changing the address. This requires that the contract was created with a "master" address specified. The private key for the "master" address should be kept in cold storage because if it is compromised, then there is no recovery. A [Contract Address Change](../protocol/actions#action-contract-address-change) message signed by the "master" key can be sent to the current contract address. This message specifies a new contract address that will be required for all future request messages.

![A contract address change action template](https://raw.githubusercontent.com/tokenized/docs/master/images/contract-address-change-action.svg?sanitize=true "Contract Address Change Action Template") {.frame .centered .padded}

<a name="static-contracts"></a>
## Static Contracts

A static contract is a legal contract similar to that which one would enter into today for the undertaking of a scope of work, to enter into a non-disclosure agreement, or to manage the sale of an off-chain asset that has not been tokenized. A static contract uses the [Static Contract Formation](../protocol/actions#action-static-contract-formation) action.

The static contract framework simply provides an easy and low-cost way for inscribing the details of these contracts onto the public ledger so the contracting parties benefit from the value of the Bitcoin network. Static contracts require only a single action to be established and do not require a Tokenized smart contract to operate.  Each of the contracting parties adds a signed input to the same transaction that has the static contract formation action in it, to allow for their signatures (intention) to be recorded to the contract.

![Updated Static Contract Formation action](https://raw.githubusercontent.com/tokenized/docs/master/images/static-contract-formation-action.svg?sanitize=true) {.frame .centered .padded}

<a name="contract-law"></a>
## Contract Law

The Tokenized Protocol ensures that all valid contracts follow the principles and conventions of contract law.  While there is some variation worldwide the basic core concepts of a contract are fairly universal.  For the purposes of the analysis in this document, the Tokenized Protocol has been examined using Australian contract law as the model, which is based on English common law. Contract administrations should always seek proper legal advice to ensure that they comply with the laws in their jurisdiction.

<a name="contract-formation"></a>
### Contract Formation

There are five essential elements necessary for legally binding Contract Formation:
- Agreement between the parties
- Consideration (a bargain requirement: generally, the supply of money, property or services or a promise to undertake, or not undertake a particular act in exchange for something of value)
- Capacity to enter legal relations (e.g. of sound mind and legal age)
- Intention by the parties to enter into legal relations (private non-commercial agreements between family members may not indicate intention to enter a legally binding contract and therefore may not be enforceable)
- Certainty (the contract has to be complete, certain, clear and binding)

Reference: J W Carter, LexisNexis, Carter on Contract (at July 2013) [Chapter 1]

<a name="agreement"></a>
#### Agreement
The agreement criteria of contract law is satisfied in the Tokenized Protocol by way of the information specified by the Contract Formation action, the Asset Creation action, the written agreement, and the Transfer and Settlement actions.  The existence of an agreement is analyzed through the rules of ‘offer and acceptance’.  In the case of a token contract, the issuer (the offerer) produces an offer (Contract Formation, Asset Creation) and the investor (the offeree) accepts the offer by way of an exchange (bitcoin for token(s)) or swap (token(s) for token(s)) type Transfer action.  A send type Transfer action is like a standard Bitcoin transaction in that it only requires sign-off by the token sender, and no on-chain consideration is required, therefore the offeree does not sign-off on the transaction and may not agree to accept the tokens being sent.  Typically a send type action is accompanied by on-chain or off-chain receipt, invoice or some other document that records the transfer of real world goods or services in consideration for the payment of tokens or bitcoin.

<a name="consideration"></a>
#### Consideration
Consideration will always be present in an exchange or swap type of Transfer action in the form of either a token or bitcoin.  Exchanges require a contracting party to provide bitcoin in return for their token(s).  Swaps have contracting parties swap tokens for other tokens directly without any bitcoin except for what is needed to pay any transaction fees.  The consideration criteria of a legally-binding contract will also be published on-chain in a Settlement transaction where the contract actually dispenses the bitcoin and token(s) to the contracting parties involved in the transfer.  

<a name="capacity"></a>
#### Capacity
Capacity will be handled by the smart contracts and the use of Identity Oracles that contain whitelisted public addresses.  These whitelisted addresses get added to the whitelist only when KYC/AML compliance checks have been completed.  The smart contract will not allow any transactions to go through that break the terms and conditions of the contract which are created in accordance with the choice of law selected for the contract.  Other capacity issues relating to being ‘of sound mind’ (e.g. intoxication) cannot be effectively managed by the Tokenized Protocol, but that is true of any online commercial interaction.

<a name="intention"></a>
#### Intention
Intention is traditionally handled by context, language and a signature by all relevant contracting parties.  For most token use cases the context will be supplied by the actual written agreement, and the descriptions and labels of the token.  Generally, a contracting party who is looking to buy a share in a company recognizes that the share is part of a commercial-agreement.  The Tokenized Protocol also uses carefully chosen terminology for the various actions and metadata fields to make the intention of the actions extremely clear to all that use it.  The language is precise and adheres to the concept of terms having their ordinary meaning to remove the potential for misunderstanding.  Most tokens will be accompanied by a written agreement and/or supporting documentation that will have handwritten signatures of the administration of the contract issuer and any relevant contracting parties.  However, most token owners will signal their intent to be bound to a legally-binding contract using a digital signature generated by their private key that is associated with the public key that holds the tokens.  The Tokenized Protocol recognizes the digital signatures of the contracting parties - in the input addresses of the Bitcoin transaction that contains the Tokenized action - as intent by the contracting parties.

<a name="certainty"></a>
#### Certainty
Certainty is captured in the formalized and standardized metadata of the Tokenized actions.  All of the important aspects of the contract are detailed and must be included for it to be considered a valid Tokenized action.  The Tokenized Protocol does not have control over the actual written agreement and there can be some uncertainty as to whether the written agreement is legally binding in this capacity, but this may be true of all contracts.  Users will have to be vigilant with the contracts they enter into and should always seek professional legal advice if they are uncertain of a contract’s effect.
