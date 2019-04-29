# Asset Management

- [Introduction](#introduction)
- [Creating an Asset](#asset-create)
	- [Asset Definition](#asset-definition)
	- [Asset Creation](#asset-creation)
- [Updating an Asset](#asset-update)
	- [Asset Modification](#asset-modification)
	- [Asset Creation for Updates](#asset-creation-update)
- [Asset Types](#asset-types)
	- [Coupons](#coupons)
	- [Loyalty Points](#loyalty-points)
	- [Membership](#membership)
	- [Common Share](#common-share)
	- [Admission Ticket](#admission-ticket)
	- [Currency](#currency)

<a name="introduction"></a>
## Introduction
Tokenized has a full and rich set of commands for the creation and modification of assets under a smart contract. A single smart contract can be used to manage a very large number of assets, each of which can be represented by different quantitiy of tokens. It is also possible to create non-fungible tokens by creating an asset with quantity 1, and metadata specific to that asset.

<a name="asset-create"></a>
## Creating an Asset

A Tokenized asset is generated when a token issuer presents a valid 'Asset Definition' action to a smart contract. The smart contract checks only that the rules proposed in the offer are compliant with its logic, but the legal and regulatory aspects of distributing and managing the assets must be managed by the issuer to ensure that assets are transacted within all applicable laws and regulations.

<a name="asset-definition"></a>
### Asset Definition

To create an 'Asset Definition', the Contract issuer must prepare an action that contains all of the required information such as:

- Asset type
- Asset rules (flags, trading restrictions, voting and governance)
- Quantity
- Fee rules for trading that asset
- The asset specific details in the Asset Payload (Each asset type has a different payload structure)

The Asset Definition action is built and signed by the issuer before being sent to the smart contract Operator:

![An Asset Definition action](https://raw.githubusercontent.com/tokenized/docs/master/images/asset-definition-action.svg?sanitize=true "An Asset Definition action") {.frame .centered .padded}

<a name="asset-creation"></a>
### Asset Creation

When the smart contract receives the Asset Definition action it unpacks the information and evaluates it. If the smart contract decides there are no issues, it builds an 'Asset Creation' action in response which is sent onto the network. The Asset Creation action contains a complete repeat of all of the information in the Asset Definition action as an acknowledgement that the smart contract has accepted the asset as valid.
The contract also adds four additional fields

- **AssetCode** - A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
- **AssetIndex** - Index of the asset in the contract. First is zero. The index is used to generate unique asset codes.
- **Timestamp** - The time at which the smart contract built the Asset Creation action
- **AssetRevision** - Set to zero for a new asset. Increments by 1 each time the asset is updated

![An Asset Creation action](https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action.svg?sanitize=true "An Asset Creation action") {.frame .centered .padded}

<a name="asset-update"></a>
## Updating an Asset

To modify a Tokenized asset, the issuer must first build an 'Asset Modification' action which contains the necessary infomration required for the smart contract to authorise and issue responses that update the asset properties.

<a name="asset-modification"></a>
### Asset Modification

The action contains the Asset Type and Asset Code, which make up the Asset ID. These fields cannot be modified.

Following on from these is the asset revision, which is incremented by 1 each time the asset is updated. An Asset Modification request that doesn't have the current version number will be rejected.

Subsequent to these fields, the modifications to the asset are contained in an array of objects, each of which has the following information:

- The field index of the contract element being changed
- The element of the field (for to identify the index number of the element within an array - complex types only)
- The Sub Field Index (to identify the field within the object in the array - complex types only)
- An instruction on whether to add or delete an element (for arrays)
- The new data being placed into the specified index

For asset modifications that require a vote to be passed, the TXID of a Result action showing a positive vote outcome for the change must be added as the final data item in the Asset Modification action. For detail on the voting process see the [Governance](governance) article.

![Asset Modification action](https://raw.githubusercontent.com/tokenized/docs/master/images/asset-modification-action.svg?sanitize=true "Asset Modification action") {.frame .centered .padded}

<a name="asset-creation-update"></a>
### Asset Creation Update

When the contract sees the Asset Modification action land in its wallet, it evaluates the action and looks to ensure that the modifications are valid.

If the contract determines that the amendment is valid, it issues a full Asset Creation action including the full details of the asset, the updated version number and a new timestamp.

From this moment, all transaction requests to the contract must abide by any amended rules that apply to the asset.

![Updated Contract Formation action](https://raw.githubusercontent.com/tokenized/docs/master/images/asset-creation-action-amendment.svg?sanitize=true "Updated Contract Formation action") {.frame .centered .padded}

<a name="asset-types"></a>
## Asset Types

When a tokenized asset is created, it includes a payload that defines the metadata that are attached to that particular token or tokens. The tokenized protocol is broad enough that any type of token can be developed and created.

For the initial release of the Tokenized protocol, the following 6 asset types will be available:

<a name="coupons"></a>
### Coupons (COU)

Coupons represent an asset that gives the bearer a right to procure a good or service with terms that are different to those under which someone without a coupon would need to agree to. This may include a discounted price, longer warranty, free installation or any other add-on or benefit.

<a name="loyalty-points"></a>
### Loyalty Points (LOY)

Loyalty points allow a merchant or business to reward repeat customers with tokens that can later be redeemed for discounted or free goods and services. Examples include coffee tokens (buy 10 coffees, get one free), airline miles (1 point per mile flown) and more.

<a name="membership"></a>
### Membership (MEM)

A membership token is a token that is usually handed out in a quantity of one.  The possession of a membership token signifies the belonging of the bearer to a defined group.  As a few examples, membership tokens can be used to represent membership in a Board of Directors, a non-profit organization, or even a special interest club.  Membership tokens can allow access to certain rights/privileges that members of the particular group are entitled, as well as any duties/responsibilities. This might include entry to a physical location such as a gym or club, or entry to a restricted part of a website such as a forum or members only zone.

<a name="common-share"></a>
### Common Share (SHC)

A common share is a share of a company providing the owner with a right to vote at shareholder meetings and to receive a part of the company profits as a dividend.

<a name="admission-ticket"></a>
### Admission Ticket (TIC)

An admission ticket confers upon its owner a certain right, especially to enter a place, travel by public transport, or participate in an event. Once the ticket has been 'redeemed', the record of ownership remains in the users wallet similar to a 'ticket stub'. Tickets can be used for any event including conferences, arena concerts, sports events, or to buy pay per view rights to an event streamed over the internet.

<a name="currency"></a>
### Currency (CUR)

Currency represents a tokenized version of a fiat currency. This is something that is issued and controlled by a legally entitled entity as a representative token of the currency being tokenized.