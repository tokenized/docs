## Tokenized Governance
The Tokenized protocol includes a full and rich governance model that allows for different priorities to be placed on different authorities for almost any aspect of a contract or asset which can be modified. These settings are all governed by the authorisation flags that are present in the most recent Contract Formation or Asset Creation actions issued by the contract.
Where a field in a contract or asset definition has been set to allow for 'Unilateral' changes to be made, this means that the Issuer may make changes to this field without needing the authority of a vote process. This means that the fields can be changed at any time without restriction.
Where a field in a contract or asset definition has been set to require a positive outcome from a Referendum, the Contract Amendment or Asset Modification action that contains the change will need to contain a TXID that references a Result action that counts the votes in a link the modification of that paramter. 

### Authorisation flags
When a Contract or Asset is created, there are a set of authorisation flags which are defined in the Contract offer or Asset Definition action. These flags determine for each parameter that can be changed what the minimum requirement for making a change is. Each field has three flags, which each define whether or not a particular governance mechanism can be used to modify that field. To enable the mechanism related to each flag they must be set to 'True' (binary 1). The three flags correspond to the enablement of the following change mechanisms:
1. Issuer can change unilaterally
2. Issuer must hold a Referendum leading to a postive result in line with voting systems
3. Parameter can only be changed after a user requested Initiative leading to a postive result as defined by voting systems
Each parameter has a set of three flags which are represented as a sequential set of three bits within the Authorisation Flags element of the contract or asset. Where parameters are a variable length array type, the flag settings apply to the whole array.

### Voting Systems
Voting systems can be set up to provide a complex and layered approach to governance. Individual settings within individual assets or contracts can have voting mechanisms that differ from all other voting systems in that contract or asset. The exception to this is that the rules that forbid the creation of a vote through referendum or initiative that apply to a contract also apply to the assets in that contract.
When a vote is performed, the result of each proposed amendment will be counted in-line with the specific voting rules attached to that field. The different ways of counting are as follows:
#### R - Relative Threshold
(Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast. Abstentations/spoiled votes do not detract from the liklihood of a vote passing as they are not included in the denominator.  
#### A - Absolute Threshold
Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens. Abstentations/spoiled votes detract from the liklihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the vote cannot pass.  50% of all tokens would have had to vote for one vote option for the vote to be successful."
#### P - Plurality
In a Plurality, the number of votes in favour of the resolution must be more than the number of votes againts. Abstentions and spoiled votes do not detract from the likelihood of a plurality passing.

## Creating and Running a Vote
There are two ways for a vote action to be created, both using the Proposal Action. 
### 1. Proposal
A Proposal is the means by which a vote action which is called. There are two ways to create a vote. 

1. Referendum
A Referendum is called by sending a Proposal action to the Smart Contract with the issuer set as the 'Initiator' of the action. Referendums can be called at any time and the cost is only the contract fees needed for the vote, and any transaction fees.
2. Initiative
An Initiative is a vote initiated by the holder of a token that has initiative rights. Any token holder regardless of the number of tokens they hold can call an initiative, as long as the Initiative Cost is paid. The initiative cost is a threshold that sets a floor on the cost of creating an initiative. It is a fee paid to the contract issuer but which forces a vote to take place.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/proposal-action.svg?sanitize=true" alt="A Proposal action" align="middle">

### 2. Vote
Once the Smart Contract receives the valid Proposal action, it creates a Vote action. The vote action is sent from the contract to itself, which is an indicator to all wallets that it is a message they should read. When user wallets see the vote action, the user is presented with all the options in the vote and can select their choices.

The Vote action itself is very simple, and contains only the timestamp when the vote was created. The action is created by spending the UTXO associated with the Proposal action it is creating the vote for. Wallets refer back to the proposal action to build the voting interface for the user.

There is no restriction on the number of Vote actions that can be active at once however the contract will reject a vote for a change to a field in a contract or asset that is already under an active Vote action, or which has had a successful Vote action that stipulates a change that has not yet been made. The vote results themselves do not activate any changes to the smart contract. It is still up to the issuer to create and send an Asset Modification or Contract Amendment action that implements the changes that have been voted on. If a Vote action results in the successful passage of an amendment order, the contract will not allow further votes on that field until the changes  
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/vote-action.svg?sanitize=true" alt="A Vote action" align="middle">

### 3. Ballot Cast
Once the user's wallet sees the Vote action, it can build the ballot for the user. The ballot consists of a set of response fields that display the vote choices and voting options detailed in the Proposal action. Once the user has selected their choices the wallet builds a Ballot Cast action. If a user has more than one asset with voting rights in a contract, their votes will be cast against their full asset holdings in aggregate. The counting is performed by the Smart Contract. 
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/ballot-cast-action.svg?sanitize=true" alt="A Ballot Cast action" align="middle">

### 4. Ballot Count
When the Smart Contract sees that the user has cast their vote using a valid Ballot Cast action, it responds with a Ballot Counted action that acknowledges the receipt of the Ballot Cast action. The contract spends the UTXO that carried the Ballot Cast action to enable the wallet to track which vote is being responded to. The action only contains a timestamp from when the Ballot Counted action was created.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/ballot-cast-action.svg?sanitize=true" alt="A Ballot Cast action" align="middle">

### 5. Result
When the time elapses on the vote, the Smart Contract tallies the votes for each option in the Proposal. The full details of the changes from the Proposal are repeated with a pass or fail result based on the voting system, and the number of votes received.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/result-action.svg?sanitize=true" alt="A Result action" align="middle">

Once the result action has been published, the Vote is concluded and the Issuer can act on the amendments that have passed.
