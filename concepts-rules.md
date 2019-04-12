# Rules

- [General](#general)
- [Contract Operations](#contract-operations)
- [Asset Operations](#asset-operations)
- [Transfer Operations](#transfer-operations)
- [Governance Operations](#governance-operations)
- [Enforcement Operations](#enforcement-operations)
- [Message Operations](#message-operations)
- [Registry Operations](#registry-operations)

The following lays out a set of rules applicable to different aspects of the tokenized protocol.

<a name="general"></a>
## General

* All contract actions must be cash flow neutral. The request action must include enough bitcoin to pay for all costs (dust, contract fees, exchange fees, mining fees, etc.) required to generate a response action. In cases where not enough bitcoin has been included, no response action will take place. 

* Smart contracts maintain a small resevoir of satoshis (small multiple of the dust value) at the contract address to use to send back to itself on contract-wide actions.  This resevoir will not deplete over time, as all fees will be paid for by the requester.

* Every contract-initiated action must be in response to a user/issuer-initiated action. No contract-initiated action will be valid without a preceding ‘request’ action initiated by a user or issuer.

* All Tokenized actions must be sent to or from a contract’s public address. The contract’s public address is what connects all associated token actions. The only exceptions to this rule are the Messaging action (M1), the Registry actions (R1 - R4) and the Static Contract Formation action (C4).  All of which operate independently of any smart contract. Therefore, for a wallet to track a token, all it has to do is add the token contract’s public address as a watch-only address and monitor for relevant actions.

* Where a contract operator has been nominated in the Contract Formation action, the contract operator's address will be treated by the smart contract as identical to the issuer's address for the initiation of all request actions.  However, the contract operator cannot transfer tokens that are not held by the contract operator's address.

* Only one Tokenized action per Bitcoin transaction, with the exception of the Message action (M1) which can be included in transactions with other Tokenized actions and in an unlimited quantity.

* The Tokenized action should always be the last output.

* If a request action is sent to the smart contract, but is invalid and the RETURN payload is malformed in such a way as it is impossible to determine which inputs to refund in the Rejection message, then the refunded bitcoin will be sent to the issuer's address. 

<a name="contract-operations"></a>
## Contract Operations

1. Every token must have a valid Contract Formation action to be considered a valid token by the protocol.
2. Every Contract Formation action must be preceded by a Contract Offer action except for in the case of static contracts - i.e. no smart contract involved.
3. The first Contract Offer and Contract Formation actions are considered to be the only valid Contract operations for a particular contract address. Any subsequent Contract Offers sent to the contract address will be ignored. There can be only one Contract Offer and one Rev. 0 Contract Formation per contract address. (When contract’s are amended the Contract Formation action increments the revision sub-field by one. Rev. 0 -> Rev. 1. The highest revision is always taken as the current one.)
4. Additional Contract Formation actions (revisions) are only valid if there is a preceding Contract Amendment action from the issuer or the contract operator, if there is one.
5. The first Contract Offer action determines the issuer’s public address and only one issuer per contract address is valid.

<a name="asset-operations"></a>
## Asset Operations

1. Every token must have an Asset Creation action to be considered a valid token by the protocol. Asset Creation actions define the properties of the token.
2. Every Asset Creation action must be preceded by a Contract Formation action.
3. All Asset Creation actions must be preceded by a Asset Definition action.
4. The Asset Definition action must come from the issuer’s address, which is set by the input address on the valid Contract Offer action.
5. Only one Asset Creation (Rev.0) action can exist per AssetID, per Contract address.
6. All additional revisions of an Asset Creation action must be preceded by an Asset Modification action initiated by the issuer’s public address.
7. A contract’s public address can have an unlimited number of Asset Creation actions but each one must have a unique Asset ID. This property allows for a practically unlimited amount of non-fungible assets to be associated and controlled by each smart contract.
8. The first Asset Creation action assigns the ownership of all tokens created to the issuer.
9. Any changes to the qty of tokens for a given asset is account for by the issuer's balance.  If tokens are burned (Asset Modification), they can only be burned up to the quantity held by the issuer at the time of Asset Modification action.  If new tokens are created, then the new tokens are automatically assigned to the issuer's address.
10. Asset ID's (Asset ID = Asset Type + base58(Asset Code + checksum)) cannot be modified.

<a name="transfer-operations"></a>
## Transfer Operations

1. All Transfer operations must be in reference to an Asset ID specified by a valid Asset Creation action.
2. All Transfer actions must be responded to by a succeeding Settlement action or a Rejection message.
3. If transfer restrictions have been placed upon an asset after a token holder legitimately took possession of it, then the token holder will still be able to transfer the tokens away.  The smart contract assumes that if an address holds a token, then it was approved by the smart contract with the rules that were relevent at the time of the transfer.

<a name="governance-operations"></a>
## Governance Operations

1. All Vote actions must be preceded by a Proposal action.
2. A Ballot Cast action is only valid if it is cast during a vote period. The vote period is defined by the Vote action timestamp, and the Vote Cut-Off Timestamp specified in the Order action.
3. Ballot Cast actions must be responded to by a Ballot Counted action if valid, or a Rejection action if invalid.
4. Result actions must have a preceding Vote action.
5. Votes cannot be traded away after a Vote has started.  If a token is traded after a vote has started, then that token will lose the ability to vote for that vote, regardless of whether a ballot was cast with that token before it was transferred.

<a name="enforcement-operations"></a>
## Enforcement Operations

1. All Enforcement actions must be preceded by an Order action.
2. A Freeze action alerts the affected token owner that the smart contract will be unable to respond to any actions with a affirmative response action (Settlement, Ballot Counted, etc.). All actions will be responded to with a Rejection message.
3. Votes submitted by a token owner whose account is frozen will not be counted.
4. A frozen address can only be unfrozen by a Thaw action.
5. Thaw actions that are not directed at a frozen address will be ignored.
6. Confiscation actions that are not directed at an address with tokens will be rejected.
7. Reconciliation actions will decrement the tokens of the specified type at the targeted address to ensure that the number of outstanding tokens issued by the issuer is maintained across the state of the blockchain. Chained token transfer actions that are broken can result in additional tokens in the system that need reconciling.
8. A Thaw action always references a specific Freeze action and removes its effect from the address(es).
9. Multiple Freeze actions can be placed on an address.
10. Freeze actions can only be undone through a Thaw or a Confiscation action. 

<a name="message-operations"></a>
## Message Operations

1. Message actions can be from any address to any other address(es).
2. Rejection actions are the negative response from a smart contract to indicate that another action is not valid. Actions that have a Rejection action as a response are ignored by the protocol.

<a name="registry-operations"></a>
## Registry Operations

1. All Registry operations that come before an Establishment action are ignored.
2. All Addition actions must be preceded by an associated Establishment action.
3. All Alteration actions must be preceded by an associated Addition action.
4. All Removal actions must be preceded by an associated Addition action.
