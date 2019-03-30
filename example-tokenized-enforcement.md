##Tokenized Governance
The Tokenized protocol includes a complete set of enforcement capabilities including the ability to:
1. Freeze tokens
2. Thaw tokens
3. Confiscate tokens
4. Reconcile token balances
These actions allow token issuers to manage their token environment for compliance with internal policies, or lawful orders from enforcement or regulatory agencies. 

To enact an enforcement order, the Issuer uses the 'Order' action. In the action, the Issuer specifies the asset the order is to be enacted on, what type of order it is and any specific information relating to that order. There is also a field in the action that allows a hash or copy of an enforcecment order or decision which relates to the action being performed.

###Freezing Tokens
When tokens are frozen, they cannot be moved. Tokens remain the property of the address that holds them however they are prevented from being traded.
When an address holds frozen tokens, it is not prevented from receiving more tokens unless by a separate registry order. It is possible for a Freeze order to freeze a larger quantity of tokens than the account holds to prevent the account from receiving new tokens and spending them. Zero token freeze actions are invalid.
An address may be subject to multiple freeze orders. The number of tokens which are frozen is the aggregate quantity specified by all of the active Freeze actions. E.g. if an address has one active Freeze order that freezes 10,000 tokens and a second Freeze order that freezes 20,000 tokens is put in place, the account may only transfer whatever balance it has in excess of 30,000 tokens. Freeze actions can only be undone through a Thaw or a Confiscation action. 

Freezing tokens is a two step process.
####1. Order (Freeze)
A Freeze order causes a specified quantity of tokens in each listed address to be frozen. A Freeze order can be applied to multiple addresses at once and can freeze any number of tokens held by a given address.
A Freeze order is temporary and must have an expiry time associated with it.
If the Freeze order is applied to an asset but the contract's address is the given as the target, the Freeze order will apply to the entire asset class, freezing all tokens.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-freeze.svg?sanitize=true" alt="Order action (Freeze)" align="middle">
####2. Freeze
After the Smart Contract has determined that the freeze order is valid, it responds by issuing a Freeze action. The action is sent to all addresses that the freeze order applies to. Once the Freeze action has been issued, any transfer orders that try to move frozen tokens will be rejected.
An issuer can place multiple freeze orders on a single address. In this case, the number of tokens frozen is the aggregate count of froz
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/freeze-action.svg?sanitize=true" alt="Freeze action" align="middle">

###Thawing Tokens
Thawing tokens reverses a Freeze order that has been put in place. One Thaw order reverses one Freeze action only. If an asset is frozen by two separate Freeze orders, there must be two separate Thaw orders applied to it before it can be traded, one per Freeze. 
Thawing tokens is a two step process.

####1 Order (Thaw)
A Thaw order reverses a single Freeze action.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-thaw.svg?sanitize=true" alt="Order action (Thaw)" align="middle">
####2. Thaw
After the Smart Contract has determined that the thaw order is valid, it responds by issuing a Thaw action. The action is sent to all addresses that the thaw order applies to. As soon as the Thaw action is sent, the Smart Contract will begin processing transfers for the previously frozen tokens.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/thaw-action.svg?sanitize=true" alt="Thaw action" align="middle">

###Confiscating Tokens
Token confiscation actions are used to move tokens from an address without the need for a signed message from the token owner. A confiscation action can be applied to tokens from multiple addresses at once, however all confiscated tokens must be sent to a single address. A confiscation action can be performed on frozen tokens. Once moved into the new address, those tokens can be moved unless a pre-emptive Freeze order is placed on the receiving address to lock down the received tokens.
Confiscating tokens is a two step process.

####1 Order (Confiscation)
A Confiscation order can be used to move tokens without the need for a signed transaction from the private key that holds the tokens. A confiscation can be applied to multiple addresses in a single action, however all confiscated tokens must be delivered to a single deposit address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-confiscation.svg?sanitize=true" alt="Order action (Thaw)" align="middle">
####2. Confiscation
After the Smart Contract has determined that the confiscation order is valid, it responds by issuing a Confiscation action. The action is sent to all addresses that the confiscation order applies to. The confiscation order sets a new balance for each address in the order as well as for the deposit address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/confiscation-action.svg?sanitize=true" alt="Confiscation action" align="middle">

###Reconciliation
A Reconciliation process is needed when a Smart Contract has received actions that have been lost by the network, or which have been incorrectly assigned by the smart contract due to error. A reconciliation is regarded as a very rare occurrence.
The Reconciliation applies new balances to a series of addresses. The action must balance. i.e. the number of tokens in the new balances must match the number of tokens previously held.
Reconciliation is a two step process.

####1 Order (Reconciliation)
A Reconciliation order can be used to resolve disputes around lost or misapplied transaction which have resulted in incorrect token balances. A Reconciliation can be applied to multiple addresses in a single action.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-reconciliation.svg?sanitize=true" alt="Order action (Thaw)" align="middle">
####2. Reconciliation
After the Smart Contract has determined that the Reconciliation order is valid, it responds by issuing a Reconciliation action. The action is sent to all addresses that the Reconciliation order applies to. The Reconciliation order sets a new balance for each address in the order as well as for the deposit address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/reconciliation-action.svg?sanitize=true" alt="Reconciliation action" align="middle">
