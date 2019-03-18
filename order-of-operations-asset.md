##Asset Actions
An asset is defined as a token or group of tokens created with a single unique asset ID and properties. There are several things that can be done with assets.
1. Asset Creation
2. Asset Modification
3. Asset Transfer
4. Asset Governance

##1. Asset Creation
Assets are created by a Smart Contract under the instruction of the Smart Contract issuer. Each token has a set of rules that govern how it can be modified in future which may require that there be a successful motion to change that item as part of a vote.

###1. Asset Definition
To create an asset, the Issuer must send the Smart Contract an Asset Definition action that fully defines the asset. This means stating the asset's type, asset number, administration settings and more, as well as the asset specific metadata. The Asset Definition action is sent to the Smart Contract's wallet in an on-chain transaction where the Smart Contract detects it and opens it for analysis.

###2. Rejection/Asset Creation
If the Smart Contract finds that the issuer is trying to create a token that is missing required information or has a contradictory setup, then it will issue a rejection message. The issuer must re-do the asset definition action with correct information.
When the Smart Contract finds a correctly defined asset (one that doesn't violate its logical checks) it will create the asset using the Asset Creation action. This action effectively repeats the information in the Asset Definition action as a confirmation that the Smart Contract has accepted its validity. It also includes a timestamp and a version which is set to 0 for a new token. The Asset Creation action marks the moment from which the contract can begin managing that asset on behalf of the Issuer.

##2. Asset Modification
Once an asset has been created, the only way to change it is through the asset modification process. An asset modification allows a token issuer to modify any asset's details, as long as the rules governing the modification of those details have been met.

###Unilateral Amendment
A unilateral amendment takes place when the Issuer makes a change to the asset which does not require a ballot or referendum to take place. This could include updating the asset's metadata or other details dependent on the rules. The process involves just two transactions.
####1. Asset Modification
The asset modification action includes details of any changes that are being made to the asset. One modification action can create multiple changes to an asset. Inside the action these are listed as individual items referenced to their position in the asset creation action, and the new values to be used. 
####2. Rejection/Asset Creation
If the modifications being requested are outside of the rules allowed by the smart contract, the agent will respond with a Rejection action. If the modification is analysed and is ok, the Smart Contract responds with an Asset Creation action which is the acknowledgement from the smart contract that the asset has been updated. The creation action contains a new full copy of all asset details and the new version number. 

###Amendment by vote
There are two ways in which a asset modification by vote can be brought forth.
####1A. Referendum
A referendum is when the Issuer issues an intent to vote to the smart contract. The smart contract will evaluate the issues being voted on (modification etc) and make sure that those which result in changes to any assets do not violate the rules.
####1B. Initiative
An initiative is the method used for an asset owner to propose a vote. There is a significant cost attached to the initiative action as conducting a vote is a costly and disruptive exercise.
####2. Vote
Once the smart contract has received a referendum or initiative action, it evaluates it for validity against the rules of the contract. If the vote is able to go ahead, the smart contract issues a Vote action onto the blockchain.
####3. Ballot Cast
When users wallets detect the vote action, they will present the user with a form that displays details of all the options being voted upon and the possible choices. When a user has finished voting, their wallet sends the transaction onto the blockchain for checking by the smart contract. If the options chosen aren't valid, the smart contract will issue a rejection action but this should in most cases be a rare occurrence as wallets will prevent users from entering invalid choices.
####4. Ballot Counted
After a user has sent their ballot onto the blockchain, the smart contract confirms that it has received it and that it is valid by issuing their wallet with a Ballot Counted action.
####5. Result
Once the vote is over (time limited) the smart contract counts the votes and publishes the result to the blockchain. 
####6. Asset Modification
If the successful motion requires any changes to be made to the asset, the Issuer must issue a new asset modification action with the updated details and a new version number for the asset. This is not something that happens automatically and the smart contract will not allow the Issuer to change fields that it is not authorised to change without authorisation unless the issuer includes a pointer to a vote result authorising the change of that item.
####7. Rejection/Contract Formation
Once the amendment has been checked against the Smart Contract rules, the Smart Contract will either send a rejection notice in the case that the Issuer is trying to make a change that isn't supported by the necessary motions, or it will issue an Asset Creation action that includes all of the changes made to the asset and an incremented version number.

###3. Asset Transfer
Exchanging assets is at the core of Tokenized's functionality and gives users the power to trade assets on the Bitcoin network, with all of the certainty and security of bitcoin transactions.
The tokenized protocol uses just 2 operations to provide for a rich and full framework to conduct exchanges between parties including the ability to exchange tokens for Bitcoin, for other tokens, or to send tokens without inbound payment. When a smart contract creates an asset, a set of rules are established which govern how that token can be exchanged.
Some tokens such as loyalty coupons can only be sent from the issuer to a customer and back again. Some may only be able to be exchnaged between people who have been whitelisted in a register. These conditions are all dependent on the nature of the smart contract and of the assets being exchanged under the smart contract. One smart contract can manage the exchange of many different types of assets with different rules for each asset. There is no effective limit on the number of assets that a Smart contract can create or manage.

There are three separate ways of moving assets using the Transfer Action:
* Send
* Exchange
* Swap

####Send
The sending of an asset is done by sending a Transfer action to the Smart Contract with the destination address and quantity of that asset. A send operation can send more than one asset type to more than one asset receiver in a transfer action allowing for fast distribution of both fungible and non-fungible token types to receivers.
The send process is a 2 step process:
#####1. Transfer Action
The entity sending the tokens builds a Transfer action that defines which assets they wish to distribute, in which quantities, and to which parties. If the sender has assets stored in multiple addresses, they will need to build a transaction that reflects that, and to sign the transaction with inputs from each of those addresses. This process should be automated within the wallet, needing the sender only to specify which assets they are sending to which parties. Once the transaction is ready it is sent to the blockchain.
#####2. Rejection/Settlement
Once the Smart Contract sees the Transfer action arrive in its wallet, it will evaluate it against the rules of the smart contract. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message. 
If the smart contract finds that the action is valid, it will issue a Settlement action. the Settlement action includes output UTXOs that go to each address receiving assets in the transaction. These utxos are detected by user wallets which use their index in the transaction to find the details of the assets that have been transferred to them in the transaction.

####Exchange
An exchange occurs when an asset or assets are being purchased for an amount in Bitcoin. This is facilitated by a smart contract with an interface to users who may or may not hold assets (such as a webpage) that will allow them to place orders to purchase assets.
The process has 5 steps:
#####1. Purchaser decides on tokens to purchase
The token purchaser views the tokens that are for sale by the vendor and decides on which token or tokens they would like to purchase. Each asset type will have its own prices, and the purchaser can purchase multiple quantities of each asset type. Once the purchaser has assembled their list of desired assets, they notify the issuer of their intention to buy. 
#####2. Issuer creates template to send to purchaser
The issuer creates a transaction template for the purchase of the tokens. This template includes an unsigned input from the token issuer as well as a pre-constructed Transfer action in the correct index to allow the user to add their own inputs and a single change output to the transaction. The user can move the OP_RETURN from its index if their wallet needs to send change to more than one address however this would be uncommon. This can be sent to the user in a URI, as an email, in an on-chain Message Action or by any other method that allows for the simple exchange of hexadecimal messages. The issuer can include their own change output which will allow them to set and pay the miner fee, as well as details of the fees and levies paid by the user to conduct the exchange.
#####3. Purchaser adds inputs and signs
Once the purchaser has received the template, their wallet will add enough inputs to satisfy the needs of the purchase, including adding their own change output. The purchaser then signs their inputs using SIGHASH_ALL which locks the transaction, preventing further change. This partially signed transaction is then transmitted back to the issuer, again via any suitable method for sending hexadecimal information.
#####4. Issuer signs Transfer Action
The issuer now signs the transfer action and sends it onto the network. 
#####5. Rejection/Settlement
Once the Smart Contract sees the Transfer action arrive in its wallet, it will evaluate it against the rules of the smart contract. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message. 
If the smart contract finds that the action is valid, it will issue a Settlement action. the Settlement action includes output UTXOs that go to each address receiving assets in the transaction. Because this exchange includes BSV as the medium of exchange, one of the outputs will be the BSV being paid to the token issuer. These utxos are detected by user wallets which use their index in the transaction to find the details of the assets that have been transferred to them in the transaction.

####Swap
An asset swap is when two asset holders conduct an exchange between themselves for another asset. A swap can be between holders of assets on a single smart contract, or between two asset holders with assets managed by different smart contracts. 
The process of conducting a swap is complex and involves multiple messages being passed by each user.
#####1. Offer
The first user prepares a swap offering for the second user. In this the first user creates a Transfer Action that outlines which assets they would like to swap and what they would like to exchange for it. This offering is sent to the second party in the exchange. It is possible for more than two token holders to be party to an exchange and for that exchange to involve more than one smart contract. Were this the case, the transfer action template would be sent between all parties in the swap until it was established that the terms were agreeable.
#####2. Transaction templating
Once the Transfer action template has been signed, the first user takes the transfer action and puts it into a transaction template, adding an input from their own sending address and any change outputs needed. They then send the transaction template to the next user who does the same until all users have added their inputs and change outputs to the transaction.
#####3. Signatures
Once all users have added their inputs, the process is repeated with each party so they can sign the transaction inputs. As each user can evaluate the whole transaction, they can validate that their outputs haven't been changed and that the transaction is what they agreed to. Users sign their inputs using SIGHASH_ALL, and the final signatory sends the fully signed transaction back to all parties and onto the network.
#####4. Smart Contract Evaluation
Once the smart contract or contracts see the swap transaction in their wallets, each one evaluates it against its own rules. If it finds that the transaction goes against the logic of the smart contract it will issue a rejection message. If any of the smart contracts issues a rejection, the transaction cannot go ahead.
When a smart contract decides that it is 