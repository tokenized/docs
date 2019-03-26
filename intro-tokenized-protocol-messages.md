# Tokenized Protocol Messages

The tokenized protocol builds upon the original Tokeda Token management system defined by Joannes Vermorel. It is what is called a Request/Response protocol where each request action is sent onto the blockchain and must be subsequently confirmed as valid by a Tokenized smart contract agent. Confirmation is a 3 step process which is as folows:

1. Receive and unpack message
2. Evaluate message instruction in terms of contract rules
3. Create and send response

Responses to messages are also sent on-chain. A response is either a confirmation of the action requested, or a rejection message. Any confirmations that make material changes to the contract which need to be evaluated in-order for the contract state to be recalculated also contain embedded timestamps such that the true state of the contract can be truthfully established in the event of a blockchain re-organisation.

## Messages

The protocol is comprised of 26 separate action messages which are broken up into 7 groups as defined below. With these actions, Tokenized provides a complete platform for the issuance, management and use of any type of digitized asset that can be created.

### 1. Contract actions

Contract actions are used to establish and modify smart contracts that are operated by a smart contract agent. The contract actions are as follows:

* [Contract Offer](../protocol/contract-offer)
* [Contract Formation](../protocol/contract-formation)
* [Contract Amendment](../protocol/contract-amendment)
* [Static Contract Formation](../protocol/static-contract-formation)

### 2. Asset actions

Asset actions are used to create and manage the assets that the contract agent controls. The asset actions are as follows:
* [Asset Definition](../protocol/asset-definition)
* [Asset Creation](../protocol/asset-creation)
* [Asset Modification](../protocol/asset-modification)

### 3. Transfer actions

Transfer actions are used to move assets from the control of one address to another. A transfer instruction is sent to the Smart Contract agent which responds with either a settlement action, or a rejection message.

* [Transfer](../protocol/transfer)
* [Settlement](../protocol/settlement)

### 4. Governance actions

Governance actions allow the issuer and asset owners to manifest changes in the smart contract rules through binding votes created by referendum and initiative actions.

* [Initiative](../protocol/initiative)
* [Referendum](../protocol/referendum)
* [Vote](../protocol/vote)
* [Ballot Cast](../protocol/ballot-cast)
* [Ballot Counted](../protocol/ballot-counted)
* [Result](../protocol/result)

### 5. Enforcement actions

Enforcement actions allow the token issuer or any user with enforcement permissions to conduct enforcement actions on the assets managed by the Smart Contract. The instructions include fields to include records of enforcement instructions received from authorities to establish the reason for each action.

* [Result](../protocol/result)
* [Order](../protocol/order)
* [Freeze](../protocol/freeze)
* [Thaw](../protocol/thaw)
* [Confiscation](../protocol/confiscation)
* [Reconciliation](../protocol/reconciliation)

### 6. Registry actions

Registry actions allow a contract issuer to set up and manage whitelists and blacklists for contracts that require KYC records to be managed for trade. When a KYC registry is in use for a particular asset, only users who have been recorded as eligible in the registry will be permitted to hold or exchange that asset.

* [Establishment](../protocol/establishment)
* [Addition](../protocol/addition)
* [Alteration](../protocol/alteration)
* [Removal](../protocol/removal)

### 7. Message actions

The "Message" action allow users of a smart contract to exchange messages between themselves or the asset issuer. The "Rejection" action is used by the smart contract to reject any actions that do not comply with the rule set in place for the asset the request relates to.

* [Message](../protocol/message)
* [Rejection](../protocol/rejection)
