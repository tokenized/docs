# Operations

- [Introduction](#introduction)
- [All Operations](#all-operations)
  - [Contract Operations](#contract-operations)
  - [Asset Operations](#asset-operations)
  - [Transfer Operations](#transfer-operations)
  - [Governance Operations](#governance-operations)
  - [Enforcement Operations](#enforcement-operations)
  - [Registry Operations](#registry-operations)
  - [Message Operations](#message-operations)
- [Order of Operations](#operation-order)

<a name="introduction"></a>
## Introduction

The Tokenized Protocol operates on a _request and response_ mechanism whereby operations are carried out in 2 steps called [actions](../protocol/actions#action-actions).  The only exceptions to this rule are the [Message](../protocol/actions#action-actions#action-message) action and the [Registery](../protocol/actions#action-actions#action-addition) actions where each action does not work on the request and response model. They are 1 step actions where no response is required.

The request and response actions are always initiated by two different classes of actors, the requester and the responder, and the definitions are as follows:

- **Requester**: the issuer, user or contract operator (on behalf of the issuer)

- **Responder**: the smart contract instance

The smart contract is an autonomous agent that listens to the Bitcoin (BSV) network for commands (request actions) addressed to it from users and issuers. It does not publish any actions to the blockchain without first being prompted by a request action from the requesting party. Each request action that is sent to the blockchain by a user or issuer, must be subsequently confirmed as valid, or invalid (rejected) by the smart contract. The smart contract is the only entity with the ability to directly modify the contract or the assets it controls. 

A response action is a 3-step process which is as follows:

1. Receive and unpack message

2. Evaluate action instruction with respect to the contract rules/terms and conditions and state (eg. token balances at addresses, token freezes, etc.)

3. Create and send response

Responses to messages are also sent on-chain. A response is either a confirmation of the action requested, or a Rejection message. All confirmation actions result in some change to the state, rules or terms of the contract.  All response actions also have a timestamp embedded in the payload that represents the time that the smart contract first saw and processed the corresponding request action.  These timestamps can be used for rebuilding the contract's state from the blockchain, even if there have been block reorganizations. 

When the contract finds that a request is in breach of the rules/T&C's that govern that contract, it will respond with a Rejection message. At this point it is up to the user's wallet to notify them of the rejection and for them to re-attempt the action in accordance with the rules. Most wallets that are configured to work with the Tokenized Protocol, will be able to prevent users from sending actions that do not meet the contract's requirement. For this reason, Rejection messages are expected to be rare.

<a name="all-operations"></a>
## All Operations

The protocol is comprised of 25 separate action messages which are broken up into 7 groups as defined below. With these actions, Tokenized provides all of the tools required for the issuance, management and exchange of any type of digital asset that can be created.

<a name="contract-operations"></a>
### Contract Operations

Contract operations are used to establish and modify smart contracts that are operated by a smart contract. Contract operations are made up of the following 4 actions:

* [Contract Offer](../protocol/actions#action-contract-offer) (Action Code: C1)
* [Contract Formation](../protocol/actions#action-contract-formation) (Action Code: C2)
* [Contract Amendment](../protocol/actions#action-contract-amendment) (Action Code: C3)
* [Static Contract Formation](../protocol/actions#action-static-contract-formation) (Action Code: C4)

<a name="asset-operations"></a>
### Asset Operations

Asset operations are used to create and manage the assets that the smart contract controls. The asset actions are as follows:

* [Asset Definition](../protocol/actions#action-asset-definition) (Action Code: A1)
* [Asset Creation](../protocol/actions#action-asset-creation) (Action Code: A2)
* [Asset Modification](../protocol/actions#action-asset-modification) (Action Code: A3)

<a name="transfer-operations"></a>
### Transfer Operations

Transfer operations are used to move assets from the control of one address to another. A transfer instruction is sent to the smart contract which responds with either a Settlement action, or a Rejection message.

* [Transfer](../protocol/actions#action-transfer) (Action Code: T1)
* [Settlement](../protocol/actions#action-settlement) (Action Code: T2)

<a name="governance-operations"></a>
### Governance Operations

Governance operations allow the issuer and asset owners to manifest changes in the smart contract rules, terms or state through binding votes created by Proposal actions.

* [Proposal](../protocol/actions#action-proposal) (Action Code: G1)
* [Vote](../protocol/actions#action-vote) (Action Code: G2)
* [Ballot Cast](../protocol/actions#action-ballot-cast) (Action Code: G3)
* [Ballot Counted](../protocol/actions#action-ballot-counted) (Action Code: G4)
* [Result](../protocol/actions#action-result) (Action Code: G5)

<a name="enforcement-operations"></a>
### Enforcement Operations

Enforcement operations provide the issuer the tools required to carry out enforcement orders.  These enforcement orders can be at the direction of legal/law enforcement authorities, or simply due to the issuer's own rules or wishes.  The instructions include fields to include records of enforcement instructions received from authorities (eg. court orders/warrants) to establish the justification for each enforcement order.  Enforcement operations will likely work in coordination with authorities and KYC registries that link identities to addresses.

* [Order](../protocol/actions#action-order) (Action Code: E1)
* [Freeze](../protocol/actions#action-freeze) (Action Code: E2)
* [Thaw](../protocol/actions#action-thaw) (Action Code: E3)
* [Confiscation](../protocol/actions#action-confiscation) (Action Code: E4)
* [Reconciliation](../protocol/actions#action-reconciliation) (Action Code: E5)

<a name="registry-operations"></a>
### Registry Operations

Registry operations allow a user or issuer to set up and manage on-chain registers which can be used for any purpose.  Registers do not require a smart contract.

* [Establishment](../protocol/actions#action-establishment) (Action Code: R1)
* [Addition](../protocol/actions#action-addition) (Action Code: R2)
* [Alteration](../protocol/actions#action-alteration) (Action Code: R3)
* [Removal](../protocol/actions#action-removal) (Action Code: R4)

<a name="message-operations"></a>
### Message Operations

Message operations allow entities to communicate with each other on-chain. No response is required and the smart contract does not need to be involved.  Messages are used to communicate all types of information, but do not alter the state, rules or terms of the contract and do not require a contract at all.  Messages are categorized into different Message Types which are distinct in the structure of payload fields. The "Rejection" action is used by the smart contract to reject any actions that do not comply with the rule set in place for the asset the request relates to.

* [Message](../protocol/actions#action-message) (Action Code: M1)
* [Rejection](../protocol/actions#action-rejection) (Action Code: M2)

<a name="operation-order"></a>
## Order of Operations

For a complete list of the different action types, and the applicable responses, please see the image below.

![Order of Operations](https://raw.githubusercontent.com/tokenized/docs/master/images/order-of-operations.svg?sanitize=true) {.frame .centered}
