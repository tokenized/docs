# Tokenized Protocol Documentation
The tokenized protocol builds upon the original Tokeda Token management system defined by Joannes Vermorel. It is what is called a fire and forget protocol where each token operation is sent onto the blockchain and must be subsequently confirmed as valid by a Tokenized smart contract agent. Confirmation is a 3 step process which is as folows:
1. Receive and unpack message
2. Evaluate message instruction in terms of contract rules
3. Create and send response
Responses to messages are also sent on-chain. A response is either a confirmation of the action requested, or a rejection message. Any confirmations that make material changes to the contract which need to be evaluated in-order for the contract state to be recalculated also contain embedded timestamps such that the true state of the contract can be truthfully established in the event of a blockchain re-organisation.

##Messages
The protocol is comprised of 29 separate action messages which are broken up into 7 groups as defined below.
###1. Contract actions
Contract actions are used to establish and modify smart contracts that are operated by a smart contract agent. The contract actions are as follows:
* <a href="../protocol/contract-offer">Contract Offer</a>
* <a href="../protocol/contract-formation">Contract Formation</a>
* <a href="../protocol/contract-amendment">Contract Amendment</a>
* <a href="../protocol/static-contract-formation">Static Contract Formation</a>

###2. Asset actions
Asset actions are used to create and manage the assets that the contract agent controls. The asset actions are as follows:
* <a href="../protocol/asset-definition">Asset Definition</a>
* <a href="../protocol/asset-creation">Asset Creation</a>
* <a href="../protocol/asset-modification">Asset Modification</a>

###3. Transfer actions
Transfer actions are used to move assets from the control of one address to another. A transfer instruction is sent to the Smart Contract agent which responds with either a settlement action, or a rejection message. 
* <a href="../protocol/transfer">Transfer</a>
* <a href="../protocol/settlement">Settlement</a>

###4. Governance actions
Governance actions allow the issuer and asset owners to manifest changes in the smart contract rules through binding votes created by referendum and initiative actions.
* <a href="../protocol/initiative">Initiative</a>
* <a href="../protocol/referendum">Referendum</a>
* <a href="../protocol/vote">Vote</a>
* <a href="../protocol/ballot-cast">Ballot Cast</a>
* <a href="../protocol/ballot-counted">Ballot Counted</a>
* <a href="../protocol/result">Result</a>

###5. Enforcement actions
Enforcement actions allow the token issuer or any user with enforcement permissions to conduct enforcement actions on the assets managed by the Smart Contract. The instructions include fields to include records of enforcement instructions received from authorities to establish the reason for each action.
* <a href="../protocol/result">Result</a>
* <a href="../protocol/order">Order</a>
* <a href="../protocol/freeze">Freeze</a>
* <a href="../protocol/thaw">Thaw</a>
* <a href="../protocol/confiscation">Confiscation</a>
* <a href="../protocol/reconciliation">Reconciliation</a>

###6. Registry actions
Registry actions allow a contract issuer to set up and manage whitelists for contracts that require KYC records to be managed for trade. When a registry is in use for a particular asset, only users who have been recorded in the registry will be permitted to hold or exchange that asset.
* <a href="../protocol/establishment">Establishment</a>
* <a href="../protocol/addition">Addition</a>
* <a href="../protocol/alteration">Alteration</a>
* <a href="../protocol/removal">Removal</a>

###7. Message actions
The "Message" action allow users of a smart contract to exchange messages between themselves or the asset issuer. The "Rejection" action is used by the smart contract to reject any actions that do not comply with the rule set in place for the asset the request relates to. 
* <a href="../protocol/message">Message</a>
* <a href="../protocol/rejection">Rejection</a>

With these actions, Tokenized provides a complete platform for the issuance, management and use of any type of digitized asset that can be created. 