##Tokenized Governance
The Tokenized protocol includes a complete set of enforcement capabilities including the ability to:
1. Freeze tokens
2. Thaw tokens
3. Confiscate tokens
4. Reconcile token balances
These actions allow token issuers to manage their token environment for compliance with internal policies, or lawful orders from enforcement or regulatory agencies. 

To enact an enforcement order, the Issuer uses the 'Order' action. In the action, the Issuer specifies the asset the order is to be enacted on, what type of order it is and any specific information relating to that order. There is also a field in the action that allows a hash or copy of an enforcecment order or decision which relates to the action being performed.

###Freezing Tokens
Freezing tokens is a two step process.

####1. Order (Freeze)
A Freeze action causes all tokens mentioned in the transaction to be frozen. A Freeze action can be applied to multiple addresses at once and can freeze any number of tokens held by a given address.
A freeze order is temporary and must have an expiry time associated with it.
If the Freeze action is applied to an asset but the contract's address is the given as the target, the freeze order will apply to the entire asset class, freezing all tokens.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-freeze.svg?sanitize=true" alt="Order action (Freeze)" align="middle">
####2. Freeze
After the Smart Contract has determined that the freeze order is valid, it responds by issuing a Freeze action. The action is sent to all addresses that the freeze order applies to. Once the Freeze action has been issued, any transfer orders that try to move frozen tokens will be rejected.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/freeze-action.svg?sanitize=true" alt="Freeze action" align="middle">

###Thawing Tokens
Thawing tokens is a two step process.

####1 Order (Thaw)
A Thaw action overrides a freeze on tokens held in any addresses it is applied to. A Thaw action can be applied to multiple addresses at once and can thaw any number of already frozen token held by a different address.
There is no requirement for tokens being thawed to have been frozen in the same Freeze action, nor is the issuer required to thaw all the frozen tokens at once.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-thaw.svg?sanitize=true" alt="Order action (Thaw)" align="middle">
####2. Thaw
After the Smart Contract has determined that the thaw order is valid, it responds by issuing a Thaw action. The action is sent to all addresses that the thaw order applies to. As soon as the Thaw action is sent, the Smart Contract will begin processing transfers for the previously frozen tokens.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/thaw-action.svg?sanitize=true" alt="Thaw action" align="middle">

###Confiscating Tokens
Confiscating tokens is a two step process.

####1 Order (Confiscation)
A Confiscation order can be used to move tokens without the need for a signed transaction from the private key that holds the tokens. A confiscation can be applied to multiple addresses in a single action, however all confiscated tokens must be delivered to a single receiving address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-thaw.svg?sanitize=true" alt="Order action (Thaw)" align="middle">
####2. Confiscation
After the Smart Contract has determined that the confiscation order is valid, it responds by issuing a Confiscation action. The action is sent to all addresses that the confiscation order applies to. As soon as the confiscation action is sent, the Smart Contract updates the balances of all addresses that have had confiscation applied as well as the address to which the confiscated funds will be sent. This address can transact using the tokens immediately.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/confiscation-action.svg?sanitize=true" alt="Confiscation action" align="middle">
