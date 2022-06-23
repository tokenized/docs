# Protocol Actions

- [Introduction](#introduction)
- [Available Actions](#all-actions)
- [Field Types](#field-types)
- [Field Aliases](#field-aliases)

<a name="introduction"></a>

## Introduction

The following actions break down the construction of a Tokenized protocol message. The action is constructed by building a single string from each of the elements in order. Each field within the action is given a specific type, including standard types and compound types.

See the [Transactions article](../concepts/transactions) for details on how to construct a complete transaction.

<a name="all-actions"></a>

## Available Actions

<div class="content-list collection-method-list" markdown="1">

- [Contract Offer](#action-contract-offer)
- [Contract Formation](#action-contract-formation)
- [Contract Amendment](#action-contract-amendment)
- [Static Contract Formation](#action-static-contract-formation)
- [Contract Address Change](#action-contract-address-change)
- [Body Of Agreement Offer](#action-body-of-agreement-offer)
- [Body Of Agreement Formation](#action-body-of-agreement-formation)
- [Body Of Agreement Amendment](#action-body-of-agreement-amendment)
- [Instrument Definition](#action-instrument-definition)
- [Instrument Creation](#action-instrument-creation)
- [Instrument Modification](#action-instrument-modification)
- [Transfer](#action-transfer)
- [Settlement](#action-settlement)
- [Proposal](#action-proposal)
- [Vote](#action-vote)
- [Ballot Cast](#action-ballot-cast)
- [Ballot Counted](#action-ballot-counted)
- [Result](#action-result)
- [Order](#action-order)
- [Freeze](#action-freeze)
- [Thaw](#action-thaw)
- [Confiscation](#action-confiscation)
- [Reconciliation](#action-reconciliation)
- [Establishment](#action-establishment)
- [Addition](#action-addition)
- [Alteration](#action-alteration)
- [Removal](#action-removal)
- [Message](#action-message)
- [Rejection](#action-rejection)
</div>

<a name="action-contract-offer"></a>

#### Contract Offer

Allows the administration to tell the smart contract what they want the details (labels, data, T&amp;C&#39;s, etc.) of the Contract to be on-chain in a public and immutable way. The Contract Offer action &#39;initializes&#39; a generic smart contract that has been spun up by either the smart contract operator or the administration. This on-chain action allows for the positive response from the smart contract with either a Contract Formation Action or a Rejection Action.

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
            varchar(tiny)
        </td>
        <td>
            The name/title of the contract.
             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreementType</td>
        <td>
            uint(1)
        </td>
        <td>
            0 - No Body of agreement included 1 - SHA-256 Hash 2 - Tokenized Body of Agreement Format where the agreement is specified with a separate C6/C7 action
<br />
            Body of Agreement - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreement</td>
        <td>
            varbin(medium)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full agreement. If BodyOfAgreementType is 2 then this field is empty and the agreement is specified in a C6/C7 action. This is specific to the smart contract and relevant Instruments. Legal and technical information.
<br />
<br />
            This field is only valid when the field BodyOfAgreementType equals 1.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ContractType</td>
        <td>deprecated</td>
        <td>
            Deprecated for more specific type. Describes the purpose of the contract.
             Example: Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="#type-document">Document[tiny]</a>
        </td>
        <td>
            Supporting documents that are important to the contract.
</td>
    </tr>
    <tr>
        <td>(Deprecated)GoverningLaw</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. 5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Legal System - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Jurisdiction</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate total smart contract running costs for the entire life of the contract. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an &#39;Expired&#39; folder.
            Contract Expiration - Amendments can be restricted to a vote.
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the issuer (company), information about the instrument, legal information, etc.  There will also be a way for token owners to vote on this page and contact details with the issuer/tokenized companies. Could be a IPv6/IPv4, or txn-id for on-chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>Issuer</td>
        <td>
            <a href="#type-entity">Entity</a>
        </td>
        <td>
            The issuer of this contract.<br />            This field is only valid when the field ContractType equals 0.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)IssuerLogoURL</td>
        <td>deprecated</td>
        <td>
            The URL of the issuer&#39;s logo.
             Example: https://example.com/images/logo.png
        </td>
    </tr>
    <tr>
        <td>ContractOperatorIncluded</td>
        <td>
            bool
        </td>
        <td>
            If true, then the second input is a contract operator. If false, then all additional inputs are just funding and &#34;includes&#34; fields are skipped in serialization.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ContractOperator</td>
        <td>deprecated</td>
        <td>
            Deprecated for operator entity contract address. An additional entity with operator access to the contract.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracle</td>
        <td>deprecated</td>
        <td>
            The oracle that provided the signature used to verify the administration&#39;s identity and association with a parent contract if one is specified.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracleSignature</td>
        <td>deprecated</td>
        <td>
            The ECDSA signature provided by the oracle specified. The first input must correspond to the administration entity and, if a contract operator is included, the second input must correspond to the contract operator entity.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracleSigBlockHeight</td>
        <td>deprecated</td>
        <td>
            The block height of the block hash used in the oracle signature.  
        </td>
    </tr>
    <tr>
        <td>ContractFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Satoshis required to be paid to the contract for each instrument action.  
        </td>
    </tr>
    <tr>
        <td>VotingSystems</td>
        <td>
            <a href="#type-voting-system">VotingSystem[tiny]</a>
        </td>
        <td>
            A list of voting systems.  
        </td>
    </tr>
    <tr>
        <td>ContractPermissions</td>
        <td>
            varbin(small)
        </td>
        <td>
            A set of permission objects containing switches and field references that define the permissions for modifying this contract. See the Permission documentation for more detail.  
        </td>
    </tr>
    <tr>
        <td>RestrictedQtyInstruments</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of Instruments (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI
            Qty of Instruments - Amendments can be restricted to a vote. Example: 1
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
            <a href="#type-oracle">Oracle[tiny]</a>
        </td>
        <td>
            A list of oracles that provide approval for all token transfers for all instruments under the contract.  
        </td>
    </tr>
    <tr>
        <td>MasterAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s master key. This key has the ability to change the active contract address in case of a security failure with the active contract key.  
        </td>
    </tr>
    <tr>
        <td>EntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s parent entity. This is not valid for entity contracts, but required for instrument and service contracts to identify the entity parent contract.<br />
            This field is required when the field ContractType equals 1.
            This field is only valid when the field ContractType equals 1.
        </td>
    </tr>
    <tr>
        <td>OperatorEntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address for the operator&#39;s entity contract.<br />            This field is only valid when the field ContractOperatorIncluded equals true.
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            uint(1)
        </td>
        <td>
            Describes the purpose of the contract. 0 - Entity, 1 - Instrument
             Example: 0
        </td>
    </tr>
    <tr>
        <td>Services</td>
        <td>
            <a href="#type-service">Service[tiny]</a>
        </td>
        <td>
            The services provided by the contract entity.<br />            This field is only valid when the field ContractType equals 0.
        </td>
    </tr>
    <tr>
        <td>AdminIdentityCertificates</td>
        <td>
            <a href="#type-admin-identity-certificate">AdminIdentityCertificate[tiny]</a>
        </td>
        <td>
            Certificates providing proof of administrator/operator identities.  
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            <a href="#alias-legal-system">LegalSystem</a>
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Legal System - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            <a href="#alias-polity">Polity</a>
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
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
        <td>Administration&#39;s Public Address</td>
        <td>The smart contract sets the administration&#39;s public address with whatever public address is in Index 0 of the first valid Contract Offer.  From then on, the SC will only respond to &#39;commands&#39; (request actions) from this address with respect to actions that are controlled by the administration according to the protocol.</td>
    </tr>
   <tr>
        <td class="text-center">1</td>
        <td>Contract Operator&#39;s Public Address (Optional)</td>
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

This txn is created by the contract (smart contract/off-chain agent/token contract) upon receipt of a valid Contract Offer Action from the administration. The smart contract will execute on a server controlled by the administration, or a smart contract operator on their behalf.

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
            varchar(tiny)
        </td>
        <td>
            The name/title of the contract.
             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreementType</td>
        <td>
            uint(1)
        </td>
        <td>
            0 - No Body of agreement included 1 - SHA-256 Hash 2 - Tokenized Body of Agreement Format where the agreement is specified with a separate C6/C7 action<br />
            Body of Agreement - Amendments can be restricted to a vote. Example: 1
        </td>
    </tr>
    <tr>
        <td>BodyOfAgreement</td>
        <td>
            varbin(medium)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full agreement. If BodyOfAgreementType is 2 then this field is empty and the agreement is specified in a C6/C7 action. This is specific to the smart contract and relevant Instruments. Legal and technical information.<br /><br />            This field is only valid when the field BodyOfAgreementType equals 1.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ContractType</td>
        <td>deprecated</td>
        <td>
            Deprecated for more specific type. Describes the purpose of the contract.
             Example: Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="#type-document">Document[tiny]</a>
        </td>
        <td>
            Supporting documents that are important to the contract.
</td>
    </tr>
    <tr>
        <td>(Deprecated)GoverningLaw</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. 5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Legal System - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Jurisdiction</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an &#39;Expired&#39; folder.
            Contract Expiration - Amendments can be restricted to a vote.
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes.  0 is valid. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Instrument, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>Issuer</td>
        <td>
            <a href="#type-entity">Entity</a>
        </td>
        <td>
            The issuer of this contract.<br />            This field is only valid when the field ContractType equals 0.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)IssuerLogoURL</td>
        <td>deprecated</td>
        <td>
            Deprecated for data in the issuer entity. The URL of the issuer&#39;s logo.
             Example: https://example.tld/images/logo.png
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ContractOperator</td>
        <td>deprecated</td>
        <td>
            Deprecated for operator entity contract address. An additional entity with operator access to the contract.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracle</td>
        <td>deprecated</td>
        <td>
            The oracle that provided the signature used to verify the administration&#39;s identity.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracleSignature</td>
        <td>deprecated</td>
        <td>
            The ECDSA signature provided by the oracle specified. The first input must correspond to the administration entity and, if a contract operator is included, the second input must correspond to the contract operator entity.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdminOracleSigBlockHeight</td>
        <td>deprecated</td>
        <td>
            The block height of the block hash used in the oracle signature.  
        </td>
    </tr>
    <tr>
        <td>ContractFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Satoshis required to be paid to the contract for each instrument action.  
        </td>
    </tr>
    <tr>
        <td>VotingSystems</td>
        <td>
            <a href="#type-voting-system">VotingSystem[tiny]</a>
        </td>
        <td>
            A list voting systems.  
        </td>
    </tr>
    <tr>
        <td>ContractPermissions</td>
        <td>
            varbin(small)
        </td>
        <td>
            A set of permission objects containing switches and field references that define the permissions for modifying this contract. See the Permission documentation for more detail.  
        </td>
    </tr>
    <tr>
        <td>RestrictedQtyInstruments</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of Instruments (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI
            Qty of Instruments - Amendments can be restricted to a vote. Example: 1
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
            <a href="#type-oracle">Oracle[tiny]</a>
        </td>
        <td>
            A list of oracles that provide approval for all token transfers for all instruments under the contract.  
        </td>
    </tr>
    <tr>
        <td>MasterAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s master key. This key has the ability to change the active contract address in case of a security failure with the active contract key.  
        </td>
    </tr>
    <tr>
        <td>ContractRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            A counter for the number of times this contract has been revised using an amendment action.
            Can&#39;t be changed by the administration, operator. Smart contract controls. Example: 0
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Can&#39;t be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
    <tr>
        <td>EntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s parent entity. This is optional for entity contracts, but required for instrument and service contracts to identify the entity parent contract.<br />            This field is required when the field ContractType equals 1.
            This field is only valid when the field ContractType equals 1.
        </td>
    </tr>
    <tr>
        <td>OperatorEntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address for the operator&#39;s entity contract.  
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            uint(1)
        </td>
        <td>
            Describes the purpose of the contract. 0 - Entity, 1 - Instrument
             Example: 0
        </td>
    </tr>
    <tr>
        <td>Services</td>
        <td>
            <a href="#type-service">Service[tiny]</a>
        </td>
        <td>
            The services provided by the contract entity.<br />            This field is only valid when the field ContractType equals 0.
        </td>
    </tr>
    <tr>
        <td>AdminIdentityCertificates</td>
        <td>
            <a href="#type-admin-identity-certificate">AdminIdentityCertificate[tiny]</a>
        </td>
        <td>
            Certificates providing proof of administrator/operator identities.  
        </td>
    </tr>
    <tr>
        <td>AdminAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s administrator. This is not contained in the contract offer payload, but determined by the inputs of the contract offer transaction and included here by the smart contract agent as a convenience.<br />  </td>
    </tr>
    <tr>
        <td>OperatorAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address of the contract&#39;s operator. This is not contained in the contract offer payload, but determined by the inputs of the contract offer transaction and included here by the smart contract agent as a convenience.&#34;
  
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            <a href="#alias-legal-system">LegalSystem</a>
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Legal System - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            <a href="#alias-polity">Polity</a>
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
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
        <td>Required so that users can monitor transactions to the contract for updates to contract/instruments.</td>
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
            <a href="#type-amendment">Amendment[tiny]</a>
        </td>
        <td>
            A collection of modifications to perform on this contract.  
        </td>
    </tr>
    <tr>
        <td>RefTxID</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
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
        <td>Administration&#39;s Public Address</td>
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
            varchar(tiny)
        </td>
        <td>
            Can be any unique identifying string, including human readable names for branding/vanity purposes. Contract identifier (instance) is the bitcoin public address. If the public address is lost, then the administration will have to reissue the entire contract, Instrument Definition and tokens with the new public address. Smart contracts can be branded and specialized to suit any terms and conditions.<br />             Example: Tesla - Shareholder Agreement
        </td>
    </tr>
    <tr>
        <td>ContractCode</td>
        <td>
            <a href="#alias-contract-code">ContractCode</a>
        </td>
        <td>
            32 randomly generated bytes. Each Contract Code should be unique. The Contract ID will be human facing and will be the Contract Code, with a checksum, encoded in base58 and prefixed by &#39;CON&#39;. Contract ID = CON &#43; base58(ContractCode &#43; checksum).  Eg. Contract ID = &#39;CON18RDoKK7Ed5zid2FkKVy7q3rULr4tgfjr4&#39;  
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
            varbin(medium)
        </td>
        <td>
            SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full terms and conditions of an agreement in the Tokenized Body of Agreement format.  This is specific to the smart contract and relevant Instruments.  Legal and technical information.  
        </td>
    </tr>
    <tr>
        <td>ContractType</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Describes the purpose of the contract.
             Example: Non-Disclosure Agreement
        </td>
    </tr>
    <tr>
        <td>SupportingDocs</td>
        <td>
            <a href="#type-document">Document[tiny]</a>
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
        <td>(Deprecated)GoverningLawDeprecated</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. 5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
             Example: USA
        </td>
    </tr>
    <tr>
        <td>(Deprecated)JurisdictionDeprecated</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. Legal proceedings/arbitration will take place using the specified Governing Law in this location.
             Example: US-CA
        </td>
    </tr>
    <tr>
        <td>EffectiveDate</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Start date of the contract.  
        </td>
    </tr>
    <tr>
        <td>ContractExpiration</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an &#39;Expired&#39; folder.  
        </td>
    </tr>
    <tr>
        <td>ContractURI</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the issuer (company), information about the Instrument, legal information, etc.  There will also be a way for token owners to vote on this page and contact details with the issuer/tokenized companies. Could be a IPv6/IPv4, or txn-id for on chain information or even a public address (DNS).
             Example: https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj
        </td>
    </tr>
    <tr>
        <td>PrevRevTxID</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            The Tx-ID of the previous contract revision.  
        </td>
    </tr>
    <tr>
        <td>Entities</td>
        <td>
            <a href="#type-entity">Entity[tiny]</a>
        </td>
        <td>
            A list of legal entities associated with this contract.  
        </td>
    </tr>
    <tr>
        <td>EntityOracle</td>
        <td>
            <a href="#type-oracle">Oracle</a>
        </td>
        <td>
            The oracle that provided the signature used to verify the entity&#39;s identity.  
        </td>
    </tr>
    <tr>
        <td>EntityOracleSignature</td>
        <td>
            varbin(tiny)
        </td>
        <td>
            The ECDSA signature provided by the oracle specified. For N entities, the first N inputs must correspond with those entities.  
        </td>
    </tr>
    <tr>
        <td>EntityOracleSigBlockHeight</td>
        <td>
            uint(4)
        </td>
        <td>
            The block height of the block hash used in the oracle signature.  
        </td>
    </tr>
    <tr>
        <td>GoverningLaw</td>
        <td>
            <a href="#alias-legal-system">LegalSystem</a>
        </td>
        <td>
            5 Letter Code to identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.
            Governing Legal System - Amendments can be restricted to a vote. Example: USA
        </td>
    </tr>
    <tr>
        <td>Jurisdiction</td>
        <td>
            <a href="#alias-polity">Polity</a>
        </td>
        <td>
            Legal proceedings/arbitration will take place using the specified Governing Law in this location.
            Jurisdiction - Amendments can be restricted to a vote. Example: US-CA
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
        <td>NewContractAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address to be used by all future requests/responses for the contract.</td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
</table>

<hr />

<a name="action-body-of-agreement-offer"></a>

#### Body Of Agreement Offer

Allows the administration to define the agreement for the contract.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C6</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Chapters</td>
        <td>
            <a href="#type-chapter">Chapter[tiny]</a>
        </td>
        <td>
            A list of chapters for the agreement.</td>
    </tr>
    <tr>
        <td>Definitions</td>
        <td>
            <a href="#type-defined-term">DefinedTerm[tiny]</a>
        </td>
        <td>
            Definition of values within the agreement.  
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
        <td>Administration&#39;s Public Address</td>
        <td></td>
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
        <td></td>
    </tr>
</table>

<hr />

<a name="action-body-of-agreement-formation"></a>

#### Body Of Agreement Formation

Provides the current version of the body of agreement for the contract.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C7</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Chapters</td>
        <td>
            <a href="#type-chapter">Chapter[tiny]</a>
        </td>
        <td>
            A list of chapters for the agreement.</td>
    </tr>
    <tr>
        <td>Definitions</td>
        <td>
            <a href="#type-defined-term">DefinedTerm[tiny]</a>
        </td>
        <td>
            Definition of terms within the agreement.  
        </td>
    </tr>
    <tr>
        <td>Revision</td>
        <td>
            uint(4)
        </td>
        <td>
            A counter for the number of times this agreement has been revised using a modification action.
            Can&#39;t be changed by the administration, operator. Smart contract controls. Example: 0
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Can&#39;t be changed by the administration, operator. Smart contract controls.
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
        <td></td>
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
        <td></td>
    </tr>
</table>

<hr />

<a name="action-body-of-agreement-amendment"></a>

#### Body Of Agreement Amendment

Allows the administration to modify the agreement for the contract.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>C8</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Revision</td>
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
            <a href="#type-amendment">Amendment[tiny]</a>
        </td>
        <td>
            A collection of modifications to perform on this instrument.  
        </td>
    </tr>
    <tr>
        <td>RefTxID</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
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
        <td>Administration&#39;s Public Address</td>
        <td></td>
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
        <td></td>
    </tr>
</table>

<hr />

<a name="action-instrument-definition"></a>

#### Instrument Definition

This action is used by the administration to define the properties/characteristics of the instrument (token) that it wants to create. An instrument has a unique identifier called InstrumentID = InstrumentType &#43; base58(InstrumentCode &#43; checksum). An instrument is always linked to a contract that is identified by the public address of the Contract wallet.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>I1</td>
    </tr>
</table>
<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>InstrumentPermissions</td>
        <td>
            varbin(small)
        </td>
        <td>
            A set of permission objects containing switches and field references that define the permissions for modifying this instrument. See the Permission documentation for more detail.
            <br />
        </td>
    </tr>
    <tr>
        <td>(Deprecated)TransfersPermitted</td>
        <td>deprecated</td>
        <td>
            Deprecated to move into specific instrument types. Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
<br />
        </td>
    </tr>
    <tr>
        <td>(Deprecated)TradeRestrictionsDeprecated</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. If specified, the instrument can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.
<br />
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
            When false holders of this instrument will not be able to vote for tokens of this instrument even on voting systems in which vote multiplers are not permitted.
             Example: true
        </td>
        <tr>
        <td>VoteMultiplier</td>
        <td>
            uint(1)
        </td>
        <td>
            Multiplies a vote by the specified integer. Where 1 token is equal to 1 vote with a 1 for vote multipler (normal), 1 token = 3 votes with a multiplier of 3, for example. If zero, then holders of this instrument don&#39;t get any votes for their tokens.
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
        <td>InstrumentModificationGovernance</td>
        <td>
            uint(1)
        </td>
        <td>
            Supported values: 1 - Contract-wide Instrument Governance. 0 - Instrument-wide Instrument Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the instrument permissions, then the vote will either be a contract-wide vote (all instruments vote on the referendum/initiative) or an instrument-wide vote (only this instrument votes on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>AuthorizedTokenQty</td>
        <td>
            uint(8)
        </td>
        <td>
            The number of tokens authorized to be issued for this instrument. Set to greater than zero for fungible tokens. If the value is 1 then it becomes a non-fungible token, where the contract would have many instruments. Set to 0 to represent a placeholder instrument, where tokens are to be issued later, or to represent a decomissioned instrument where all tokens have been revoked.
             Example: 1000000
        </td>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            <a href="#alias-instrument-type">InstrumentType</a>
        </td>
        <td>
            A code representing the type of instrument and the structure of the payload.
             This field is always required.
        </td>
    </tr>
    <tr>
        <td>InstrumentPayload</td>
        <td>
            varbin(small)
        </td>
        <td>
            A custom payload that contains meta data about this instrument. Payload structure and length is dependent on the instrument type chosen. See instrument documentation for more details.
             This field is always required.
        </td>
    </tr>
    <tr>
        <td>TradeRestrictions</td>
        <td>
            <a href="#alias-varchar">Polity[small]</a>
        </td>
        <td>
            If specified, the instrument can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.  
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
        <td>Administration&#39;s Public Address</td>
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
        <td>The contract that this instrument should be assigned to. Must include enough for the responding action.</td>
    </tr>
</table>

<hr />

<a name="action-instrument-creation"></a>

#### Instrument Creation

This action creates an instrument in response to the administration&#39;s instructions in the Definition Action.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>I2</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>InstrumentIndex</td>
        <td>
            uint(8)
        </td>
        <td>
            The index of the instrument within the contract. First instrument is zero, second is one. Used to derive the instrument code.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>InstrumentPermissions</td>
        <td>
            varbin(small)
        </td>
        <td>
            A set of permission objects containing switches and field references that define the permissions for modifying this instrument. See the Permission documentation for more detail.<br />
        </td>
    </tr>
    <tr>
        <td>(Deprecated)TransfersPermitted</td>
        <td>deprecated</td>
        <td>
            Deprecated to move into specific instrument types. Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.<br />        </td>
    </tr>
    <tr>
        <td>(Deprecated)TradeRestrictionsDeprecated</td>
        <td>deprecated</td>
        <td>
            Deprecated to remove fixed size. If specified, the instrument can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.<br />
        </td>
    </tr>
    <tr>
        <td>EnforcementOrdersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if the administration is permitted to make enforcement orders on user tokens and balances, otherwise set to false to disable this feature.
             Example: true
        </td>
    </tr>
    <tr>
        <td>VotingRights</td>
        <td>
            bool
        </td>
        <td>
            When false holders of this instrument will not be able to vote for tokens of this instrument even on voting systems in which vote multiplers are not permitted.
             Example: true
        </td>
    </tr>
    <tr>
        <td>VoteMultiplier</td>
        <td>
            uint(1)
        </td>
        <td>
            Multiplies a vote by the specified integer. Where 1 token is equal to 1 vote with a 1 for vote multipler (normal), 1 token = 3 votes with a multiplier of 3, for example. If zero, then holders of this instrument don&#39;t get any votes for their tokens.
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
        <td>InstrumentModificationGovernance</td>
        <td>
            uint(1)
        </td>
        <td>
            Supported values: 1 - Contract-wide Instrument Governance.  0 - Instrument-wide Instrument Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the instrument permissions, then the vote will either be a contract-wide vote (all instruments vote on the referendum/initiative) or an instrument-wide vote (only this instrument votes on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>AuthorizedTokenQty</td>
        <td>
            uint(8)
        </td>
        <td>
            The number of tokens authorized to be issued for this instrument. Set to greater than zero for fungible tokens. If the value is 1 then it becomes a non-fungible token, where the contract would have many instruments. Set to 0 to represent a placeholder instrument, where tokens are to be issued later, or to represent a decomissioned instrument where all tokens have been revoked.
             Example: 1000000
        </td>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            <a href="#alias-instrument-type">InstrumentType</a>
        </td>
        <td>
            A code representing the type of instrument and the structure of the payload.<br />
        </td>
    </tr>
    <tr>
        <td>InstrumentPayload</td>
        <td>
            varbin(small)
        </td>
        <td>
            A custom payload that contains meta data about this instrument. Payload structure and length is dependent on the instrument type chosen. See instrument documentation for more details.<br />
        </td>
    </tr>
    <tr>
        <td>InstrumentRevision</td>
        <td>
            uint(4)
        </td>
        <td>
            A counter for the number of times this instrument has been revised using a modification action.
            Can&#39;t be changed by the administration, operator. Smart contract controls. Example: 456789
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Timestamp in nanoseconds of when the smart contract created the action.
            Can&#39;t be changed by the administration, operator. Smart contract controls.
        </td>
    </tr>
    <tr>
        <td>TradeRestrictions</td>
        <td>
            <a href="#alias-varchar">Polity[small]</a>
        </td>
        <td>
            If specified, the instrument can only be traded within the specified trade restriction zone. For example, AUS would restrict to Australian residents only.<br />
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
        <td>The contract that this instrument was assigned to.</td>
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
        <td>Required so that users can monitor transactions to the contract for updates to contract/instruments.</td>
    </tr>
</table>

<hr />

<a name="action-instrument-modification"></a>

#### Instrument Modification

Token Dilutions, Call Backs/Revocations, burning etc.

<table>
    <tr>
        <th style="width:15%">Action Code</th>
        <td>I3</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>InstrumentRevision</td>
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
            <a href="#type-amendment">Amendment[tiny]</a>
        </td>
        <td>
            A collection of modifications to perform on this instrument.<br />
        </td>
    </tr>
    <tr>
        <td>RefTxID</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            The Bitcoin transaction ID of the associated result action that permitted the modifications. See Governance for more details.<br />
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
        <td>Administration&#39;s Public Address</td>
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
        <td>The contract that this instrument currently belongs to. Must include enough for the responding action.</td>
    </tr>
</table>

<hr />

<a name="action-transfer"></a>

#### Transfer

A Token Owner(s) Sends, Exchanges or Swaps a token(s) or Bitcoin for a token(s) or Bitcoin. Can be as simple as sending a single token to a receiver. Or can be as complex as many senders sending many different instruments - controlled by many different smart contracts - to a number of receivers. This action also supports atomic swaps (tokens for tokens). Since many parties and contracts can be involved in a transfer and the corresponding settlement action, the partially signed T1 and T2 actions will need to be passed around on-chain with an M1 action, or off-chain.

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
        <td>Instruments</td>
        <td>
            <a href="#type-instrument-transfer">InstrumentTransfer[tiny]</a>
        </td>
        <td>
            The Instruments involved in the Transfer Action.<br />
        </td>
    </tr>
    <tr>
        <td>OfferExpiry</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            This prevents any party from holding on to the partially signed message as a form of an option.  Eg. the exchange at this price is valid for 30 mins.<br />
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
            <a href="#alias-address">Address</a>
        </td>
        <td>
            Identifies the public address that the exchange fee should be paid to.
<br />
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
        <td>Instrument Senders</td>
        <td>Instrument (token) Sending Public Address. Instruments[i].InstrumentSenders[j].Index references these inputs.</td>
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
        <td>Contract Public Address for Instrument X</td>
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
        <td>Instruments</td>
        <td>
            <a href="#type-instrument-settlement">InstrumentSettlement[tiny]</a>
        </td>
        <td>
            The Instruments settled by the transfer action.
            <br />
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>Contract Public Address (Instrument X)</td>
        <td>Contract (Instrument X) in response to a transfer action with Instrument X being sent to another address(es).</td>
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
        <td>Instrument 1 Settlement Address X</td>
        <td>Address X that is being settled for Instrument 1.</td>
    </tr>
</table>

<hr />

<a name="action-proposal"></a>

#### Proposal

Allows the Administration/Token Holders to propose a change (aka Initiative/Shareholder vote). A significant cost - specified in the Contract Formation - can be attached to this action when sent from Token Holders to reduce spam, as the resulting vote will be put to all token owners.

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
        <td>Type</td>
        <td>
            uint(1)
        </td>
        <td>
            Type of proposal. Supported values:
  0 Referendum / Administration Initiates / Members Vote
  1 Initiative / Members Initiate / Members Vote
  2 AdministrativeMatter / Administration Initiates / Administrators Vote
<br />
        </td>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
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
        <td>ProposedAmendments</td>
        <td>
            <a href="#type-amendment">Amendment[tiny]</a>
        </td>
        <td>
            Each element contains details of which fields to modify, or delete. Because the number of fields in a Contract and Instrument is dynamic due to some fields being able to be repeated, the index value of the field needs to be calculated against the Contract or Instrument the changes are to apply to. In the event of a Vote being created from this Initiative, the changes will be applied to the version of the Contract or Instrument at that time.
        </td>
    </tr>
    <tr>
        <td>VoteOptions</td>
        <td>
            varchar(tiny)
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
            varchar(medium)
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
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>Operator / Token Owner&#39;s Public Address</td>
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
            <a href="#alias-timestamp">Timestamp</a>
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

Used by Token Owners to cast their ballot (vote) on proposals. 1 Vote per token unless a vote multiplier is specified in the relevant Instrument Definition action.

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
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            Tx ID of the Vote the Ballot Cast is being made for.
        </td>
    </tr>
    <tr>
        <td>Vote</td>
        <td>
            varchar(tiny)
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
        <td>Token Owner&#39;s Public Address</td>
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
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            Tx ID of the Vote the Ballot Cast is being made for.
        </td>
    </tr>
    <tr>
        <td>Vote</td>
        <td>
            varchar(tiny)
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
            <a href="#alias-timestamp">Timestamp</a>
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

Once a vote has been completed the results are published. After the result is posted, it is up to the administration to send a contract/instrument amendement if appropriate.

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
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>ProposedAmendments</td>
        <td>
            <a href="#type-amendment">Amendment[tiny]</a>
        </td>
        <td>
            Each element contains details of which fields to modify, or delete. Because the number of fields in a Contract and Instrument is dynamic due to some fields being able to be repeated, the index value of the field needs to be calculated against the Contract or Instrument the changes are to apply to. In the event of a Vote being created from this Initiative, the changes will be applied to the version of the Contract or Instrument at that time.  
        </td>
    </tr>
    <tr>
        <td>VoteTxId</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            Link to the Vote Action txn.  
        </td>
    </tr>
    <tr>
        <td>OptionTally</td>
        <td>
            uint(8)[tiny]
        </td>
        <td>
            List of number of valid votes counted for each vote option. Length is encoded like a regular list object, but must match the length of VoteOptions from the Proposal action.  
        </td>
    </tr>
    <tr>
        <td>Result</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw for 1st place, all winning options are listed.  
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>TargetAddresses</td>
        <td>
            <a href="#type-target-address">TargetAddress[medium]</a>
        </td>
        <td>
            The holders and quantities that are effected by the order. For a contract or instrument wide freeze only the contract address is specified. Zero quantities are invalid unless it is for the contract address in an instrument wide or contract wide freeze. In a thaw order this field is not serialized, because the entire freeze from the FreezeTxId freeze action will be thawed.  
        </td>
    </tr>
    <tr>
        <td>FreezeTxId</td>
        <td>
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            The tx id of the freeze action that is being thawed. Only serialized for thaw orders.  
        </td>
    </tr>
    <tr>
        <td>FreezePeriod</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Used for a &#39;time out&#39;.  Tokens are automatically unfrozen after the expiration timestamp without requiring a Thaw Action. Null value for Thaw, Confiscation and Reconciallitaion orders.
             Example: Tue Oct 09 2018 05:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>DepositAddress</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The public address for confiscated tokens to be deposited in.  Null for Freeze, Thaw, actions.
            Eventually the supporting evidence/explanation can be supported by a Subfield that has the public address (and a signed message) owned by a legal authority for ID verification/certification purposes.
        </td>
    </tr>
    <tr>
        <td>AuthorityName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. Enforcement Authority Name (eg. Issuer, Queensland Police Service, Tokenized, etc.)
             Example: Supreme and District Courts Brisbane
        </td>
    </tr>
    <tr>
        <td>AuthorityPublicKey</td>
        <td>
            varbin(tiny)
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
            Algorithm used for order signature. Only valid value is currently 1 = ECDSA&#43;secp256k1
             Example: 1
        </td>
    </tr>
    <tr>
        <td>OrderSignature</td>
        <td>
            varbin(tiny)
        </td>
        <td>
            Length 0-255 bytes. Signature for a message that lists out the target addresses and deposit address. Signature of (Contract PKH, Compliance Action, Authority Name, Instrument Code, Supporting Evidence Hash, FreezePeriod, TargetAddresses, and DepositAddress)  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)SupportingEvidenceHash</td>
        <td>deprecated</td>
        <td>
            Deprecated for new supporting evidence type and data fields (bin 32). SHA-256: warrant, court order, etc.  
        </td>
    </tr>
    <tr>
        <td>(Deprecated)RefTxs</td>
        <td>deprecated</td>
        <td>
            Deprecated for a new data format for reference transactions (varbin medium). The request/response actions that were dropped.  The entire txn for both actions is included as evidence that the actions were accepted into the mempool at one point and that the senders (token/Bitcoin) signed their intent to transfer.  The management of this record keeping is off-chain and managed by the administration or operator to preserve the integrity of the state of the tokens. Only applicable for reconcilliation actions.  No subfield when F, T, R is selected as the Compliance Action subfield.
            Can be null.  Dropped actions that require a reconciliation action to fix the break in the chain are considered to be an extremely rare event.
        </td>
    </tr>
    <tr>
        <td>BitcoinDispersions</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[small]</a>
        </td>
        <td>
            Index of address in TargetAddresses and amount of bitcoin (in satoshis) they are receiving in exchange for their tokens.  
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(medium)
        </td>
        <td>
            A message to include with the enforcement order.
             Example: Compelled by a court order.
        </td>
    </tr>
    <tr>
        <td>SupportingEvidenceFormat</td>
        <td>
            uint(1)
        </td>
        <td>
            The data format of the supporting evidence field. 0 = no evidence data provided, 1 = markdown containing warrant, court order, etc.  
        </td>
    </tr>
    <tr>
        <td>SupportingEvidence</td>
        <td>
            varbin(tiny)
        </td>
        <td>
            Supporting evidence related to the order being requested.  
        </td>
    </tr>
    <tr>
        <td>ReferenceTransactions</td>
        <td>
            <a href="#type-reference-transaction">ReferenceTransaction[medium]</a>
        </td>
        <td>
            The request/response actions that were dropped.  The entire txn for both actions is included as evidence that the actions were accepted into the mempool at one point and that the senders (token/Bitcoin) signed their intent to transfer.  The management of this record keeping is off-chain and managed by the administration or operator to preserve the integrity of the state of the tokens. Only applicable for reconcilliation actions.  No subfield when F, T, R is selected as the Compliance Action subfield.
            Can be null.  Dropped actions that require a reconciliation action to fix the break in the chain are considered to be an extremely rare event.
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
        <td>Administration&#39;s Public Address</td>
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

The contract responding to an Order action to freeze instruments. To be used to comply with contractual/legal/issuer requirements. The target public address(es) will be marked as frozen. However the Freeze action publishes this fact to the public blockchain for transparency. The contract will not respond to any actions requested by the frozen address.

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
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[small]</a>
        </td>
        <td>
            Indices to addresses in outputs and the quantities being frozen. If the only address is the contract address and the instrument code is zeros, then it is a contract wide freeze. If the only address is the contract address and the instrument code is specified, then it is an instrument wide freeze.  
        </td>
    </tr>
    <tr>
        <td>FreezePeriod</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Used for a &#39;time out&#39;.  Tokens are automatically unfrozen after the expiration timestamp without requiring a Thaw Action.  
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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

The contract responding to an Order action to thaw instruments. To be used to comply with contractual obligations or legal requirements. The Alleged Offender&#39;s tokens will be unfrozen to allow them to resume normal exchange and governance activities.

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
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            The tx id of the freeze action that is being reversed.
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>Can be the Contract Address for a &#39;Contract-wide&#39; Thaw in response to a Contract-wide Freeze.</td>
    </tr>
</table>

<hr />

<a name="action-confiscation"></a>

#### Confiscation

The contract responding to an Order action to confiscate instruments. To be used to comply with contractual obligations, legal and/or issuer requirements.

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
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[small]</a>
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
            Deposit address&#39;s token balance after confiscation.
             Example: 10000
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>Can be the Contract Address for a &#39;Contract-wide&#39; Confiscation.</td>
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

The contract responding to an Order action to reconcile instruments. To be used at the direction of the administration to fix record keeping errors with bitcoin and token balances.

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
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type.
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Quantities</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[small]</a>
        </td>
        <td>
            The holders effected by the reconciliation and their balance remaining.  
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
            varchar(medium)
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
            varchar(medium)
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
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            Transaction ID of the register entry to be altered.
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(medium)
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
            <a href="#alias-tx-id">TxId</a>
        </td>
        <td>
            Transaction ID of the register entry to be altered.</td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(medium)
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

<a name="action-message"></a>

#### Message

The message action is a general purpose communication action. &#39;Twitter/SMS&#39; for Issuers/Investors/Users. The message txn can also be used for passing partially signed txns on-chain, establishing private communication channels and EDI (receipting, invoices, PO, and private offers/bids). The messages are broken down by type for easy filtering in the a user&#39;s wallet. The Message Types are listed in the Message Types table.

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
        <td>SenderIndexes</td>
        <td>
            uint(4)[tiny]
        </td>
        <td>
            Associates the message to a particular input by the index. If none are specified then the first input is assumed.</td>
    </tr>
    <tr>
        <td>ReceiverIndexes</td>
        <td>
            uint(4)[tiny]
        </td>
        <td>
            Associates the message to a particular output by the index. If none are specified then the first output is assumed.  
        </td>
    </tr>
    <tr>
        <td>MessageCode</td>
        <td>
            uint(2)
        </td>
        <td>
  
        </td>
    </tr>
    <tr>
        <td>MessagePayload</td>
        <td>
            varbin(medium)
        </td>
        <td>
            Public or private (RSA public key, Diffie-Hellman). Issuers/Contracts can send the signifying amount of satoshis to themselves for public announcements or private &#39;notes&#39; if encrypted. See Message Types for a full list of potential use cases.
<br />
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
        <td>Receiver Public Address&#34;</td>
        <td>The recipient&#39;s address for the message, supplied by the sender.</td>
    </tr>
</table>

<hr />

<a name="action-rejection"></a>

#### Rejection

Used to reject request actions that do not comply with the Contract. If money is to be returned to a User then it is used in lieu of the Settlement Action to properly account for token balances. All Administration/User request Actions must be responded to by the Contract with an Action. The only exception to this rule is when there is not enough fees in the first Action for the Contract response action to remain revenue neutral. If not enough fees are attached to pay for the Contract response then the Contract will not respond.

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
            uint(4)[tiny]
        </td>
        <td>
            Associates the message to a particular output by the index. If none are specified then the first output is assumed.</td>
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
            <a href="#alias-rejection-code">RejectionCode</a>
        </td>
        <td>
            Classifies the rejection by a type.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>Message</td>
        <td>
            varchar(small)
        </td>
        <td>
            Length 0-65,535 bytes. Message that explains the reasoning for a rejection, if needed.  Most rejection types will be captured by the Rejection Type Subfield.
             Example: Sorry, you don&#39;t have enough tokens.
        </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
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
        <td>The affected user or contract&#39;s publid addresses. Refunds all money provided in the request action, less fees</td>
    </tr>
</table>

<hr />

<a name="field-types"></a>

## Field Types

<div class="content-list collection-method-list" markdown="1">
- [Administrator](#type-administrator)
- [Administrator Identity Certificate](#type-admin-identity-certificate)
- [Amendment](#type-amendment)
- [InstrumentReceiver](#type-instrument-receiver)
- [Instrument Settlement](#type-instrument-settlement)
- [Instrument Transfer](#type-instrument-transfer)
- [Chapter](#type-chapter)
- [Clause](#type-clause)
- [Defined Term](#type-defined-term)
- [Document](#type-document)
- [Entity](#type-entity)
- [Manager](#type-manager)
- [Oracle](#type-oracle)
- [Quantity Index](#type-quantity-index)
- [Reference Transaction](#type-reference-transaction)
- [Service](#type-service)
- [Target Address](#type-target-address)
- [Voting System](#type-voting-system)
</div>

<a name="type-administrator"></a>

### Administrator

Administrator is used to refer to a Administration role in an Entity.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            <a href="#alias-role">Role</a>
        </td>
        <td>
            Chairman, Director, Managing Partner, etc.. Found in &#39;Roles&#39; in Specification/Resources
             Example: 7
        </td>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid.
             Example: Satoshi Nakamoto
        </td>
    </tr>
</table>

<a name="type-admin-identity-certificate"></a>

### Administrator Identity Certificate

A certificate provided by an identity oracle to verify the administrator address is associated with the issuer entity identification information. Also if a contract operator is provided then it verifies that the contract operator address is associated with the specified contract operator identity information. For a child contract that references a parent entity contract the certificate verifies that the administrator address is associated with that entity contract.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>EntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The entity contract address of the service on chain that defines the identity oracle.
        </td>
    </tr>
    <tr>
        <td>Signature</td>
        <td>
            <a href="#alias-signature">Signature</a>
        </td>
        <td>
            The signature provided by the oracle specified. The first input must correspond to the  administration entity and, if a contract operator is included, the second input must  correspond to the contract operator entity.&#34;<br />  </td>
    </tr>
    <tr>
        <td>BlockHeight</td>
        <td>
            uint(4)
        </td>
        <td>
            The block height of the block hash used in the oracle signature.  
        </td>
    </tr>
    <tr>
        <td>Expiration</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            Oracles have the option to specify an expiration after which a new certificate should be  provided.  
        </td>
    </tr>
</table>

<a name="type-amendment"></a>

### Amendment

An Amendment is used to describe the modification of a single field in a Contract or Instrument, as defined in the ContractFormation and InstrumentCreation messages.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>FieldIndexPath</td>
        <td>
            varbin(tiny)
        </td>
        <td>
            List of indices that identify the field/sub-field to be amended.
            The index path of the field being modified. Encoded as a list of base 128 var ints. Each index is an index into the current object, top level being the ContractFormation or InstrumentCreation. Indexes are defined by protobuf messages. If the current level is a list, then the index is a zero based offset to the element in the list.
        </td>
    </tr>
    <tr>
        <td>Operation</td>
        <td>
            uint(1)
        </td>
        <td>
            0 = Modify. 1 = Add an element to the data to the array of elements. 2 = Delete the element listed in the Element field. The Add and Delete operations only apply to a particilar element of a complex array type. For example, it could be used to remove a particular VotingSystem from a Contract.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>Data</td>
        <td>
            varbin(medium)
        </td>
        <td>
            New data for the amended subfield. Data type depends on the the type of the field being amended. The value should be serialize as defined by the protocol.
            The bytes must be encoded in the format of the field being modified.
        </td>
    </tr>
</table>

<a name="type-instrument-receiver"></a>

### InstrumentReceiver

An InstrumentReceiver is a quantity, address, and oracle signature. The quantity could be used to describe a number of tokens, or a value. The address is where the instrument will be sent.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Address</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The address receiving the tokens</td>
    </tr>
    <tr>
        <td>Quantity</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of tokens to be received by address at Output X
             Example: 100
        </td>
    </tr>
    <tr>
        <td>OracleSigAlgorithm</td>
        <td>
            uint(1)
        </td>
        <td>
            0 = No Oracle-signed Message (OracleConfirmationSig skipped in serialization), 1 = ECDSA&#43;secp256k1. If the contract for the instrument being received has oracles, then a signature is required from one of them.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>OracleIndex</td>
        <td>
            uint(1)
        </td>
        <td>
            Specifies the index into the list of oracles in the contract offer that was used to authorize this transfer.  
        </td>
    </tr>
    <tr>
        <td>OracleConfirmationSig</td>
        <td>
            <a href="#alias-signature">Signature</a>
        </td>
        <td>
            Length 0-255 bytes. If restricted to a oracle (whitelist) or has transfer restrictions (age, location, investor status): ECDSA&#43;secp256k1 (or the like) signed message provided by an approved/trusted oracle through an API signature of the defined message. If no transfer restrictions(trade restriction/age restriction fields in the Instrument Type payload. or restricted to a whitelist by the Contract Auth Flags, it is a NULL field.  
        </td>
    </tr>
    <tr>
        <td>OracleSigBlockHeight</td>
        <td>
            uint(4)
        </td>
        <td>
            The block height of the block hash used in the oracle signature.  
        </td>
    </tr>
    <tr>
        <td>OracleSigExpiry</td>
        <td>
            <a href="#alias-timestamp">Timestamp</a>
        </td>
        <td>
            This specifies the time at which the Oracle signature expires.  
        </td>
    </tr>
</table>

<a name="type-instrument-settlement"></a>

### Instrument Settlement

InstrumentSettlement is the data required to settle an instrument transfer.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ContractIndex</td>
        <td>
            uint(2)
        </td>
        <td>
            Index of input containing the contract&#39;s address for this offset
        </td>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type. Example: COU
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Settlements</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[tiny]</a>
        </td>
        <td>
            Each element contains the resulting token balance of Instrument X for the output Address, which is referred to by the index.  
        </td>
    </tr>
</table>

<a name="type-instrument-transfer"></a>

### Instrument Transfer

InstrumentTransfer is the data required to transfer an instrument.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>ContractIndex</td>
        <td>
            uint(2)
        </td>
        <td>
            Index of output containing the contract&#39;s address for this offset
        </td>
    </tr>
    <tr>
        <td>InstrumentType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the instrument type. Example: COU
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>InstrumentCode</td>
        <td>
            <a href="#alias-instrument-code">InstrumentCode</a>
        </td>
        <td>
            A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)
            Cannot be changed by the administration, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>InstrumentSenders</td>
        <td>
            <a href="#type-quantity-index">QuantityIndex[tiny]</a>
        </td>
        <td>
            Each element has the value of tokens to be spent from the input address, which is referred to by the index.  
        </td>
    </tr>
    <tr>
        <td>InstrumentReceivers</td>
        <td>
            <a href="#type-instrument-receiver">InstrumentReceiver[tiny]</a>
        </td>
        <td>
            Each element has the value of tokens to be received, the address, and an oracle signature if required.  
        </td>
    </tr>
</table>

<a name="type-chapter"></a>

### Chapter

A chapter is the top level structure of an agreement. It contains articles.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Title</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            The title of the chapter.
        </td>
    </tr>
    <tr>
        <td>Preamble</td>
        <td>
            varchar(small)
        </td>
        <td>
            The introduction to the chapter.  
        </td>
    </tr>
    <tr>
        <td>Articles</td>
        <td>
            <a href="#type-clause">Clause[tiny]</a>
        </td>
        <td>
            A list of articles for the chapter.  
        </td>
    </tr>
</table>

<a name="type-clause"></a>

### Clause

A clause is the standard piece of an agreement, contained in each of the sub-levels of the agreement. Articles, Sections, Subsections, Paragraphs, and Subparagraphs.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Title</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            The title of the clause.</td>
    </tr>
    <tr>
        <td>Body</td>
        <td>
            varchar(small)
        </td>
        <td>
            The body of the clause.  
        </td>
    </tr>
    <tr>
        <td>Children</td>
        <td>
            <a href="#type-clause">Clause[tiny]</a>
        </td>
        <td>
            A list of clauses under this clause.  
        </td>
    </tr>
</table>

<a name="type-defined-term"></a>

### Defined Term

A definition define a term specified throughout an agreement.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Term</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            The name of the term being defined. Linked to from within the agreement with curly braces {}  around the name.  
        </td>
    </tr>
    <tr>
        <td>Definition</td>
        <td>
            varchar(small)
        </td>
        <td>
            The definition of the name.  
        </td>
    </tr>
</table>

<a name="type-document"></a>

### Document

A file containing data.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Full name, including file extension, of the file. Length 0-255 bytes. 0 is valid.
             Example: Agreement.pdf
        </td>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            MIME type of the file. Length 0-255 bytes. 0 is valid.
             Example: application/pdf
        </td>
    </tr>
    <tr>
        <td>Contents</td>
        <td>
            varbin(medium)
        </td>
        <td>
            The contents of the file.  
        </td>
    </tr>
</table>

<a name="type-entity"></a>

### Entity

Entity represents the details of a legal Entity, such as a public or private company, government agency, or and individual.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 1-255 bytes (0 is not valid). Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. 
             Example: Tesla Inc.
        </td>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            <a href="#alias-entity-type">EntityType</a>
        </td>
        <td>
            The type of entity. (i.e Public Company, Individual) (Specification/Resources).
             Example: P
        </td>
    </tr>
    <tr>
        <td>LEI</td>
        <td>
            fixedchar(20)
        </td>
        <td>
            Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up of a 20-character identifier that identifies distinct legal entities that engage in financial transactions. It is defined by ISO 17442.[1] Natural persons are not required to have an LEI; they’re eligible to have one issued, however, but only if they act in an independent business capacity.[2] The LEI is a global standard, designed to be non-proprietary data that is freely accessible to all.[3] As of December 2018, over 1,300,000 legal entities from more than 200 countries have now been issued with LEIs.
            ISO 17442 - https://en.wikipedia.org/wiki/Legal_Entity_Identifier Example: 54930084UKLVMY22DS16
        </td>
    </tr>
    <tr>
        <td>UnitNumber</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Issuer/Entity/Contracting Party X Address Details (eg. HQ)
             Example: 2
        </td>
    </tr>
    <tr>
        <td>BuildingNumber</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: 13577
        </td>
    </tr>
    <tr>
        <td>Street</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Fairmont Ave
        </td>
    </tr>
    <tr>
        <td>SuburbCity</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Robinoh
        </td>
    </tr>
    <tr>
        <td>TerritoryStateProvinceCode</td>
        <td>
            fixedchar(5)
        </td>
        <td>
             Example: BC
        </td>
    </tr>
    <tr>
        <td>CountryCode</td>
        <td>
            fixedchar(3)
        </td>
        <td>
             Example: USA
        </td>
    </tr>
    <tr>
        <td>PostalZIPCode</td>
        <td>
            fixedchar(12)
        </td>
        <td>
             Example: 50210
        </td>
    </tr>
    <tr>
        <td>EmailAddress</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. Address for text-based communication: eg. email address, Bitcoin address
             Example: satoshi@tokenized.com
        </td>
    </tr>
    <tr>
        <td>PhoneNumber</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid. Phone Number for Entity.
             Example: 0448484848
        </td>
    </tr>
    <tr>
        <td>Administration</td>
        <td>
            <a href="#type-administrator">Administrator[tiny]</a>
        </td>
        <td>
            A list of people that are in Administrative Roles for the Entity.  eg. Chair, Director, Managing Partner, etc.
  
        </td>
    </tr>
    <tr>
        <td>Management</td>
        <td>
            <a href="#type-manager">Manager[tiny]</a>
        </td>
        <td>
            A list of people in Management Roles for the Entity. e.g CEO, COO, CTO, CFO, Secretary, Executive, etc.  
        </td>
    </tr>
    <tr>
        <td>DomainName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Domain name owned by this entity. Length 0-255 bytes. 0 is valid.
             Example: tokenized.com
        </td>
    </tr>
    <tr>
        <td>(Deprecated)EntityContractAddress</td>
        <td>deprecated</td>
        <td>
            Deprecated for separate field in contract. Address of entity contract. When the contract type is instrument contract, or a child type, this field refers to the entity specified in the contract at the address specified. When this field is present, no other fields should be included in the entity.  
        </td>
    </tr>
    <tr>
        <td>PaymailHandle</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. Handle containing an alias and domain name performing queries defined in the Paymail protocol.
             Example: satoshi@tokenized.id
        </td>
    </tr>
</table>

<a name="type-manager"></a>

### Manager

Manager is used to refer to a role that is responsible for the Management of an Entity.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            <a href="#alias-role">Role</a>
        </td>
        <td>
            CEO, COO, CFO, etc. Found in &#39;Roles&#39; in Specification/Resources
             Example: 5
        </td>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid.
             Example: Satoshi Nakamoto
        </td>
    </tr>
</table>

<a name="type-oracle"></a>

### Oracle

A Oracle defines the details of a public Oracle.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>(Deprecated)Entity</td>
        <td>deprecated</td>
        <td>
            Deprecated for service contract address. Identifying information about the oracle.</td>
    </tr>
    <tr>
        <td>(Deprecated)URL</td>
        <td>deprecated</td>
        <td>
            Deprecated for service contract address. Length 0-255 bytes. 0 is valid. If applicable: URL for REST/RPC Endpoint
             Example: http://oracle.tokenized.com/api/3650d9/version2010
        </td>
    </tr>
    <tr>
        <td>(Deprecated)PublicKey</td>
        <td>deprecated</td>
        <td>
            Deprecated for service contract address. Length 0-255 bytes. 0 is not valid. Oracle Public Key (eg. Bitcoin Public key), used to confirm digital signed proofs for transfers.  Can also be the same public address that controls a Tokenized Oracle.  
        </td>
    </tr>
    <tr>
        <td>OracleTypes</td>
        <td>
            uint(1)[tiny]
        </td>
        <td>
            The type of the oracle. 0 = Identity, 1 = Authority, 2 = Event. More than one value can be included to specify the oracle has more than one type.  
        </td>
    </tr>
    <tr>
        <td>EntityContract</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            The entity contract address of the service on chain that defines the oracle.  
        </td>
    </tr>
</table>

<a name="type-quantity-index"></a>

### Quantity Index

A QuantityIndex contains a quantity, and an index. The quantity could be used to describe a number of tokens, or a value. The index is used to refer to an input or output index position.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Index</td>
        <td>
            uint(2)
        </td>
        <td>
            The index of the input/output (depending on context) sending/receiving the tokens.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>Quantity</td>
        <td>
            uint(8)
        </td>
        <td>
            Number of tokens being sent
             Example: 100
        </td>
    </tr>
</table>

<a name="type-reference-transaction"></a>

### Reference Transaction

A bitcoin transaction and the outputs that it spends.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Transaction</td>
        <td>
            varbin(tiny)
        </td>
        <td>
            A bitcoin transaction serialized in the bitcoin P2P format.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>Outputs</td>
        <td>
            varbin(large)[medium]
        </td>
        <td>
            The bitcoin outputs corresponding to the inputs for the transaction. Serialized in bitcoin P2P format. There must be the same count as there are inputs in the contained transaction and they must be in the same order.  
        </td>
    </tr>
</table>

<a name="type-service"></a>

### Service

A definition of a service provided by an identity oracle to verify the administrator address is associated with the issuer entity identification information. Also if a contract operator is provided then it verifies that the contract operator address is associated with the specified contract operator identity information. For a child contract that references a parent entity contract the certificate verifies that the administrator address is associated with that entity contract.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            uint(1)
        </td>
        <td>
            Describes the type of service.
  0 - Identity Oracle
  1 - Authority Oracle
  2 - Event Oracle
  3 - Contract Operator
<br />
             Example: 0
        </td>
    </tr>
    <tr>
        <td>URL</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            The base URL of the service. For each service type there are predefined methods for  determining the specific endpoints.  
        </td>
    </tr>
    <tr>
        <td>PublicKey</td>
        <td>
            <a href="#alias-public-key">PublicKey</a>
        </td>
        <td>
            The public key used to verify and authorize the service.  
        </td>
    </tr>
</table>

<a name="type-target-address"></a>

### Target Address

A TargetAddress defines a public address and quantity.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Address</td>
        <td>
            <a href="#alias-address">Address</a>
        </td>
        <td>
            Public address where the token balance will be changed.</td>
    </tr>
    <tr>
        <td>Quantity</td>
        <td>
            uint(8)
        </td>
        <td>
            Qty of tokens to be frozen, thawed, confiscated or reconciled. For Contract-wide freezes 0 will be used.
             Example: 10000
        </td>
    </tr>
</table>

<a name="type-voting-system"></a>

### Voting System

A VotingSystem defines all details of a Voting System.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            eg. Special Resolutions, Ordinary Resolutions, Fundamental Matters, General Matters, Directors&#39; Vote, Poll, etc.
             Example: Special Resolutions
        </td>
    </tr>
    <tr>
        <td>VoteType</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            R - Relative Threshold, A - Absolute Threshold, P - Plurality.  Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast.  Abstentations/spoiled votes do not detract from the likelihood of a vote passing as they are not included in the denominator.  Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens.  Abstentations/spoiled votes detract from the likelihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the vote cannot pass.  50% of all tokens would have had to vote for one vote option for the vote to be successful. Plurality means the most favoured option is selected, regardless of the number of votes cast or the percentage relative to other choices.
             Example: A
        </td>
    </tr>
    <tr>
        <td>TallyLogic</td>
        <td>
            uint(1)
        </td>
        <td>
            0 - Standard Scoring (&#43;1 * # of tokens owned), 1 - Weighted Scoring (1st choice * Vote Max * # of tokens held, 2nd choice * Vote Max-1 * # of tokens held,..etc.)
             Example: 0
        </td>
    </tr>
    <tr>
        <td>ThresholdPercentage</td>
        <td>
            uint(1)
        </td>
        <td>
            This field is ignored when VoteType is P (Plurality). Otherwise it is the percentage of ballots required for a proposal to pass. Valid values are greater than 0 and less than 100. 75 means 75% and greater.  Only applicable to Relative and Absolute Threshold vote methods.  The Plurality vote method requires no threshold value (NULL), as the successful vote option is simply selected on the basis of highest ballots cast for it.
             Example: 75
        </td>
    </tr>
    <tr>
        <td>VoteMultiplierPermitted</td>
        <td>
            bool
        </td>
        <td>
            Where an instrument has a vote multiplier, true must be set here for the vote multiplier to count, otherwise votes are simply treated as 1x per token.  
        </td>
    </tr>
    <tr>
        <td>HolderProposalFee</td>
        <td>
            uint(8)
        </td>
        <td>
            Token Owners must pay the fee amount to broadcast a valid Proposal.  If the Proposal action is valid, the smart contract will start a vote. 0 is valid.
             Example: 100
        </td>
    </tr>
</table>

<a name="field-aliases"></a>

## Field Aliases

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr id="alias-role">
            <td>Role</td>
            <td>
                uint(1)
            </td>
            <td>
                A role within an entity. (i.e. CEO, CFO)
                 Example: 5
            </td>
        </tr>
        <tr id="alias-entity-type">
            <td>EntityType</td>
            <td>
                fixedchar(1)
            </td>
            <td>
                A type of entity. (i.e. Individual, Public Company)
                 Example: I
            </td>
        </tr>
        <tr id="alias-polity">
            <td>Polity</td>
            <td>
                varchar(tiny)
            </td>
            <td>
                Polities (eg. Countries/Nation-States (ISO-3166 Alpha-3)
                 Example: GBR
            </td>
        </tr>
        <tr id="alias-legal-system">
            <td>LegalSystem</td>
            <td>
                varchar(tiny)
            </td>
            <td>
                LegalSystems (Legal Systems for Governing Law/Choice of Law
                 Example: GBREW
            </td>
        </tr>
        <tr id="alias-rejection-code">
            <td>RejectionCode</td>
            <td>
                uint(1)
            </td>
            <td>
                Codes returned in rejection messages when a request is not accepted.
                 Example: 10
            </td>
        </tr>
        <tr id="alias-tag">
            <td>Tag</td>
            <td>
                uint(1)
            </td>
            <td>
                Predefined tags for output metadata.
                 Example: 1
            </td>
        </tr>
        <tr id="alias-address">
            <td>Address</td>
            <td>
                varbin(small)
            </td>
            <td>
                A representation of a bitcoin address in raw format, with no check sum or encoding.
                 Example: 20f8d521553a2b0de0ceba82b70c5dd184c6cd2f43
            </td>
        </tr>
        <tr id="alias-contract-code">
            <td>ContractCode</td>
            <td>
                bin(32)
            </td>
            <td>
                32 randomly generated bytes. Each Contract Code should be unique. The Contract ID will be human facing and will be the Contract Code, with a checksum, encoded in base58 and prefixed by &#39;CON&#39;. Contract ID = CON &#43; base58(ContractCode &#43; checksum).  Eg. Contract ID = &#39;CON18RDoKK7Ed5zid2FkKVy7q3rULr4tgfjr4&#39;
                 Example: 260840c0b3d4dadb870cd34ffbfc47fed903fe7d94a7a5bab491fb728aebcc74
            </td>
        </tr>
        <tr id="alias-instrument-type">
            <td>InstrumentType</td>
            <td>
                fixedchar(3)
            </td>
            <td>
                A code representing the type of instrument and the structure of the payload.
                 Example: CCY
            </td>
        </tr>
        <tr id="alias-instrument-code">
            <td>InstrumentCode</td>
            <td>
                bin(20)
            </td>
            <td>
                Represents a unique identifier for an instrument/token.
                 Example: 0e6996402ea456156838652e3bd82c6c0986ef79
            </td>
        </tr>
        <tr id="alias-timestamp">
            <td>Timestamp</td>
            <td>
                uint(8)
            </td>
            <td>
                Represents a time, encoded as a 64 bit unsigned integer representing the number of nanoseconds since the Unix epoch.
                 Example: 1594668650000000000
            </td>
        </tr>
        <tr id="alias-tx-id">
            <td>TxId</td>
            <td>
                bin(32)
            </td>
            <td>
                Represents a Bitcoin transaction ID, the double SHA256 hash of the serialized transaction.
                 Example: 9d1ef0b1201c1dec3c1eb1caf758a988205226173e988e7a04afb4ea9977f506
            </td>
        </tr>
        <tr id="alias-public-key">
            <td>PublicKey</td>
            <td>
                bin(33)
            </td>
            <td>
                Represents a compressed public key.
                 Example: 027fed903fe7d94a7a5bab491fb728aebcc74260840c0b3d4dadb870cd34ffbfc4
            </td>
        </tr>
        <tr id="alias-signature">
            <td>Signature</td>
            <td>
                varbin(tiny)
            </td>
            <td>
                Represents a DER encoded elliptic curve signature.
                 Example: 3044022036164b0c724e6f19e234306444a11631b2f8e47d05468a099928adce0dead62102205138a635827d61915483e7ca1a53b37975a9aa0617c78ef7ac199d94742c36cf
            </td>
        </tr>
</table>
