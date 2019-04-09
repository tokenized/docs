## Creation and management of Tokenized assets

1. [Asset Creation](#asset-creation)
2. [Asset Modification](#asset-modification)
3. [Asset Types](#asset-types)

<a name="asset-creation"></a>
## Tokenized Asset Creation
A Tokenized asset is generated when a token issuer presents a valid 'Asset Definition' action to a smart contract. The smart contract checks only that the rules proposed in the offer are compliant with its logic, but the legal and regulatory aspects of distributing and managing the assets must be managed by the issuer to ensure that assets are transacted within all applicable laws and regulations.

### 1. Asset Definition
To create an 'Asset Definition', the Contract issuer must prepare an action that contains all of the required information such as:
* Asset details (Type, code)
* Asset rules (flags, trading restrictions, voting and governance)
* Quantity
* Fee rules for trading that asset
* The asset specific details in the Asset Payload (Each asset type has a different payload structure)
The Asset Definition action is built and signed by the issuer before being sent to the smart contract Operator:
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-definition-action.svg?sanitize=true" alt="An Asset Definition action" align="middle">

### 2. Asset Creation
When the smart contract receives the Asset Definition action it unpacks the information and evaluates it. If the smart contract decides there are no issues, it builds an 'Asset Creation' action in response which is sent onto the network. The Asset Creation action contains a complete repeat of all of the information in the Asset Definition action as an acknowledgement that the smart contract has accepted the asset as valid.
The contract also adds two additional fields
1. Timestamp - The time at which the smart contract built the Asset Creation action
2. Version field - Set to zero for a new asset. Increments by 1 each time the asset is updated
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action.svg?sanitize=true" alt="An Asset Creation action" align="middle">

<a name="asset-midification"></a>
## Tokenized Asset Modification
To modify a Tokenized asset, the issuer must first build an 'Asset Modification' action which contains the necessary infomration required for the smart contract to authorise and issue responses that update the asset properties.

### 1. Asset Modification
The action contains the Asset Type and Asset Code, which make up the Asset ID. These fields cannot be modified.
Following on from these is the asset revision, which is incremented by 1 each time the asset is updated. An Asset Modification request that has a version number that isn't in sequence will be rejected.
Subsequent to these fields, the modifications to the asset are contained in an array of objects, each of which has the following information:
* The field index of the contract element being changed
* The element of the field (for to identify the index number of the element within an array - complex types only)
* The Sub Field Index (to identify the field within the object in the array - complex types only)
* An instruction on whether to add or delete an element (for arrays)
* The new data being placed into the specified index
For asset modifications that require a vote to be passed, the TXID of a Result action showing a positive vote outcome for the change must be added as the final data item in the Asset Modification action. For detail on the voting process please see [Governance](governance).
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-modification-action.svg?sanitize=true" alt="Asset Modification action" align="middle">

### 2. Asset Creation
When the contract sees the Asset Modification action land in its wallet, it evaluates the action and looks to ensure that the modifications are valid. 
If the contract determines that the amendment is valid, it issues a full Asset Creation action including the full details of the asset, the updated version number and a new timestamp.
From this moment, all transaction requests to the contract must abide by any amended rules that apply to the asset.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action-amendment.svg?sanitize=true" alt="Updated Contract Formation action" align="middle">

<a name="asset-types"></a>
## Tokenized Asset Types

When a tokenized asset is created, it includes a payload that defines the metadata that are attached to that particular token or tokens. The tokenized protocol is broad enough that any type of token can be developed and created.

For the initial release of the Tokenized protocol, the following 6 asset types will be available:

### 1. [COU - Coupons](../assets/cou)

Coupons represent an asset that gives the bearer a right to procure a good or service with terms that are different to those under which someone without a coupon would need to agree to. This may include a discounted price, longer warranty, free installation or any other add-on or benefit.

### 2. [LOY - Loyalty Points](../assets/loy)

Loyalty points allow a merchant or business to reward repeat customers with tokens that can later be redeemed for discounted or free goods and services. Examples include coffee tokens (buy 10 coffees, get one free), airline miles (1 point per mile flown) and more.

### 3. [MEM - Membership](../assets/mem)

A membership token is a token that is usually handed out in a quantity of one.  The possession of a membership token signifies the belonging of the bearer to a defined group.  As a few examples, membership tokens can be used to represent membership in a Board of Directors, a non-profit organization, or even a special interest club.  Membership tokens can allow access to certain rights/privileges that members of the particular group are entitled, as well as any duties/responsibilities. This might include entry to a physical location such as a gym or club, or entry to a restricted part of a website such as a forum or members only zone.

### 4. [SHC - Common Share](../assets/shc)

A common share is a share of a company providing the owner with a right to vote at shareholder meetings and to receive a part of the company profits as a dividend.

### 5. [TIC - Admission Ticket](../assets/tic)

An admission ticket confers upon its owner a certain right, especially to enter a place, travel by public transport, or participate in an event. Once the ticket has been 'redeemed', the record of ownership remains in the users wallet similar to a 'ticket stub'. Tickets can be used for any event including conferences, arena concerts, sports events, or to buy pay per view rights to an event streamed over the internet.

### 6. [CUR - Currency](../assets/cur)

Currency represents a tokenized version of a fiat currency. This is something that is issued and controlled by a legally entitled entity as a representative token of the currency being tokenized.