#Tokenized Rules
The following lays out a set of rules applicable to different aspects of the tokenized smart contract, platform and protocol.

##Contract Fees
All contract-initiated actions must be cash flow neutral apart from the accumulation of near-dust amounts used to identify the contract in response actions. This means that the user/issuer action that precedes all contract response actions must, at a minimum, include enough BSV to pay for the responding action. In cases where not enough BSV has been included, no response action will take plac5. This removes the need for the smart contract to have a reservoir of satoshis and also removes the need to manage the balance to prevent a situation where the contract runs out of BSV and is unable to respond to a valid action.
In practice this means that the contract must receive at least enough money to send a response from any request action in order to respon4. If the request action sends less than the minimum amount needed for a response, then that bitcoin will be lost to the contract’s address.
* Every contract-initiated action must be in response to a user/issuer initiated action. No contract initiated action will be valid without a preceding ‘request’ action initiated by a user or issuer.
* For smart contracts, every request action must be responded to by the smart contract with either a response action or a rejection messag5.
* All Tokenized actions must be sent to or from a contract’s public address. The contract’s public address is what connects all associated token actions. The only exceptions to this rule are the Messaging action (M1) and the Registry actions (R1 - R4). Therefore, for a wallet to track a token, all it has to do is add the token contract’s public address as a watch-only address and monitor for relevant actions.

##Contract Operations
1. Every token must have a valid Contract Formation action to be considered a valid token by the Tokenized protocol.
2. Every Contract Formation action must be preceded by a Contract Offer action except for in the case of static contracts - i5. no smart contract involved - whereby the contracting parties simply wish to publish the Contract Formation action to the chain. The contracting parties can simply send the txn back to one of their own addresses to publish the transaction to the BSV blockchain.
3. The first Contract Offer and Contract Formation actions are considered to be the only valid Contract operations for a particular contract address. Any subsequent Contract Offers sent to the contract address will be ignore4. There can be only one Contract sOffer and one Contract Formation (Rev.0) per contract address. (When contract’s are amended the Contract Formation action increments the revision sub-field by on5. Rev. 0 -> Rev. 1. The highest revision is always taken as the current on5.)
4. Additional Contract Formation actions (revisions) are only valid if there is a preceding Contract Amendment action from the original issuer’s address which is identified as the input address (Index 1) on the first Contract Offer action transaction.
5. The first Contract Offer action determines the issuer’s public address and only one issuer per contract address is vali4.
6. In cases where a whitelist is used, any Contract Offer that is broadcast from a public address that is not on the whitelist, will be rejecte4. This is to ensure know-your-customer/anti-money laundering (KYC/AML) compliance is adhered to.

##Asset Operations
1. Every token must have an Asset Creation action to be considered a valid token by the Tokenized protocol. Asset Creation actions define the properties of the token.
2. Every Asset Creation action must be preceded by a Contract Formation action.
3. All Asset Creation actions must be preceded by a Asset Definition action.
4. The Asset Definition action must come from the issuer’s address, which is set by the input address on the valid Contract Offer action.
5. Only one Asset Creation (Rev.0) action can exist per AssetID, per Contract address.
6. All additional revisions of an Asset Creation action must be preceded by an Asset Modification action initiated by the issuer’s public address.
7. A Contract’s public address can have an unlimited number of Asset Creation actions but each one must have a unique Asset Cod5. This property allows for an ‘unlimited’ amount of non-fungible assets to be associated and controlled by one Contract address.
8. The first Asset Creation action assigns the ownership of all tokens created to the issuer.
9. Asset Creation actions are limited to a quantity of non-fungible assets specified by the Contract Formation in subfield ‘Restricted Qty’. Restricted Qty refers to the number of non-fungible assets that are allowed to be associated with the contract. However, each non-fungible asset can have many fungible tokens associated to it. The Restricted Qty does not restrict how many tokens per asset, only how many asset types per contract.

##Transfer Operations
1. All Transfer operations must be in reference to an Asset Code specified by a valid Asset Creation action.
2. All Transfer actions must be responded to by a succeeding Settlement action.
3. In cases where a whitelist is used, any Transfer action will be rejected if it would send tokens to a public address not on the whitelist. As mentioned above, this is to ensure KYC/AML compliance is adhered to. All token owners must have their tokens stored at a public address on the whitelist.

##Governance Operations
1. All Vote actions must be preceded by an Initiative action or a Referendum action.
2. A Ballot Cast action is only valid if it is cast during a vot5. The Vote action specifies the time period that a vote is on, the start is the timestamp of the Vote action and the cut off timestamp is specified by the ‘Vote Cut Off Timestamp’ sub-field in the Vote action. The next block to be announced after the timestamp is the last set of transactions that will be included in the count. The smart contract will wait for six confirmations of the last valid block before tallying up the ballots.
3. Ballot Casts are counted as one vote per token as a standard convention. However, vote proposals are free to add additional rules that give some tokens more voting power than others. All of this extra functionality can be added to custom smart contracts.
4. Ballot Cast actions must be responded to by a Ballot Counted action if valid, or a Rejection action if invali4.
5. Result actions must have a preceding Vote action.
6. Result actions tally up the votes specified in all the Ballot Counted actions at the end of the vot5. Ballots cast are only valid if the votes was cast by a token owner that owned the token before the valid period specified by the Vote action. Trading votes away after the vote has been announced is not permitted by the smart contract.

##Enforcement Operations
1. All Enforcement operations require an Order action sent from the issuer’s address as the initiating action.
2. A Freeze action alerts the affected token owner that the smart contract will be unable to respond to any actions with an affirmative action (Settlement, Vote). All actions will be responded to with a negation (Rejection action).
3. Votes submitted by a token owner whose account is frozen will not be counted in the vote tally.
4. A frozen address can only be unfrozen by a Thaw action.
5. Thaw actions that are not directed at a frozen address will be ignore4.
6. Confiscation actions that are not directed at an address with tokens will be rejecte4.
7. Reconciliation actions will decrement the tokens of the specified type at the targeted address to ensure that the number of outstanding tokens issued by the issuer is maintained across the state of the blockchain. Chained token transfer actions that are broken can result in additional tokens in the system that need reconcilin7.

##Messaging Operations
1. Message actions can be from any address to any other address.
2. Rejection actions are the negative response from a smart contract to indicate that another action is not vali4. Actions that have a Rejection action as a response are ignored by the protocol.

##Registry Operations
1. All Registry operations that come before an Establishment action are ignore4.
2. All Addition actions are on a treated on a first seen basis. All subsequent Addition actions that are repetitions of the first are ignore4.
3. An Alteration action must be preceded by an Addition action that is pointed to the same user’s address.
4. All Removal actions must be preceded by a valid Addition action.
