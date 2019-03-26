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
