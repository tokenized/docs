##Tokenized Asset Creation
A Tokenized asset is generated when a token Issuer presents a valid 'Asset Definition' action to a Smart Contract. The Smart Contract checks only that the rules proposed in the offer are compliant with its logic, but the legal and regulatory aspects of distributing and managing the assets must be managed by the Issuer to ensure that assets are transacted within all applicable laws and regulations.

###1. Asset Definition
To create an 'Asset Definition', the Contract Issuer must prepare an action that contains all of the required information such as:
* Asset details (Type, code)
* Asset rules (flags, trading restrictions, voting and governance)
* Quantity
* Fee rules for trading that asset
* The asset specific details in the Asset Payload (Each asset type has a different payload structure)
The Asset Definition action is built and signed by the Issuer before being sent to the Smart Contract Operator:
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-definition-action.svg?sanitize=true" alt="An Asset Definition action" align="middle">

###2. Asset Creation
When the Smart Contract receives the Asset Definition action it unpacks the information and evaluates it. If the Smart Contract decides there are no issues, it builds an 'Asset Creation' action in response which is sent onto the network. The Asset Creation action contains a complete repeat of all of the information in the Asset Definition action as an acknowledgement that the Smart Contract has accepted the asset as valid.
The contract also adds two additional fields
1. Timestamp - The time at which the Smart Contract built the Asset Creation action
2. Version field - Set to zero for a new asset. Increments by 1 each time the asset is updated
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action.svg?sanitize=true" alt="An Asset Creation action" align="middle">

##Tokenized Asset Modification
To modify a Tokenized asset, the issuer must first build an 'Asset Modification' action which contains the necessary infomration required for the Smart Contract to authorise and issue responses that update the asset properties.
The action contains the Asset Type and Asset Code, which make up the Asset ID. These fields cannot be modified.
Following on from these is the asset revision, which is incremented by 1 each time the asset is updated. An Asset Modification request that has a version number that isn't in sequence will be rejected.
Subsequent to these fields, the modifications to the asset are contained in an array of objects, each of which has the following information:
* The field index of the contract element being changed
* The element of the field (for to identify the index number of the element within an array - complex types only)
* The Sub Field Index (to identify the field within the object in the array - complex types only)
* An instruction on whether to add or delete an element (for arrays)
* The new data being placed into the specified index
For asset modifications that require a vote to be passed, the TXID of a Result action showing a positive vote outcome for the change must be added as the final data item in the Asset Modification action.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-modification-action.svg?sanitize=true" alt="Asset Modification action" align="middle">

###2. Contract Formation
When the contract sees the Contract Amendment action land in its wallet, it evaluates the action and looks to ensure that the modifications are valid. 
If the contract determines that the amendment is valid, it issues a full Contract Formation action including the full details of the contract, the updated version number and a new timestamp.
From this moment, all transaction requests to the contract must abide by the amended rules.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action-amendment.svg?sanitize=true" alt="Updated Contract Formation action" align="middle">
