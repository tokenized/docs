##Tokenized Contract Formation
A tokenized contract is formed when a token issuer presents a valid 'Contract Offer' action to a smart contract. The Smart Contract checks only that the rules of the smart contract are compliant with its logic, but the legal and regulatory aspects of dealing with the assets being created must be pre-established to ensure the contract operates within market rules.

###1. Contract Offer
To create a Contract Offer, the Contract Issuer must prepare an 'Offer' action that contains all of the required information such as:
* Contract name
* Governing Law
* Jurisdiction
* Contract rules, voting systems
* Detail of the issuing entity/entities including key personnel, addresses etc.
Included with the offer is either a hash and a URL linking to a contract file, or when possible, the entire contract file itself as a Markdown formatted file or PDF.
The contract offer action must be signed by both the Issuer and the Smart Contract Operator, so the issuer first builds a template transaction which it sends to the Smart Contract Operator:
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action-template.svg?sanitize=true" alt="A contract offer action template" align="middle">
If the operator is happy with this contract, they will add an input from their own wallet, add the change outputs they need and sign the contract offer using SIGHASH_ALL before sending it back to the issuer. Once the issuer has reviewed the Smart Contract Operator's changes, they can sign their own input (or inputs) using SIGHASH_ALL and send the transaction onto the network.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-offer-action-final.svg?sanitize=true" alt="Final contract offer action" align="middle">

###2. Contract Formation
When the Smart Contract receives the offer action it unpacks the information and evaluates it. If it decides there are no issues, it builds a 'Contract Formation' action in response which it sends onto the network. The Contract Formation Action contains a complete repeat of all of the information in the Contract Offer action as an acknowledgement that the Smart Contract has accepted the setup as valid.
The contract also adds two additional fields
1. Timestamp - The time at which the Smart Contract built the Contract formation action
2. Version field - Set to zero for a new contract. Increments by 1 each time the contract is updated
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action.svg?sanitize=true" alt="Contract Formation action" align="middle">

##Tokenized Contract Amendment
The amendment of a tokenized contract can be simple when the rules or conditions being changed are able to be amended without needing a vote. This is called a Unilateral Amendment, and is comprised of just 2 actions.
1. Contract Amendment
2. Contract Formation

Where a Contract Amendment seeks to make changes that require a vote through referendum or initiative, the 

###1. Contract Amendment
If the issuer wants to change the issuer address (e.g. in the event of a contract being sold) or to change the Operator address (to move to a new service provider) there are flags for these options. The Smart Contract receives the new addresses for these contracts from signed inputs paying into the transaction carrying the action.
Following on from these flags is the new contract revision, which is incremented by 1 each time the contract is updated. A Contract Amendment request that has a version number that isn't in sequence will be rejected.
For amendments that require a vote to be passed that 
Subsequent to these fields, amendments to the contract are contained in an array of objects, each of which has the following information:
* The field index of the contract element being changed
* The element of the field (for to identify the index number of the element within an array - complex types only)
* The Sub Field Index (to identify the field within the object in the array - complex types only)
* An instruction on whether to add or delete an element (for arrays)
* The new data being placed into the specified index
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-amendment-action.svg?sanitize=true" alt="Contract Amendment action" align="middle">

###2. Contract Formation
When the contract sees the Amendment action land in its wallet, it pulls the action apart and looks to ensure that the modifications are valid. 
If the contract determines that the amendment is valid, it issues a full Contract Formation transaction including the full details of the contract, including the updated version number and a new timestamp.
From this moment, all transaction requests to the contract must abide by the amended rules.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/contract-formation-action-amendment.svg?sanitize=true" alt="Updated Contract Formation action" align="middle">
