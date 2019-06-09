# Protocol Actions

- [Introduction](#introduction)
- [Header Fields](#header-fields)
- [Available Actions](#all-actions)

<a name="introduction"></a>
## Introduction

The following actions break down the construction of a Tokenized protocol message. The action is constructed by building a single string from each of the elements in order. Each field within the action is given a specific type, including standard types and compound types.

See the [Transactions article](../concepts/transactions) for details on how to construct a complete transaction.

<a name="header-fields"></a>
## Header Fields

Every protocol action is prepended with a header that specifies the necessary details about the subsequent action contents.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that determines the structure of the action payload and field definitions.
        </td>
    </tr>
    <tr>
        <td>ActionCode</td>
        <td>
            fixedchar(2)
        </td>
        <td>
            The Action Code that determines the expected contents of the action payload. Example: C1
        </td>
    </tr>
</table>

<a name="all-actions"></a>
## Available Actions

<div class="content-list collection-method-list" markdown="1">
- [Asset Definition](#action-asset-definition)
- [Asset Creation](#action-asset-creation)
- [Asset Modification](#action-asset-modification)
- [Contract Offer](#action-contract-offer)
- [Contract Formation](#action-contract-formation)
- [Contract Amendment](#action-contract-amendment)
- [Static Contract Formation](#action-static-contract-formation)
- [Contract Address Change](#action-contract-address-change)
- [Order](#action-order)
- [Freeze](#action-freeze)
- [Thaw](#action-thaw)
- [Confiscation](#action-confiscation)
- [Reconciliation](#action-reconciliation)
- [Proposal](#action-proposal)
- [Vote](#action-vote)
- [Ballot Cast](#action-ballot-cast)
- [Ballot Counted](#action-ballot-counted)
- [Result](#action-result)
- [Message](#action-message)
- [Rejection](#action-rejection)
- [Establishment](#action-establishment)
- [Addition](#action-addition)
- [Alteration](#action-alteration)
- [Removal](#action-removal)
- [Transfer](#action-transfer)
- [Settlement](#action-settlement)
</div>

<a name="action-asset-definition"></a>
#### Asset Definition

This action is used by the administration to define the properties/characteristics of the asset (token) that it wants to create. An asset has a unique identifier called AssetID = AssetType + base58(AssetCode + checksum). An asset is always linked to a contract that is identified by the public address of the Contract wallet.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>A1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: COU
        </td>
    </tr>
    <tr>
        <td>AssetAuthFlags</td>
        <td>
            varbin(8)
        </td>
        <td>
            A set of switches that define the authorization rules for this asset. See the Authorization Flags documentation for more detail.
            
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>TradeRestrictions</td>
        <td>
            <a href="resources#resource-polities">Polity[16]</a>
        </td>
        <td>
            If specified, the asset can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.
             Example: GBR
        </td>
    </tr>
    <tr>
        <td>EnforcementOrdersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make enforcement orders on user tokens and balances, otherwise set to false to disable this feature.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>VotingRights</td>
        <td>
            bool
        </td>
        <td>
            When false holders of this asset will not be able to vote for tokens of this asset even on voting systems in which vote multiplers are not permitted.
            
        </td>
    </tr>
    <tr>
        <td>VoteMultiplier</td>
        <td>
            uint(1)
        </td>
        <td>
            Multiplies a vote by the specified integer. Where 1 token is equal to 1 vote with a 1 for vote multipler (normal), 1 token = 3 votes with a multiplier of 3, for example. If zero, then holders of this asset don't get any votes for their tokens.
             Example: 3
        </td>
    </tr>
    <tr>
        <td>AdministrationProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make proposals outside of the smart contract scope.
            General Governance Example: true
        </td>
    </tr>
    <tr>
        <td>HolderProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if a holder is permitted to make proposals outside of the smart contract scope.
             Example: true
        </td>
    </tr>
    <tr>
        <td>AssetModificationGovernance</td>
        <td>
            uint(1)
        </td>
        <td>
            Supported values: 1 - Contract-wide Asset Governance. 0 - Asset-wide Asset Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the asset auth flags, then the vote will either be a contract-wide vote (all assets vote on the referendum/initiative) or an asset-wide vote (only this asset votes on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>TokenQty</td>
        <td>
            uint(8)
        </td>
        <td>
            The number of tokens to issue with this asset. Set to greater than zero for fungible tokens. If the value is 1 then it becomes a non-fungible token, where the contract would have many assets. Set to 0 to represent a placeholder asset, where tokens are to be issued later, or to represent a decomissioned asset where all tokens have been revoked.
             Example: 1000000
        </td>
    </tr>
    <tr>
        <td>AssetPayload</td>
        <td>
            varbin(16)
        </td>
        <td>
            A custom payload that contains meta data about this asset. Payload structure and length is dependent on the asset type chosen. See asset documentation for more details.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Administration's Public Address</td>
        <td>This action can only come from the administration.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that this asset should be assigned to. Must include enough for the responding action.</td>
    </tr>
</table>


<hr />



<a name="action-asset-creation"></a>
#### Asset Creation

This action creates an asset in response to the administration's instructions in the Definition Action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>A2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>AssetIndex</td>
        <td>
            uint(8)
        </td>
        <td>
            The index of the asset within the contract. First asset is zero, second is one. Used to derive the asset code.
            
        </td>
    </tr>
    <tr>
        <td>AssetAuthFlags</td>
        <td>
            varbin(8)
        </td>
        <td>
            A set of switches that define the authorization rules for this asset. See the Authorization Flags documentation for more detail.
            
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>TradeRestrictions</td>
        <td>
            <a href="resources#resource-polities">Polity[16]</a>
        </td>
        <td>
            If specified, the asset can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.
             Example: GBR
        </td>
    </tr>
    <tr>
        <td>EnforcementOrdersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make enforcement orders on user tokens and balances, otherwise set to false to disable this feature.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>VotingRights</td>
        <td>
            bool
        </td>
        <td>
            When false holders of this asset will not be able to vote for tokens of this asset even on voting systems in which vote multiplers are not permitted.
            
        </td>
    </tr>
    <tr>
        <td>VoteMultiplier</td>
        <td>
            uint(1)
        </td>
        <td>
            Multiplies a vote by the specified integer. Where 1 token is equal to 1 vote with a 1 for vote multipler (normal), 1 token = 3 votes with a multiplier of 3, for example. If zero, then holders of this asset don't get any votes for their tokens.
             Example: 3
        </td>
    </tr>
    <tr>
        <td>AdministrationProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make proposals outside of the smart contract scope.
            General Governance Example: true
        </td>
    </tr>
    <tr>
        <td>HolderProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if a holder is permitted to make proposals outside of the smart contract scope.
             Example: true
        </td>
    </tr>
    <tr>
        <td>AssetModificationGovernance</td>
        <td>
            uint(1)
        </td>
        <td>
            Supported values: 1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the asset auth flags, then the vote will either be a contract-wide vote (all assets vote on the referendum/initiative) or an asset-wide vote (only this asset votes on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>TokenQty</td>
        <td>
            uint(8)
        </td>
        <td>
            The number of tokens to issue with this asset. Set to greater than zero for fungible tokens. If the value is 1 then it becomes a non-fungible token, where the contract would have many assets. Set to 0 to represent a placeholder asset, where tokens are to be issued later, or to represent a decomissioned asset where all tokens have been revoked.
             Example: 1000000
        </td>
    </tr>
    <tr>
        <td>AssetPayload</td>
        <td>
            varbin(16)
        </td>
        <td>
            A custom payload that contains meta data about this asset. Payload structure and length is dependent on the asset type chosen. See asset documentation for more details.
            
        </td>
    </tr>
    <tr>
        <td>AssetRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            A counter for the number of times this asset has been revised using a modification action.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration or operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that this asset was assigned to.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Required so that users can monitor transactions to the contract for updates to contract/assets.</td>
    </tr>
</table>


<hr />



<a name="action-asset-modification"></a>
#### Asset Modification

Token Dilutions, Call Backs/Revocations, burning etc.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>A3</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>AssetRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            The current revision figure to ensure the modification provided is based on the latest version.
            Cannot be Amended Example: 0
        </td>
    </tr>
    <tr>
        <td>Amendments</td>
        <td>
            <a href="field-types#type-amendment">Amendment[8]</a>
        </td>
        <td>
            A collection of modifications to perform on this asset.
            
        </td>
    </tr>
    <tr>
        <td>RefTxID</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            The Bitcoin transaction ID of the associated result action that permitted the modifications. See Governance for more details.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Administration's Public Address</td>
        <td>This action can only come from the administration.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that this asset currently belongs to. Must include enough for the responding action.</td>
    </tr>
</table>


<hr />



<a name="action-contract-offer"></a>
#### Contract Offer

Allows the administration to tell the smart contract what they want the details (labels, data, T&C's, etc.) of the Contract to be on-chain in a public and immutable way. The Contract Offer action 'initializes' a generic smart contract that has been spun up by either the smart contract operator or the administration. This on-chain action allows for the positive response from the smart contract with either a Contract Formation Action or a Rejection Action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ContractName</td>
        <td>
            varchar(8)
        </td>
        <td>
            Can be any unique identifying string, including human readable names for branding/vanity purposes. Contract identifier (instance) is the bitcoin public key hash address. If the public address is lost, then the administration will have to reissue the entire contract, Asset Definition and tokens with the new public address. Smart contracts can be branded and specialized to suit any terms and conditions.

             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreementType</td>
        <td>
            uint(1)
        </td>
        <td>
            1 - SHA-256 Hash, 2 - Tokenized Body of Agreement Format
            Body of Agreement - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreement</td>
        <td>
            varbin(32)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full terms and conditions of an agreement in the Tokenized Body of Agreement format.  This is specific to the smart contract and relevant Assets.  Legal and technical information.
            
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            varchar(8)
        </td>
        <td>
            Describes the purpose of the contract.
             Example: Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="field-types#type-document">Document[8]</a>
        </td>
        <td>
            Supporting documents that are important to the contract.
            
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Law - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate total smart contract running costs for the entire life of the contract. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.
            Contract Expiration - Amendments can be restricted to a vote. Example: Wed May 09 2018 00:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(8)
        </td>
        <td>
            Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the issuer (company), information about the asset, legal information, etc.  There will also be a way for token owners to vote on this page and contact details with the issuer/tokenized companies. Could be a IPv6/IPv4, or txn-id for on-chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>Issuer</td>
        <td>
            <a href="field-types#type-entity">Entity</a>
        </td>
        <td>
            The issuer of this contract.
            
        </td>
    </tr>
    <tr>
        <td>IssuerLogoURL</td>
        <td>
            varchar(8)
        </td>
        <td>
            The URL of the issuer's logo.
             Example: https://example.com/images/logo.png
        </td>
    </tr>
    <tr>
        <td>ContractOperatorIncluded</td>
        <td>
            bool
        </td>
        <td>
            If true, then the second input is a contract operator. If false, then all additional inputs are just funding and "includes" fields are skipped in serialization.
            
        </td>
    </tr>
    <tr>
        <td>ContractOperator</td>
        <td>
            <a href="field-types#type-entity">Entity</a>
        </td>
        <td>
            An additional entity with operator access to the contract.
            
        </td>
    </tr>
    <tr>
        <td>ContractAuthFlags</td>
        <td>
            varbin(16)
        </td>
        <td>
            A set of switches that define the authorization rules for this contract. See the Authorization Flags documentation for more detail. Other terms and conditions that are out of the smart contract's control should be listed in the Body of Agreement.
            Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.
        </td>
    </tr>
    <tr>
        <td>ContractFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Satoshis required to be paid to the contract for each asset action.
            
        </td>
    </tr>
    <tr>
        <td>VotingSystems</td>
        <td>
            <a href="field-types#type-voting-system">VotingSystem[8]</a>
        </td>
        <td>
            A list of voting systems.
            
        </td>
    </tr>
    <tr>
        <td>RestrictedQtyAssets</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI
            Qty of Assets - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>AdministrationProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make proposals outside of the smart contract scope.
            General Governance Example: true
        </td>
    </tr>
    <tr>
        <td>HolderProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if a holder is permitted to make proposals outside of the smart contract scope.
             Example: true
        </td>
    </tr>
    <tr>
        <td>Oracles</td>
        <td>
            <a href="field-types#type-oracle">Oracle[8]</a>
        </td>
        <td>
            A list of oracles that provide approval for all token transfers for all assets under the contract.
            
        </td>
    </tr>
    <tr>
        <td>MasterPKH</td>
        <td>
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            The public key hash of the contract's master key. This key has the ability to change the active contract address in case of a security failure with the active contract key.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Administration's Public Address</td>
        <td>The smart contract sets the administration's public address with whatever public address is in Index 0 of the first valid Contract Offer.  From then on, the SC will only respond to 'commands' (request actions) from this address with respect to actions that are controlled by the administration according to the protocol.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>Contract Operator's Public Address (Optional)</td>
        <td>Can also be used as a cold storage backup for the issuer. This is important if the issuer wants to be able to change their address as changes to the issuer or operator pkh in an amendment require signatures from both the issuer and the operator pkhs. The one exception to this rule, the Contract Operator can nominate a secondary controlling public address that can act on behalf of the issuer for issuer related requests. Typically this will be the Smart Contract Operator.
</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>A contract address that has no other contract associated to it already.</td>
    </tr>
</table>


<hr />



<a name="action-contract-formation"></a>
#### Contract Formation

This txn is created by the contract (smart contract/off-chain agent/token contract) upon receipt of a valid Contract Offer Action from the administration.  The smart contract will execute on a server controlled by the administration, or a smart contract operator on their behalf.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ContractName</td>
        <td>
            varchar(8)
        </td>
        <td>
            Can be any unique identifying string, including human readable names for branding/vanity purposes. Contract identifier (instance) is the bitcoin public key hash address. If the public address is lost, then the administration will have to reissue the entire contract, asset definition and tokens with the new public address. Smart contracts can be branded and specialized to suit any terms and conditions.

             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreementType</td>
        <td>
            uint(1)
        </td>
        <td>
            1 - SHA-256 Hash, 2 - Tokenized Body of Agreement Format
            Body of Agreement - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreement</td>
        <td>
            varbin(32)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full terms and conditions of an agreement in the Tokenized Body of Agreement format.  This is specific to the smart contract and relevant Assets.  Legal and technical information.
            
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            varchar(8)
        </td>
        <td>
            Describes the purpose of the contract.
             Example: Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="field-types#type-document">Document[8]</a>
        </td>
        <td>
            Supporting documents that are important to the contract.
            
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Law - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.
            Contract Expiration - Amendments can be restricted to a vote. Example: Wed May 09 2018 00:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes.  0 is valid. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>Issuer</td>
        <td>
            <a href="field-types#type-entity">Entity</a>
        </td>
        <td>
            The issuer of this contract.
            
        </td>
    </tr>
    <tr>
        <td>IssuerLogoURL</td>
        <td>
            varchar(8)
        </td>
        <td>
            The URL of the issuer's logo.
             Example: https://example.tld/images/logo.png
        </td>
    </tr>
    <tr>
        <td>ContractOperatorIncluded</td>
        <td>
            bool
        </td>
        <td>
            If true, then the second input is a contract operator. If false, then all additional inputs are just funding and "includes" fields are skipped in serialization.
            
        </td>
    </tr>
    <tr>
        <td>ContractOperator</td>
        <td>
            <a href="field-types#type-entity">Entity</a>
        </td>
        <td>
            An additional entity with operator access to the contract.
            
        </td>
    </tr>
    <tr>
        <td>ContractAuthFlags</td>
        <td>
            varbin(16)
        </td>
        <td>
            A set of switches that define the authorization rules for this contract. See the Authorization Flags documentation for more detail. Other terms and conditions that are out of the smart contract's control should be listed in the Body of Agreement
            Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.
        </td>
    </tr>
    <tr>
        <td>ContractFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Satoshis required to be paid to the contract for each asset action.
            
        </td>
    </tr>
    <tr>
        <td>VotingSystems</td>
        <td>
            <a href="field-types#type-voting-system">VotingSystem[8]</a>
        </td>
        <td>
            A list voting systems.
            
        </td>
    </tr>
    <tr>
        <td>RestrictedQtyAssets</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI
            Qty of Assets - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>AdministrationProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make proposals outside of the smart contract scope.
            General Governance Example: true
        </td>
    </tr>
    <tr>
        <td>HolderProposal</td>
        <td>
            bool
        </td>
        <td>
            Set to true if a holder is permitted to make proposals outside of the smart contract scope.
             Example: true
        </td>
    </tr>
    <tr>
        <td>Oracles</td>
        <td>
            <a href="field-types#type-oracle">Oracle[8]</a>
        </td>
        <td>
            A list of oracles that provide approval for all token transfers for all assets under the contract.
            
        </td>
    </tr>
    <tr>
        <td>MasterPKH</td>
        <td>
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            The public key hash of the contract's master key. This key has the ability to change the active contract address in case of a security failure with the active contract key.
            
        </td>
    </tr>
    <tr>
        <td>ContractRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            A counter for the number of times this contract has been revised using an amendment action.
            Can't be changed by the administration or smart contract operator. Example: 0
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The related contract address.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Required so that users can monitor transactions to the contract for updates to contract/assets.</td>
    </tr>
</table>


<hr />



<a name="action-contract-amendment"></a>
#### Contract Amendment

The administration can initiate an amendment to the contract establishment metadata. The ability to make an amendment to the contract is restricted by the Authorization Flag set on the current revision of Contract Formation action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C3</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ChangeAdministrationAddress</td>
        <td>
            bool
        </td>
        <td>
            Used to change the administration address.  The new administration address must be in the input[1] position. A change of the administration or operator address requires both the operator and the administration address to be in the inputs (both signatures) of the Contract Amendment action.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>ChangeOperatorAddress</td>
        <td>
            bool
        </td>
        <td>
            Used to change the smart contract operator address.  The new operator address must be in the input[1] position, unless the administration is being changed too, then it is in input[2]. A change of the administration or operator address requires both the operator and the administration address to be in the inputs (both signatures) of the Contract Amendment action.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>ContractRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            Counter 0 to (2^32)-1
             Example: 42
        </td>
    </tr>
    <tr>
        <td>Amendments</td>
        <td>
            <a href="field-types#type-amendment">Amendment[8]</a>
        </td>
        <td>
            A collection of modifications to perform on this contract.
            
        </td>
    </tr>
    <tr>
        <td>RefTxID</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            The Bitcoin transaction ID of the associated result action that permitted the modifications. See Governance for more details.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Administration's Public Address</td>
        <td>This action can only come from the administration.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>New Administration Public Address</td>
        <td>Only treated as the new administration address when the Change Administration Address flag is set to true.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The related contract address.</td>
    </tr>
</table>


<hr />



<a name="action-static-contract-formation"></a>
#### Static Contract Formation

Static Contract Formation Action

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C4</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ContractName</td>
        <td>
            varchar(8)
        </td>
        <td>
            Can be any unique identifying string, including human readable names for branding/vanity purposes. Contract identifier (instance) is the bitcoin public address. If the public address is lost, then the administration will have to reissue the entire contract, Asset Definition and tokens with the new public address. Smart contracts can be branded and specialized to suit any terms and conditions.

             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>ContractCode</td>
        <td>
            <a href="field-types#type-contract-code">ContractCode</a>
        </td>
        <td>
            32 randomly generated bytes. Each Contract Code should be unique. The Contract ID will be human facing and will be the Contract Code, with a checksum, encoded in base58 and prefixed by 'CON'. Contract ID = CON + base58(ContractCode + checksum).  Eg. Contract ID = 'CON18RDoKK7Ed5zid2FkKVy7q3rULr4tgfjr4'
            
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreementType</td>
        <td>
            uint(1)
        </td>
        <td>
            1 - SHA-256 Hash, 2 - Tokenized Body of Agreement Format
            Body of Agreement - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreement</td>
        <td>
            varbin(32)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full terms and conditions of an agreement in the Tokenized Body of Agreement format.  This is specific to the smart contract and relevant Assets.  Legal and technical information.
            
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            varchar(8)
        </td>
        <td>
            Describes the purpose of the contract.
             Example: Non-Disclosure Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="field-types#type-document">Document[8]</a>
        </td>
        <td>
            Supporting documents that are important to the contract.
            
        </td>
    </tr>
    <tr>
        <td>ContractRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            Counter 0 to (2^32)-1
             Example: 0
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
             Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
             Example: US-CA
        </td>
    </tr>
    <tr>
        <td>EffectiveDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Start date of the contract.
            
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.
            
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the issuer (company), information about the Asset, legal information, etc.  There will also be a way for token owners to vote on this page and contact details with the issuer/tokenized companies. Could be a IPv6/IPv4, or txn-id for on chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>PrevRevTxID</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            The Tx-ID of the previous contract revision.
            
        </td>
    </tr>
    <tr>
        <td>Entities</td>
        <td>
            <a href="field-types#type-entity">Entity[8]</a>
        </td>
        <td>
            A list of legal entities associated with this contract.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Issuer or Party X Public Address</td>
        <td>Any number of involved parties with this contract.</td>
    </tr>
</table>




<hr />



<a name="action-contract-address-change"></a>
#### Contract Address Change

This txn is signed by the master contract key defined in the contract formation and changes the active contract address which the contract uses to receive and respond to requests. This is a worst case scenario fallback to only be used when the contract private key is believed to be exposed.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C5</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>NewContractPKH</td>
        <td>
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            The address to be used by all future requests/responses for the contract.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the action was created.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Master Public Address</td>
        <td>The contract master address.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Currently active, and soon to be deactivated, contract address.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>New Contract Public Address</td>
        <td>The address the contract will use from this point forward.</td>
    </tr>
</table>


<hr />



<a name="action-order"></a>
#### Order

Used by the administration to signal to the smart contract that the tokens that a particular public address(es) owns are to be confiscated, frozen, thawed or reconciled.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>E1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ComplianceAction</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            Freeze (F), Thaw (T), Confiscate (C), Reconcile (R)
             Example: F
        </td>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>TargetAddresses</td>
        <td>
            <a href="field-types#type-target-address">TargetAddress[16]</a>
        </td>
        <td>
            The holders and quantities that are effected by the order. For a contract or asset wide freeze only the contract address is specified. Zero quantities are invalid unless it is for the contract address in an asset wide or contract wide freeze. In a thaw order this field is not serialized, because the entire freeze from the FreezeTxId freeze action will be thawed.
            
        </td>
    </tr>
    <tr>
        <td>FreezeTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            The tx id of the freeze action that is being thawed. Only serialized for thaw orders.
            
        </td>
    </tr>
    <tr>
        <td>FreezePeriod</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Used for a 'time out'.  Tokens are automatically unfrozen after the expiration timestamp without requiring a Thaw Action. Null value for Thaw, Confiscation and Reconciallitaion orders.
             Example: Tue Oct 09 2018 05:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>DepositAddress</td>
        <td>
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            The public address for confiscated tokens to be deposited in.  Null for Freeze, Thaw, actions.
            Eventually the supporting evidence/explanation can be supported by a Subfield that has the public address (and a signed message) owned by a legal authority for ID verification/certification purposes.
        </td>
    </tr>
    <tr>
        <td>AuthorityIncluded</td>
        <td>
            bool
        </td>
        <td>
            Specifies if an authority signature is included. For Reconcialitaion actions all authority signature related fields are skipped during serialization.
            
        </td>
    </tr>
    <tr>
        <td>AuthorityName</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. Enforcement Authority Name (eg. Issuer, Queensland Police Service, Tokenized, etc.)
             Example: Supreme and District Courts Brisbane
        </td>
    </tr>
    <tr>
        <td>AuthorityPublicKey</td>
        <td>
            varbin(8)
        </td>
        <td>
            Length 0-255 bytes. Public Key associated with the Enforcement Authority
            
        </td>
    </tr>
    <tr>
        <td>SignatureAlgorithm</td>
        <td>
            uint(1)
        </td>
        <td>
            Algorithm used for order signature. Only valid value is currently 1 = ECDSA+secp256k1
             Example: 1
        </td>
    </tr>
    <tr>
        <td>OrderSignature</td>
        <td>
            varbin(8)
        </td>
        <td>
            Length 0-255 bytes. Signature for a message that lists out the target addresses and deposit address. Signature of (Contract PKH, Compliance Action, Authority Name, Asset Code, Supporting Evidence Hash, FreezePeriod, TargetAddresses, and DepositAddress)
            
        </td>
    </tr>
    <tr>
        <td>SupportingEvidenceHash</td>
        <td>
            bin(32)
        </td>
        <td>
            SHA-256: warrant, court order, etc.
            
        </td>
    </tr>
    <tr>
        <td>RefTxs</td>
        <td>
            varbin(32)
        </td>
        <td>
            The request/response actions that were dropped.  The entire txn for both actions is included as evidence that the actions were accepted into the mempool at one point and that the senders (token/Bitcoin) signed their intent to transfer.  The management of this record keeping is off-chain and managed by the administration or operator to preserve the integrity of the state of the tokens. Only applicable for reconcilliation actions.  No subfield when F, T, R is selected as the Compliance Action subfield.
            Can be null.  Dropped actions that require a reconciliation action to fix the break in the chain are considered to be an extremely rare event.
        </td>
    </tr>
    <tr>
        <td>BitcoinDispersions</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[16]</a>
        </td>
        <td>
            Index of address in TargetAddresses and amount of bitcoin (in satoshis) they are receiving in exchange for their tokens.
            
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(32)
        </td>
        <td>
            A message to include with the enforcement order.
             Example: Compelled by a court order.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Administration's Public Address</td>
        <td>This action can only come from the administration.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Contract fee and funding for response transaction.</td>
    </tr>
</table>


<hr />



<a name="action-freeze"></a>
#### Freeze

The contract responding to an Order action to freeze assets. To be used to comply with contractual/legal/issuer requirements. The target public address(es) will be marked as frozen. However the Freeze action publishes this fact to the public blockchain for transparency. The contract will not respond to any actions requested by the frozen address.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>E2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[16]</a>
        </td>
        <td>
            Indices to addresses in outputs and the quantities being frozen. If the only address is the contract address and the asset code is zeros, then it is a contract wide freeze. If the only address is the contract address and the asset code is specified, then it is an asset wide freeze.
            
        </td>
    </tr>
    <tr>
        <td>FreezePeriod</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Used for a 'time out'.  Tokens are automatically unfrozen after the expiration timestamp without requiring a Thaw Action.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Target Public Address X</td>
        <td>If Target Public Address is the Contract Address then the entire contract is frozen.  All request actions during the Freeze period will be ignored and rejected when the contract is thawed and rebuilds.</td>
    </tr>
</table>


<hr />



<a name="action-thaw"></a>
#### Thaw

The contract responding to an Order action to thaw assets. To be used to comply with contractual obligations or legal requirements. The Alleged Offender's tokens will be unfrozen to allow them to resume normal exchange and governance activities.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>E3</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>FreezeTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            The tx id of the freeze action that is being reversed.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Target Public Address X</td>
        <td>Can be the Contract Address for a 'Contract-wide' Thaw in response to a Contract-wide Freeze.</td>
    </tr>
</table>


<hr />



<a name="action-confiscation"></a>
#### Confiscation

The contract responding to an Order action to confiscate assets. To be used to comply with contractual obligations, legal and/or issuer requirements.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>E4</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[16]</a>
        </td>
        <td>
            The holders effected by the confiscation and their balance remaining.
            
        </td>
    </tr>
    <tr>
        <td>DepositQty</td>
        <td>
            uint(8)
        </td>
        <td>
            Deposit address's token balance after confiscation.
             Example: 10000
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Target Public Address X</td>
        <td>Can be the Contract Address for a 'Contract-wide' Confiscation.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>Deposit Public Address</td>
        <td>Dust limit rule minimum value output of 546</td>
    </tr>
</table>


<hr />



<a name="action-reconciliation"></a>
#### Reconciliation

The contract responding to an Order action to reconcile assets. To be used at the direction of the administration to fix record keeping errors with bitcoin and token balances.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>E5</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[16]</a>
        </td>
        <td>
            The holders effected by the reconciliation and their balance remaining.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Target Public Address X</td>
        <td>546 minimum.  If N bitcoin needs to be sent to the address, then this will be the output that receives the Bitcoin.</td>
    </tr>
</table>


<hr />



<a name="action-proposal"></a>
#### Proposal

Allows the Administration/Token Holders to propose a change (aka Initiative/Shareholder vote).  A significant cost - specified in the Contract Formation - can be attached to this action when sent from Token Holders to reduce spam, as the resulting vote will be put to all token owners.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>G1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Initiator</td>
        <td>
            uint(1)
        </td>
        <td>
            Who initiated the proposal. Supported values: 0 - Administration, 1 - Holder
            
        </td>
    </tr>
    <tr>
        <td>AssetSpecificVote</td>
        <td>
            bool
        </td>
        <td>
            When true this proposal is specific to an asset and the asset type and asset code fields are serialized.
            
        </td>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>VoteSystem</td>
        <td>
            uint(1)
        </td>
        <td>
            X for Vote System X. (1-255, 0 is not valid.)
             Example: 1
        </td>
    </tr>
    <tr>
        <td>Specific</td>
        <td>
            bool
        </td>
        <td>
            When true the ProposedAmendments field is included and specifies the exact changes to make to the contract/asset on chain. When false this is just a general proposal like a strategy/direction and doesn't result in any on chain update.
            
        </td>
    </tr>
    <tr>
        <td>ProposedAmendments</td>
        <td>
            <a href="field-types#type-amendment">Amendment[8]</a>
        </td>
        <td>
            Each element contains details of which fields to modify, or delete. Because the number of fields in a Contract and Asset is dynamic due to some fields being able to be repeated, the index value of the field needs to be calculated against the Contract or Asset the changes are to apply to. In the event of a Vote being created from this Initiative, the changes will be applied to the version of the Contract or Asset at that time.
            
        </td>
    </tr>
    <tr>
        <td>VoteOptions</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option. Typical votes will likely be multiple choice or Y/N. Vote instances are identified by the Tx-ID. AB would be used for Y/N (binary) type votes. When Specific is true, only AB is a valid value.
             Example: ABCDEFGHIJKLMNO
        </td>
    </tr>
    <tr>
        <td>VoteMax</td>
        <td>
            uint(1)
        </td>
        <td>
            Range: 1-X. How many selections can a voter make in a Ballot Cast. 1 is selected for Y/N (binary). When Specific is true, only 1 is a valid value.
             Example: 15
        </td>
    </tr>
    <tr>
        <td>ProposalDescription</td>
        <td>
            varchar(32)
        </td>
        <td>
            Length restricted by the Bitcoin protocol. 0 is valid. Description or details of the vote
             Example: Change the name of the Contract.
        </td>
    </tr>
    <tr>
        <td>ProposalDocumentHash</td>
        <td>
            bin(32)
        </td>
        <td>
            SHA256 Hash of the proposal document to be distributed to voters.
             Example: 77201b0094f50df309f0343e4f44dae64d0de503c91038faf2c6b039f9f18aec
        </td>
    </tr>
    <tr>
        <td>VoteCutOffTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Ballot casts after this timestamp will not be included. The vote has finished.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Operator / Token Owner's Public Address</td>
        <td>The user making the proposal for this contract.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Includes contract fee and holder proposal fee if applicable.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>Contract Public Address</td>
        <td>Fund the Result TX at Vote cut off</td>
    </tr>
</table>


<hr />



<a name="action-vote"></a>
#### Vote

A vote is created by the Contract in response to a valid Proposal Action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>G2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Required so that users can monitor transactions to the contract for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-ballot-cast"></a>
#### Ballot Cast

Used by Token Owners to cast their ballot (vote) on proposals. 1 Vote per token unless a vote multiplier is specified in the relevant Asset Definition action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>G3</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>VoteTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            Tx ID of the Vote the Ballot Cast is being made for.
            
        </td>
    </tr>
    <tr>
        <td>Vote</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 1-255 bytes. 0 is not valid. Max length is the VoteMax value from the Proposal action. Accept, Reject, Abstain, Spoiled, Multiple Choice, or Preference List. 15 options total. Order of preference. 1st position = 1st choice. 2nd position = 2nd choice, etc. A is always Accept and B is always reject in a Y/N votes.
             Example: A
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Token Owner's Public Address</td>
        <td>The user casting the ballot for this contract.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Funds ballot cast response.</td>
    </tr>
</table>


<hr />



<a name="action-ballot-counted"></a>
#### Ballot Counted

The smart contract will respond to a Ballot Cast action with a Ballot Counted action if the Ballot Cast is valid. If the Ballot Cast is not valid, then the smart contract will respond with a Rejection Action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>G4</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>VoteTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            Tx ID of the Vote the Ballot Cast is being made for.
            
        </td>
    </tr>
    <tr>
        <td>Vote</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 1-255 bytes. 0 is not valid. Max length is the VoteMax value from the Proposal action. Accept, Reject, Abstain, Spoiled, Multiple Choice, or Preference List. 15 options total. Order of preference. 1st position = 1st choice. 2nd position = 2nd choice, etc. A is always Accept and B is always reject in a Y/N votes.
             Example: A
        </td>
    </tr>
    <tr>
        <td>Quantity</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of votes counted for this ballot. Factors in vote multipliers if there are any allowed, otherwise it is just quantity of tokens held.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Required so that users can monitor transactions to the contract for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-result"></a>
#### Result

Once a vote has been completed the results are published. After the result is posted, it is up to the administration to send a contract/asset amendement if appropriate.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>G5</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AssetSpecificVote</td>
        <td>
            bool
        </td>
        <td>
            When true this proposal is specific to an asset and the asset type and asset code fields are serialized.
            
        </td>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset. It is generated by hashing the contract public key hash and the asset index. SHA256(contract PKH + asset index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Specific</td>
        <td>
            bool
        </td>
        <td>
            When true the ProposedAmendments field is included and specifies the exact changes to make to the Contract/Asset on chain. When false this is just a general proposal like a strategy/direction and doesn't result in any on chain update.
            
        </td>
    </tr>
    <tr>
        <td>ProposedAmendments</td>
        <td>
            <a href="field-types#type-amendment">Amendment[8]</a>
        </td>
        <td>
            Each element contains details of which fields to modify, or delete. Because the number of fields in a Contract and Asset is dynamic due to some fields being able to be repeated, the index value of the field needs to be calculated against the Contract or Asset the changes are to apply to. In the event of a Vote being created from this Initiative, the changes will be applied to the version of the Contract or Asset at that time.
            
        </td>
    </tr>
    <tr>
        <td>VoteTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            Link to the Vote Action txn.
            
        </td>
    </tr>
    <tr>
        <td>OptionTally</td>
        <td>
            uint64[8]
        </td>
        <td>
            List of number of valid votes counted for each vote option. Length is encoded like a regular list object, but must match the length of VoteOptions from the Proposal action.
            
        </td>
    </tr>
    <tr>
        <td>Result</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw for 1st place, all winning options are listed.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>Required so that users can monitor transactions to the contract for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-message"></a>
#### Message

The message action is a general purpose communication action. 'Twitter/SMS' for Issuers/Investors/Users. The message txn can also be used for passing partially signed txns on-chain, establishing private communication channels and EDI (receipting, invoices, PO, and private offers/bids). The messages are broken down by type for easy filtering in the a user's wallet. The Message Types are listed in the Message Types table.


<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>M1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AddressIndexes</td>
        <td>
            uint16[8]
        </td>
        <td>
            Associates the message to a particular output by the index.
            
        </td>
    </tr>
    <tr>
        <td>MessageType</td>
        <td>
            uint16
        </td>
        <td>
            Potential for up to 65,535 different message types. Values from resources/Messages.yaml
             Example: 6000
        </td>
    </tr>
    <tr>
        <td>MessagePayload</td>
        <td>
            varbin(32)
        </td>
        <td>
            Public or private (RSA public key, Diffie-Hellman). Issuers/Contracts can send the signifying amount of satoshis to themselves for public announcements or private 'notes' if encrypted. See Message Types for a full list of potential use cases.

             Example: Hello world!
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Sender Public Address</td>
        <td>The user sending the message.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Receiver Public Address"</td>
        <td>The recipient's address for the message, supplied by the sender.</td>
    </tr>
</table>


<hr />



<a name="action-rejection"></a>
#### Rejection

Used to reject request actions that do not comply with the Contract. If money is to be returned to a User then it is used in lieu of the Settlement Action to properly account for token balances. All Administration/User request Actions must be responded to by the Contract with an Action.  The only exception to this rule is when there is not enough fees in the first Action for the Contract response action to remain revenue neutral.  If not enough fees are attached to pay for the Contract response then the Contract will not respond.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>M2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AddressIndexes</td>
        <td>
            uint16[8]
        </td>
        <td>
            Associates the message to a particular output by the index.
            
        </td>
    </tr>
    <tr>
        <td>RejectAddressIndex</td>
        <td>
            uint(2)
        </td>
        <td>
            The address which is believed to have caused the rejection.
            
        </td>
    </tr>
    <tr>
        <td>RejectionCode</td>
        <td>
            <a href="resources#resource-rejections">RejectionCode</a>
        </td>
        <td>
            Classifies the rejection by a type.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(16)
        </td>
        <td>
            Length 0-65,535 bytes. Message that explains the reasoning for a rejection, if needed.  Most rejection types will be captured by the Rejection Type Subfield.
             Example: Sorry, you don't have enough tokens.
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address</td>
        <td>The contract that is performing this action.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>User / Contract public addresses</td>
        <td>The affected user or contract's publid addresses. Refunds all money provided in the request action, less fees</td>
    </tr>
</table>


<hr />



<a name="action-establishment"></a>
#### Establishment

Establishes an on-chain register.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>R1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(32)
        </td>
        <td>
            A custom message to include with this action.
             Example: North America Whitelist
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>The address of the associated register.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>Required so that users can monitor transactions to the register for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-addition"></a>
#### Addition

Adds an entry to the Register.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>R2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(32)
        </td>
        <td>
            A custom message to include with this action.
             Example: username
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>The address of the associated register.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>Required so that users can monitor transactions to the register for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-alteration"></a>
#### Alteration

A register entry/record can be altered.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>R3</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>EntryTxID</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            Transaction ID of the register entry to be altered.
            
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(32)
        </td>
        <td>
            A custom message to include with this action.
             Example: Changed Country of Residence
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>The address of the associated register.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>Required so that users can monitor transactions to the register for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-removal"></a>
#### Removal

Removes an entry/record from the Register.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>R4</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>EntryTxID</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>
            Transaction ID of the register entry to be altered.
            
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(32)
        </td>
        <td>
            A custom message to include with this action.
             Example: Removed due to violation of company policy.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>The address of the associated register.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Register Public Address</td>
        <td>Required so that users can monitor transactions to the register for notifications of this action.</td>
    </tr>
</table>


<hr />



<a name="action-transfer"></a>
#### Transfer

A Token Owner(s) Sends, Exchanges or Swaps a token(s) or Bitcoin for a token(s) or Bitcoin.  Can be as simple as sending a single token to a receiver.  Or can be as complex as many senders sending many different assets - controlled by many different smart contracts - to a number of receivers.  This action also supports atomic swaps (tokens for tokens).  Since many parties and contracts can be involved in a transfer and the corresponding settlement action, the partially signed T1 and T2 actions will need to be passed around on-chain with an M1 action, or off-chain.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>T1</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Assets</td>
        <td>
            <a href="field-types#type-asset-transfer">AssetTransfer[8]</a>
        </td>
        <td>
            The Assets involved in the Transfer Action.
            
        </td>
    </tr>
    <tr>
        <td>OfferExpiry</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            This prevents any party from holding on to the partially signed message as a form of an option.  Eg. the exchange at this price is valid for 30 mins.
            
        </td>
    </tr>
    <tr>
        <td>ExchangeFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Fixed amount of bitcoin being paid to an exchange for facilitating a transfer.
             Example: 0.01
        </td>
    </tr>
    <tr>
        <td>ExchangeFeeAddress</td>
        <td>
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            Identifies the public address that the exchange fee should be paid to.
            
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Asset Senders</td>
        <td>Asset (token) Sending Public Address. Assets[i].AssetSenders[j].Index references these inputs.</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address for Asset X</td>
        <td>Enough for the costs of the responding action, including any bitcoins being transfered, and the Contract Fee.</td>
    </tr>
</table>


<hr />



<a name="action-settlement"></a>
#### Settlement

Settles the transfer request of bitcoins and tokens from transfer (T1) actions.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>T2</td>
    </tr>
</table>


<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Assets</td>
        <td>
            <a href="field-types#type-asset-settlement">AssetSettlement[8]</a>
        </td>
        <td>
            The Assets settled by the transfer action.
            
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Cannot be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
</table>

##### Transaction Summary


<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Input</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Contract Public Address (Asset X)</td>
        <td>Contract (Asset X) in response to a transfer action with Asset X being sent to another address(es).</td>
    </tr>
</table>



<table>
   <tr>
        <th style="width:5%" class="text-center">Index</th>
        <th style="width:30%">Output</th>
        <th>Description</th>
   </tr>
   <tr>
        <td class="text-center">0</td>
        <td>Asset 1 Settlement Address X</td>
        <td>Address X that is being settled for Asset 1.</td>
    </tr>
</table>


<hr />


