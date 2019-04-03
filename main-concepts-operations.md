# Tokenized Protocol Operations

The Tokenized protocol operates on a request and response mechanism where operations are carried out in 2 steps (except Message and Registry), called 'actions'.  The request and response actions are always initiated by two different entities, the requester, which can be the issuer, user or contract operator (on behalf of the issuer), and the responder, which is the smart contract. Each request action is sent to the blockchain by a user or issuer, and must be subsequently confirmed as valid by the smart contract. A response action is a 3-step process which is as follows:

1. Receive and unpack message
2. Evaluate action instruction with respect to the contract rules and state
3. Create and send response

Responses to messages are also sent on-chain. A response is either a confirmation of the action requested, or a rejection message. All confirmation actions result in some change to the state, rules or terms of the contract.  All response actions also have a timestamp embedded in the payload that represents the time that the smart contract first saw and processed the corresponding request action.  These timestamps can be used for rebuilding the contract's state from the blockchain, even if there have been block reorganizations. 

## Operations

The protocol is comprised of 25 separate action messages which are broken up into 7 groups as defined below. With these actions, Tokenized provides all of the tools required for the issuance, management and exchange of any type of digitized asset that can be created.

### 1. Contract Operations

Contract operations are used to establish and modify smart contracts that are operated by a smart contract. Contract operations are made up of the following 4 actions:

* [Contract Offer](../protocol/contract-offer) (Action Code: C1)
* [Contract Formation](../protocol/contract-formation) (Action Code: C2)
* [Contract Amendment](../protocol/contract-amendment) (Action Code: C3)
* [Static Contract Formation](../protocol/static-contract-formation) (Action Code: C4)

### 2. Asset Operations

Asset operations are used to create and manage the assets that the smart contract controls. The asset actions are as follows:

* [Asset Definition](../protocol/asset-definition) (Action Code: A1)
* [Asset Creation](../protocol/asset-creation) (Action Code: A2)
* [Asset Modification](../protocol/asset-modification) (Action Code: A3)

### 3. Transfer Operations

Transfer operations are used to move assets from the control of one address to another. A transfer instruction is sent to the smart contract which responds with either a Settlement action, or a Rejection message.

* [Transfer](../protocol/transfer) (Action Code: T1)
* [Settlement](../protocol/settlement) (Action Code: T2)

### 4. Governance Operations

Governance operations allow the issuer and asset owners to manifest changes in the smart contract rules, terms or state through binding votes created by Proposal actions.

* [Proposal](../protocol/proposal) (Action Code: G1)
* [Vote](../protocol/vote) (Action Code: G2)
* [Ballot Cast](../protocol/ballot-cast) (Action Code: G3)
* [Ballot Counted](../protocol/ballot-counted) (Action Code: G4)
* [Result](../protocol/result) (Action Code: G5)

### 5. Enforcement Operations

Enforcement operations provide the issuer the tools required to carry out enforcement orders.  These enforcement orders can be at the direction of legal/law enforcement authorities, or simply due to the issuer's own rules or wishes.  The instructions include fields to include records of enforcement instructions received from authorities (eg. court orders/warrants) to establish the justification for each enforcement order.  Enforcement operations will likely work in coordination with authorities and KYC registries that link identities to addresses.

* [Order](../protocol/order) (Action Code: E1)
* [Freeze](../protocol/freeze) (Action Code: E2)
* [Thaw](../protocol/thaw) (Action Code: E3)
* [Confiscation](../protocol/confiscation) (Action Code: E4)
* [Reconciliation](../protocol/reconciliation) (Action Code: E5)

### 6. Registry Operations

Registry operations allow a user or issuer to set up and manage on-chain registers which can be used for any purpose.  Registers do not require a smart contract.

* [Establishment](../protocol/establishment) (Action Code: R1)
* [Addition](../protocol/addition) (Action Code: R2)
* [Alteration](../protocol/alteration) (Action Code: R3)
* [Removal](../protocol/removal) (Action Code: R4)

### 7. Message Operations

Message operations allow entities to communicate with each other on-chain. No response is required and the smart contract does not need to be involved.  Messages are used to communicate all types of information, but do not alter the state, rules or terms of the contract and do not require a contract at all.  Messages are categorized into different Message Types which are distinct in the structure of payload fields. The "Rejection" action is used by the smart contract to reject any actions that do not comply with the rule set in place for the asset the request relates to.

* [Message](../protocol/message) (Action Code: M1)
* [Rejection](../protocol/rejection) (Action Code: M2)
