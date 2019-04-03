# Asset Actions

An asset is defined as a token or group of tokens created with a single unique asset ID and properties. There are several things that can be done with assets.

1. [Asset Creation](#asset-creation)
2. [Asset Modification](#asset-modification)
3. [Asset Transfer](#asset-transfer)
4. [Asset Enforcement](#asset-enforcement)

<a name="asset-creation"></a>
## Asset Creation

Assets are created by a smart contract under the instruction of the smart contract issuer. Each token has a set of rules that govern how it can be modified in future which may require that there be a successful motion to change that item as part of a vote.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation.svg?sanitize=true" alt="Asset Creation Process">

### 1. Asset Definition

To create an asset, the issuer must send the smart contract an Asset Definition action that fully defines the asset. This means stating the asset's type, asset number, administration settings and more, as well as the asset specific metadata. The Asset Definition action is sent to the smart contract's wallet in an on-chain transaction where the smart contract detects it and opens it for analysis.

### 2. Rejection/Asset Creation

If the smart contract finds that the issuer is trying to create a token that is missing required information or has a contradictory setup, then it will issue a rejection message. The issuer must re-do the asset definition action with correct information.

When the smart contract finds a correctly defined asset (one that doesn't violate its logical checks) it will create the asset using the Asset Creation action. This action effectively repeats the information in the Asset Definition action as a confirmation that the smart contract has accepted its validity. It also includes a timestamp and a version which is set to 0 for a new token. The Asset Creation action marks the moment from which the contract can begin managing that asset on behalf of the issuer.

<a name="asset-modification"></a>
## Asset Modification

Once an asset has been created, the only way to change it is through the asset modification process. An asset modification allows a token issuer to modify any asset's details, as long as the rules governing the modification of those details have been met. There are two ways to modify an asset:

1. [Unilateral Modification](#unilateral-modification)
2. [Modification by Vote](#modification-by-vote)

<a name="unilateral-modification"></a>
## Unilateral Modification

A unilateral modification takes place when the issuer makes a change to the asset which does not require a ballot or referendum to take place. This could include updating the asset's metadata or other details dependent on the rules. The process involves just two transactions.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-modification-unilateral.svg?sanitize=true" alt="Unilateral Asset Modification Process">

### 1. Asset Modification

The asset modification action includes details of any changes that are being made to the asset. One modification action can create multiple changes to an asset. Inside the action these are listed as individual items referenced to their position in the asset creation action, and the new values to be used.

### 2. Rejection/Asset Creation

If the modifications being requested are outside of the rules allowed by the smart contract, the agent will respond with a Rejection action. If the modification is analysed and is ok, the smart contract responds with an Asset Creation action which is the acknowledgement from the smart contract that the asset has been updated. The creation action contains a new full copy of all asset details and the new version number.

<a name="modification-by-vote"></a>
### Modification by vote

There are two ways in which an Asset Modification by vote can be brought forth. 
1. Referendum (called by the issuer)
2. Initiative (called by any holder of a token that has voting rights, subject to their payment of the initiative fee)

Both are initiated using the Proposal action. 
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-amendment-by-vote.svg?sanitize=true" alt="Asset Modification by Vote">

#### 1. Proposal

The proposal action is sent to the smart contract which will evaluate the issues being voted on (amendments etc) and make sure that those which result in changes to the smart contract do not violate the rules.

### 2. Vote

Once the smart contract has received a referendum or initiative action, it evaluates it for validity against the rules of the contract. If the vote is able to go ahead, the smart contract issues a Vote action onto the blockchain.

### 3. Ballot Cast

When users wallets detect the vote action, they will present the user with a form that displays details of all the options being voted upon and the possible choices. When a user has finished voting, their wallet sends the transaction onto the blockchain for checking by the smart contract. If the options chosen aren't valid, the smart contract will issue a rejection action but this should in most cases be a rare occurrence as wallets will prevent users from entering invalid choices.

### 4. Ballot Counted

After a user has sent their ballot onto the blockchain, the smart contract confirms that it has received it and that it is valid by issuing their wallet with a Ballot Counted action.

### 5. Result

Once the vote is over (time limited) the smart contract counts the votes and publishes the result to the blockchain.

### 6. Asset Modification

If the successful motion requires any changes to be made to the asset, the issuer must issue a new asset modification action with the updated details and a new version number for the asset. This is not something that happens automatically and the smart contract will not allow the issuer to change fields that it is not permitted to change unless the issuer includes a pointer to a vote result authorising the change of that item.

#### 7. Rejection/Asset Creation

Once the amendment has been checked against the smart contract rules, the smart contract will either send a rejection notice in the case that the issuer is trying to make a change that isn't supported by the necessary motions, or it will issue an Asset Creation action that includes all of the changes made to the asset and an incremfented version number.

<a name="asset-transfer"></a>
## Asset Transfer

Exchanging assets is at the core of Tokenized's functionality and gives users the power to trade assets on the Bitcoin network, with all of the certainty and security of bitcoin transactions.

The tokenized protocol uses just 2 operations to provide for a rich and full framework to conduct exchanges between parties including the ability to exchange tokens for Bitcoin, for other tokens, or to send tokens without inbound payment. When a smart contract creates an asset, a set of rules are established which govern how that token can be exchanged.

Some tokens such as loyalty coupons can only be sent from the issuer to a customer and back again. Some may only be able to be exchnaged between people who have been whitelisted in a register. These conditions are all dependent on the nature of the smart contract and of the assets being exchanged under the smart contract. One smart contract can manage the exchange of many different types of assets with different rules for each asset. There is no effective limit on the number of assets that a smart contract can create or manage.

There are three separate ways of moving assets using the Transfer Action:

* [Send](#send)
* [Exchange](#exchange)
* [Swap](#swap)

<a name="send"></a>
### Send

The sending of an asset is done by sending a Transfer action to the smart contract with the destination address and quantity of that asset. A send operation can send more than one asset type to more than one asset receiver in a transfer action allowing for fast distribution of both fungible and non-fungible token types to receivers.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-transfer-send.svg?sanitize=true" alt="Sending an Asset">

The send process is a 2 step process:

#### 1. Transfer Action

The entity sending the tokens builds a Transfer action that defines which assets they wish to distribute, in which quantities, and to which parties. If the sender has assets stored in multiple addresses, they will need to build a transaction that reflects that, and to sign the transaction with inputs from each of those addresses. This process should be automated within the wallet, needing the sender only to specify which assets they are sending to which parties. Once the transaction is ready it is sent to the blockchain.

#### 2. Rejection/Settlement

Once the smart contract sees the Transfer action arrive in its wallet, it will evaluate it against the rules of the smart contract. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message.

If the smart contract finds that the action is valid, it will issue a Settlement action. the Settlement action includes output UTXOs that go to each address receiving assets in the transaction. These utxos are detected by user wallets which use their index in the transaction to find the details of the assets that have been transferred to them in the transaction.

<a name="exchange"></a>
### Exchange

An exchange occurs when an asset or assets are being purchased for an amount in Bitcoin. This is facilitated by a smart contract with an interface to users who may or may not hold assets (such as a webpage) that will allow them to place orders to purchase assets.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-transfer-exchange.svg?sanitize=true" alt="Exchanging Assets">

The process has 5 steps:

#### 1. Purchaser decides on tokens to purchase

The token purchaser views the tokens that are for sale by the token seller and decides on which token or tokens they would like to purchase. Each asset type will have its own prices, and the purchaser can purchase multiple quantities of each asset type. Once the purchaser has assembled their list of desired assets, they notify the smart contract operators of their intention to buy.

##### 2. issuer creates template to send to purchaser

The issuer creates a transaction template for the purchase of the tokens. This template includes an unsigned input from the token issuer as well as a pre-constructed Transfer action. This can be sent to the user in a URI, as an email, in an on-chain Message Action or by any other method that allows for the simple exchange of hexadecimal messages. The issuer can also include their own change output which will allow them to set and pay the miner fee, as well as details of the fees and levies paid by the user to conduct the exchange.

#### 3. Purchaser adds inputs and signs
Once the purchaser has received the template, their wallet will add enough inputs to satisfy the needs of the purchase, including adding their own change output. The purchaser then signs their inputs using SIGHASH_ALL which locks the transaction, preventing further change. This partially signed transaction is then transmitted back to the issuer, again via any suitable method for sending hexadecimal information.

#### 4. issuer signs Transfer Action

The issuer now signs the transfer action and sends it onto the network.

#### 5. Rejection/Settlement

Once the smart contract sees the Transfer action arrive in its wallet, it will evaluate it against the rules of the smart contract. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message.

If the smart contract finds that the action is valid, it will issue a Settlement action. the Settlement action includes output UTXOs that go to each address receiving assets in the transaction. Because this exchange includes BSV as the medium of exchange, one of the outputs will be the BSV being paid to the token issuer. These utxos are detected by user wallets which use their index in the transaction to find the details of the assets that have been transferred to them in the transaction.

<a name="swap"></a>
### Swap

An asset swap is when two asset holders conduct an exchange between themselves for another asset. A swap can be between holders of assets on a single smart contract, or between two asset holders with assets managed by different smart contracts.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-transfer-swap.svg?sanitize=true" alt="Intercontract Atomic Swap">

The process of conducting a swap is complex and involves multiple messages being passed by each user.

#### 1. Offer

The first user prepares a swap offering for the second user. In this the first user creates a Transfer Action that outlines which assets they would like to swap and what they would like to exchange for it. This offering is sent to the second party in the exchange. It is possible for more than two token holders to be party to an exchange and for that exchange to involve more than one smart contract. Were this the case, the transfer action template would be sent between all parties in the swap until it was established that the terms were agreeable.

#### 2. Transaction templating

Once the Transfer action template has been signed, the first user takes the transfer action and puts it into a transaction template, adding an input from their own sending address and any change outputs needed. They then send the transaction template to the next user who does the same until all users have added their inputs and change outputs to the transaction.

#### 3. Signatures

Once all users have added their inputs, the process is repeated with each party so they can sign the transaction inputs. As each user can evaluate the whole transaction, they can validate that their outputs haven't been changed and that the transaction is what they agreed to. Users sign their inputs using SIGHASH_ALL, and th
e final signatory sends the fully signed transaction back to all parties and onto the network.

#### 4. smart contract Evaluation, Rejection/Settlement

Once the smart contract or contracts see the swap transaction in their wallets, each one evaluates it against its own rules. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message. If any of the smart contracts issues a rejection, the transaction cannot go ahead.

In a contract trading assets managed by a single smart contract, once the smart contract decides that it is a valid transaction it will issue a Settlement which outlines the final balances controlled by each PKH.

In a trade involving multiple smart contracts, each will have an input connected to the transaction which it will need to sign using SIGHASH_ALL before the transaction can be sent onto the network. this means that each contract can completely evaluate the conditions of the trade are being upheld before signing.

<a name="asset-enforcement"></a>
## Asset Enforcement

Asset Enforcement means action by the issuer upon assets over which it does not directly control.

These actions may be due to reasons of legal enforcement, contract breach, or simply built into the usage model of the token. There are numerous ways in which enforcement actions can be used in a smart contract including including:

* [Freezing tokens](#freezing-tokens)
* [Thawing tokens](#thawing-tokens)
* [Confiscating tokens](#confiscating-tokens)
* [Reconciling token balances](#reconciling-token-balances)

Each of these actions is ordered by the issuer sending an 'Order' transaction to the blockchain with instructions for the smart contract on what actions are needed.

One order instruction can perform one enforcement action type on one asset, but to many addresses.

<a name="freezing-tokens"></a>
### Freezing and Thawing Tokens

To freeze tokens, the issuer must send an Order action that identifies the asset being frozen, the addresses holding that asset upon which the freeze order is to be applied, and the number of tokens from each address that the order is acting upon. In this way, a contract may freeze one or all tokens held by a user.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-enforcement-freeze.svg?sanitize=true" alt="Freezing Assets">

#### 1. Issuing the freeze order

The issuer first creates an order action which contains all of the pertinant information relating to the tokens being frozen. This includes the Asset type and code for the tokens being frozen, the addresses where they are held, and the quantities being frozen at each address. The order also includes a place for a public key and signature from the authority who created the order being enforced as well as a link to a transaction containing supporting evidence. In some instances where a freeze may only be temporary, there is also a field to determine a Freeze Period.

#### 2. smart contract Evaluation, Rejection/Freeze

When the smart contract receives the order it will evaluate it for compliance with the smart contract rules including whether the correct of information has been supplied, and that the signature and public key are from an authority with the right to create enforcement actions on the contract.

If the smart contract finds that the order is invalid, it will issue a rejection action with a message detailing the issues with the order.

If the smart contract finds that the order is valid, it will respond by creating a 'Freeze Action' which it will send onto the blockchain. Once the freeze action has been sent, the users wallets should flag that their assets have been frozen and not allow them to attempt any transfer actions. The freeze goes into effect the moment the smart contract has validated and responded to the freeze action. The contract does not need for the action to be propagated across the network or confirmed in a block for the freeze to take effect and can immediately begin rejecting actions that operate on frozen assets.

So that the action can be tracked from 'Order' to 'Enforcement', rather than including references to the order transaction in the freeze action, the smart contract simply creates the Freeze action using the same UTXO that the Order action was sent with. By doing this there can be no question that the action is in response to a particular order.

<a name="thawing-tokens"></a>
#### 3. Thawing tokens

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-enforcement-thaw.svg?sanitize=true" alt="Thawing Assets">

For tokens that do not have an automatic time out on the thaw action, or upon which the freeze action is able to be lifted, the issuer must create a an 'Order Action' that instructs the smart contract to thaw the tokens and send it to the smart contract. The order contains the same set of information as the freeze action, including the address list, token quantities, transaction reference to the enforcement order and however the tokens being referenced are the ones having the freeze action lifted.

The smart contract will again spend the receiving UTXO into a 'Thaw Action' which repeats the list of addresses and token quantities being thawed so that wallets can update details to their users.

Once the smart contract has issued the thaw action, token transfers can begin immediately.

<a name="confiscating-tokens"></a>
### Confiscating Tokens

The process of confiscating a token is predicated on the legal right of the issuer to perform the confiscation action. issuers must have the right to confiscate the tokens either due to malfeasance on the part of the token holder, or through the terms and conditions of the smart contract itself.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-enforcement-confiscation.svg?sanitize=true" alt="Confiscating Assets">

Once the issuer has established that they have the need and the right to confiscate tokens, the process is straight forward.

#### 1. Issuing the Confiscation Order

The Confiscation order comes in the form of an Order action that details the AssetID of the token being confiscated, the authority who has determined that the tokens must be confiscated, their signature and public key and copies of or links to the legal documentation regarding the confiscation event.

The order also includes a address to which all of the tokens confiscated in the order will be sent. This address can be one controlled by the legal authority requesting the confiscation, or in the context of returning tokens to someone after a fraud event, can specify that the tokens be sent back to the original owner.

Once the confiscation order has been built, the issuer sends it in a Bitcoin transaction to the wallet of the smart contract.

#### 2. smart contract Evaluation, Rejection/Confiscation

When the smart contract receives the order it will evaluate it for compliance with the smart contract rules including whether the correct of information has been supplied, and that the signature and public key are from an authority with the right to create enforcement actions on the contract.

If the smart contract finds that the order is invalid, it will issue a rejection action with a message detailing the issues with the order.

If the smart contract finds that the order is valid, it will issue a confiscation order that strips the addresses listed of the number of tokens in the order. The confiscation order is adequate to settle all token account balances on its own and does not need to be followed up with any further transaction. Once the tokens have been re-allocated, the receiving account is free to use them as normal.

A Confiscation action cannot be reversed and would be regarded as the final outcome of a legal dispute. Tokens can be confiscated while they are frozen, and are automatically thawed as soon as the re-allocation is complete.

<img src="https://github.com/tokenized/docs/blob/master/images/confiscation.JPG?raw=true" width="100%" alt="Confiscation action flow diagram">

<a name="reconciling-token-balances"></a>
### Reconciling Token balances

In the rare event of a failure on the Bitcoin network that causes Tokenized transactions to be lost, the action used to update the smart contract to reflect a new state is called 'Reconciliation'.

A reconciliation is an order from the issuer to the smart contract that reflects a new state of ownership for the asset. The reconciliation must balance meaning that at the end of a reconciliation, the total number of tokens attached to the asset cannot change.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-enforcement-reconciliation.svg?sanitize=true" alt="Reconciling Assets">

The process of reconciling a contract is as follows:

#### 1. Issuing the Reconciliation Order

The Reconciliation order comes in the form of an Order action that details the AssetID of the token being reconciled, documentation relating to the reasons for the reconciliation and a full set of balances for the updated state of any accounts impacted by the reconciliation action.

The action also has fields for the mandatory inclusion of full hexadecimal strings for each transaction that included an action that was lost/rejected by the network as proof that the actions were once received as a zero-conf transaction into the wallet of a Tokenized smart contract. The transactions must be complete, signed and valid Bitcoin transactions that spend UTXOS that still exist on the network.

#### 2. smart contract Evaluation, Rejection/Reconciliation

When the smart contract receives the order it will evaluate it for compliance with the smart contract rules including whether the correct information has been supplied, and that the signature and public key are from an authority with the right to create enforcement actions on the contract.

If the smart contract finds that the order is invalid, it will issue a rejection action with a message detailing the issues with the order.

If the smart contract finds that the order is valid, it will issue a reconciliation order that effectively re-settles the token balances of all of the accounts involved. The reconciliation order is adequate to settle all token account balances on its own and does not need to be followed up with any further transaction. Once the tokens have been re-allocated, accounts are free to use them as normal.

A Reconciliation action cannot be reversed and would be regarded as the final outcome of a legal dispute. The preconditions needed for a reconciliation to be required are exceptionally rare and as such any moves to create a reconciliation action on a contract should be performed with extreme oversight.
