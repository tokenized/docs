##Asset Actions
An asset is defined as a token or group of tokens created with a single unique asset ID and properties. There are several things that can be done with assets.
1. Asset Creation
2. Asset Modification
3. Asset Exchange
4. Asset Governance

##Asset Creation
Assets are created by a Smart Contract under the instruction of the Smart Contract issuer. Each token has a set of rules that govern how it can be modified in future which may require that there be a successful motion to change that item as part of a vote.

###1. Asset Definition
To create an asset, the Issuer must send the Smart Contract an Asset Definition action that fully defines the asset. This means stating the asset's type, asset number, administration settings and more, as well as the asset specific metadata. The Asset Definition action is sent to the Smart Contract's wallet in an on-chain transaction where the Smart Contract detects it and opens it for analysis.

###2. Rejection/Asset Creation
If the Smart Contract finds that the issuer is trying to create a token that is missing required information or has a contradictory setup, then it will issue a rejection message. The issuer must re-do the asset definition action with correct information.
When the Smart Contract finds a correctly defined asset (one that doesn't violate its logical checks) it will create the asset using the Asset Creation action. This action effectively repeats the information in the Asset Definition action as a confirmation that the Smart Contract has accepted its validity. It also includes a timestamp and a version which is set to 0 for a new token. The Asset Creation action marks the moment from which the contract can begin managing that asset on behalf of the Issuer.

##Asset Modification
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