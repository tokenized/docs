##Contract Actions
There are two ways that an issuer can interact with their Smart Contract:
1. [Establishment](#establishment)
2. [Amendment](#amendment)

<a name="establishment"></a>
##Establishment
The establishment of a contract is a two step process.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-establishment.svg?sanitize=true" alt="Contract Establishment Process">
###1. Contract Offer
The Contract offer is a transaction sent from the Contract Issuer to the smart contract which outlines the details of a contract the issuer is seeking to create. The offer contains a complete copy of all details of the contract which includes things such as rules limiting on the number of assets the contract can manage, details on how the contract will be governed and information on the issuer, the smart contract operator, and key persons linked to the creation of the contract.
###2. Contract Formation
Once the smart contract has evaluated the contract offer and determined that all the necessary information is present, it will send a Contract Formation action onto the blockchain. The contract formation action is an exact copy of the contract offer, which is timestamped with the date and time at which the contract went live and a version number.
The Contract Formation action marks the moment from which the contract can begin creating and managing assets on behalf of the issuer.

<a name="amendment"></a>
##Amendment
Once a contract has been formed, the only way to change it is through the contract amendment process. A contract amendment allows a token issuer to modify any contract details, as long as the rules governing the modification of those details have been met.

###Unilateral Amendment
A unilateral amendment takes place when the contract issuer makes a change to the contract which does not require a ballot or referendum to take place. This could include updating the office address of the token issuer, or changing the details of a key person tied to the contract. The process involves just two transactions.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-amendment-unilateral.svg?sanitize=true" alt="Unilateral Contract Amendment">
####1. Contract Amendment
The contract amendment action includes details of any changes that are being made to a smart contract. One amendment action can create multiple changes to a contract. Inside the action these are listed as individual items referenced to their position in the contract formation action, and the new values to be used.
####2. Contract Formation
The amendment action is followed by a Contract Formation action which is the acknowledgement from the smart contract that the contract has been updated. The formation action contains a new full copy of all contract details updated to the new version number. 

###Amendment by vote
There are two ways in which a contract amendment by vote can be brought forth.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-amendment-by-vote.svg?sanitize=true" alt="Contract Amendment by Vote">

####1A. Referendum
A referendum is when the Issuer issues an intent to vote to the smart contract. The smart contract will evaluate the issues being voted on (amendments etc) and make sure that those which result in changes to the smart contract do not violate the rules.
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
####6. Contract Amendment
If the successful motion requires any changes to be made to the contract, the Issuer must issue a new Contract Amendment action with the updated details and a new version number for the contract. This is not something that happens automatically and the smart contract will not allow the Issuer to change fields that it is not authorised to change without authorisation unless the issuer includes a pointer to a vote result authorising the change of that item.
####7. Rejection/Contract Formation
Once the amendment has been checked against the Smart Contract rules, the Smart Contract will either send a rejection notice in the case that the Issuer is trying to make a change that isn't supported by the necessary motions, or it will issue a Contract Formation action that includes all of the changes made to the smart contract.  