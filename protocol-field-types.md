# Protocol Field Types

- [Primitive Types](#primitive-types)
- [Basic Types](#basic-types)
- [Compound Types](#compound-types)

Each field in a protocol action is assigned with a data type. Standard scalar types have a single value, these include primitive and basic types. While [compound types](#compound-types) are made up of fields that have their own types, including nested compound types.

<a name="primitive-types"></a>
## Primitive Types

<table>
   <tr>
        <th style="width:15%">Type</th>
        <th>Description</th>
   </tr>
    <tr><td>int</td><td>A signed integer. <code>size</code> is the number of bits for the integer. Valid values for <code>size</code> are 8, 16, 32, 64.</td></tr>
    <tr><td>uint</td><td>An unsigned integer. <code>size</code> is the number of bits for the integer. Valid values for <code>size</code> are 8, 16, 32, 64.</td></tr>
    <tr><td>float</td><td>A floating point number. <code>size</code> is the number of bits for the float. Valid values for <code>size</code> are 32 and 64.</td></tr>
    <tr><td>bool</td><td>A boolean stored as 1 byte.</td></tr>
    <tr><td>bin</td><td>Fixed length binary data. <code>size</code> is the length in bytes of the data.</td></tr>
    <tr>
        <td>varbin</td>
        <td>
            Variable length binary data.
            The data is preceded by an integer that specifies the actual length in bytes.
            <code>size</code> is the number of bits used to serialize the length in bytes of the data.
            Valid values for <code>size</code> are 8, 16, 32, and 64.
            For example, a <code>varbin</code> value with a <code>size</code> of 8 will be able to contain up to 255 bytes and will be preceded by a 1 byte unsigned integer specifying the length in bytes.
        </td>
    </tr>
    <tr>
        <td>fixedchar</td>
        <td>
            Fixed length text data.
            The data is assumed to be UTF-8 unless the first two bytes are a valid UTF-16 BOM (Byte Order Method).
            <code>size</code> is the length in bytes of the data.
        </td>
    </tr>
    <tr>
        <td>varchar</td>
        <td>
            Variable length text data.
            The data is assumed to be UTF-8 unless the first two bytes are a valid UTF-16 BOM (Byte Order Method).
            The data is preceded by an integer that specifies the actual length in bytes.
            <code>size</code> is the number of bits used to serialize the length in bytes of the data.
            Valid values for <code>size</code> are 8, 16, 32, and 64.
            For example, a `varchar` value with a <code>size</code> of 8 will be able to contain up to 255 bytes and will be preceded by a 1 byte unsigned integer specifying the length in bytes.
        </td>
    </tr>
</table>

<a name="basic-types"></a>
## Basic Types

<a name="type-op-return-message"></a>
### Op Return Message

`OpReturnMessage` implements a base interface for all message types.

Provides the ability to serialize the data as a Bitcoin OP_RETURN script and to request the variable payload data.

<a name="type-payload-message"></a>
### Payload Message

`PayloadMessage` is the interface for messages that are derived from payloads, such as asset types and message types.

Provides the ability to serialize the data.

<a name="type-tx-id"></a>
### Tx Id

`TxId` represents a Bitcoin transaction ID.

It is the double SHA256 hash of the serialized transaction.

`size` does not need to be specified and is always 32 bytes.

<a name="type-public-key-hash"></a>
### Public Key Hash

`PublicKeyHash` represents a Bitcoin Public Key Hash.

It is the RIPEMD160 hash of the SHA256 of the serialized public key.

Public key hashes are used as an "address" to send/receive transactions, tokens, and messages.

`size` does not need to be specified and is always 20 bytes.

<a name="type-asset-code"></a>
### Asset Code

`AssetCode` represents a unique identifier for an asset/token.

`size` does not need to be specified and is always 32 bytes.

<a name="type-contract-code"></a>
### Contract Code

`ContractCode` represents a unique identifier for a static contract.

The `size` does not need to be specified and is always 32 bytes.

<a name="type-timestamp"></a>
### Timestamp

`Timestamp` represents a time. `size` does not need to be specified and is always 8 bytes.

<a name="type-polity"></a>
### Polity

`Polity` represents a unique identifier for a nation/state/political entity. `size` does not need to be specified and is always 3 bytes.

<a name="compound-types"></a>
## Compound Types

<div class="content-list collection-method-list" markdown="1">
- [Administrator](#type-administrator)
- [Age Restriction](#type-age-restriction)
- [Amendment](#type-amendment)
- [Asset Settlement](#type-asset-settlement)
- [Asset Transfer](#type-asset-transfer)
- [Entity](#type-entity)
- [Manager](#type-manager)
- [Oracle](#type-oracle)
- [Quantity Index](#type-quantity-index)
- [Target Address](#type-target-address)
- [Token Receiver](#type-token-receiver)
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
            Role
        </td>
        <td>
            Chairman, Director, Managing Partner, etc.. Found in 'Roles' in Specification/Resources
            7 - Chair Example: 7
        </td>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)
             Example: Satoshi Nakamoto
        </td>
    </tr>
</table>



<a name="type-age-restriction"></a>
### Age Restriction

Age restriction is used to specify required ages for asset ownership.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Lower</td>
        <td>
            uint(1)
        </td>
        <td>
            The lowest age valid to own asset. Zero for no restriction.
            
        </td>
    </tr>
    <tr>
        <td>Upper</td>
        <td>
            uint(1)
        </td>
        <td>
            The highest age valid to own asset. Zero for no restriction.
            
        </td>
    </tr>
</table>



<a name="type-amendment"></a>
### Amendment

An Amendment is used to describe the modification of a single field in a Contract or Asset, as defined in the ContractFormation and AssetCreation messages.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>FieldIndex</td>
        <td>
            uint(1)
        </td>
        <td>
            Index of the field to be amended.
            A field with a complex array type uses the same FieldIndex value for all elements. For example, in C1 the VotingSystems field is FieldIndex 16. Indexes are zero based. Example: 2
        </td>
    </tr>
    <tr>
        <td>Element</td>
        <td>
            uint(2)
        </td>
        <td>
            Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.
            To specify the 3rd VotingSystem of a Contract, the value 2 would be given. Indexes are zero based. Example: 0
        </td>
    </tr>
    <tr>
        <td>SubfieldIndex</td>
        <td>
            uint(1)
        </td>
        <td>
            Index of the subfield to be amended. This only applies to specific fields containing complex types with subfields. This is used to specify which field of the object the amendment applies to.
            For example to specify the 2nd field of a VotingSystem, value 1 would be given. Example: 1
        </td>
    </tr>
    <tr>
        <td>SubfieldElement</td>
        <td>
            uint(2)
        </td>
        <td>
            Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.
            For example to specify the 2nd field of a VotingSystem, value 1 would be given. Example: 1
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
            varbin(32)
        </td>
        <td>
            New data for the amended subfield. Data type depends on the the type of the field being amended. The value should be serialize as defined by the protocol.
            The bytes should be in an format appropriate for the field being modified.
        </td>
    </tr>
</table>



<a name="type-asset-settlement"></a>
### Asset Settlement

AssetSettlement is the data required to settle an asset transfer.

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
            Index of input containing the contract's address for this offset
            
        </td>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type. Example: COU
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset, made up of 32 randomly generated bytes. The asset code is a human readable identifier that can be used in a similar way to a Bitcoin (BSV) address.
            Cannot be changed by issuer, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>Settlements</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[]</a>
        </td>
        <td>
            Each element contains the resulting token balance of Asset X for the output Address, which is referred to by the index.
            
        </td>
    </tr>
</table>



<a name="type-asset-transfer"></a>
### Asset Transfer

AssetTransfer is the data required to transfer an asset.

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
            Index of output containing the contract's address for this offset
            
        </td>
    </tr>
    <tr>
        <td>AssetType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            Three letter character that specifies the asset type. Example: COU
             Example: SHC
        </td>
    </tr>
    <tr>
        <td>AssetCode</td>
        <td>
            <a href="field-types#type-asset-code">AssetCode</a>
        </td>
        <td>
            A unique code that is used to identify the asset, made up of 32 randomly generated bytes. The asset code is a human readable identifier that can be used in a similar way to a Bitcoin (BSV) address.
            Cannot be changed by issuer, operator or smart contract.
        </td>
    </tr>
    <tr>
        <td>AssetSenders</td>
        <td>
            <a href="field-types#type-quantity-index">QuantityIndex[]</a>
        </td>
        <td>
            Each element has the value of tokens to be spent from the input address, which is referred to by the index.
            
        </td>
    </tr>
    <tr>
        <td>AssetReceivers</td>
        <td>
            <a href="field-types#type-token-receiver">TokenReceiver[]</a>
        </td>
        <td>
            Each element has the value of tokens to be received by the output address, which is referred to by the index.
            
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
            varchar(8)
        </td>
        <td>
            Length 1-255 bytes (0 is not valid). Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. 
             Example: Tesla Inc.
        </td>
    </tr>
    <tr>
        <td>Type</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).
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
        <td>AddressIncluded</td>
        <td>
            bool
        </td>
        <td>
            Registered/Physical/mailing address(HQ). Y-1/N-0, N means there is no issuer address.
            Entity/Contracting Party X Details Example: 1
        </td>
    </tr>
    <tr>
        <td>UnitNumber</td>
        <td>
            varchar(8)
        </td>
        <td>
            Issuer/Entity/Contracting Party X Address Details (eg. HQ)
             Example: 2
        </td>
    </tr>
    <tr>
        <td>BuildingNumber</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: 13577
        </td>
    </tr>
    <tr>
        <td>Street</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Fairmont Ave
        </td>
    </tr>
    <tr>
        <td>SuburbCity</td>
        <td>
            varchar(8)
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
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. Address for text-based communication: eg. email address, Bitcoin address
             Example: satoshi@tokenized.com
        </td>
    </tr>
    <tr>
        <td>PhoneNumber</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-50 bytes. 0 is valid. Phone Number for Entity.
             Example: 0448484848
        </td>
    </tr>
    <tr>
        <td>Administration</td>
        <td>
            <a href="field-types#type-administrator">Administrator[]</a>
        </td>
        <td>
            A list of people that are in Administrative Roles for the Entity.  eg. Chair, Director, Managing Partner, etc.
            
        </td>
    </tr>
    <tr>
        <td>Management</td>
        <td>
            <a href="field-types#type-manager">Manager[]</a>
        </td>
        <td>
            A list of people in Management Roles for the Entity. e.g CEO, COO, CTO, CFO, Secretary, Executive, etc.
            
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
            Role
        </td>
        <td>
            CEO, COO, CFO, etc. Found in 'Roles' in Specification/Resources
            5 - CEO Example: 5
        </td>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)
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
        <td>Name</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid. Oracle X Name (eg. Coinbase, Tokenized, etc.)
             Example: Tokenized
        </td>
    </tr>
    <tr>
        <td>URL</td>
        <td>
            varchar(8)
        </td>
        <td>
            Length 0-255 bytes. 0 is valid. If applicable: URL for REST/RPC Endpoint
             Example: http://oracle.tokenized.com/api/3650d9/version2010
        </td>
    </tr>
    <tr>
        <td>PublicKey</td>
        <td>
            varbin(8)
        </td>
        <td>
            Length 0-255 bytes. 0 is not valid. Oracle Public Key (eg. Bitcoin Public key), used to confirm digital signed proofs for transfers.  Can also be the same public address that controls a Tokenized Oracle.
            
        </td>
    </tr>
</table>



<a name="type-quantity-index"></a>
### Quantity Index

A QuantityIndex contains a quantity, and an index. The quantity could be used to describe a number of tokens, or a value. The index is used to refer to an input index position.

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
            The index of the input sending the tokens
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
            <a href="field-types#type-public-key-hash">PublicKeyHash</a>
        </td>
        <td>
            Public address where the token balance will be changed.
            
        </td>
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



<a name="type-token-receiver"></a>
### Token Receiver

A TokenReceiver is contains a quantity, index, and oracle signature. The quantity could be used to describe a number of tokens, or a value. The index is used to refer to an input index position.

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
            The index of the output receiving the tokens
             Example: 0
        </td>
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
            0 = No Oracle-signed Message (OracleConfirmationSig skipped in serialization), 1 = ECDSA+secp256k1. If the contract for the asset being received has oracles, then a signature is required from one of them.
             Example: 1
        </td>
    </tr>
    <tr>
        <td>OracleConfirmationSig</td>
        <td>
            varbin(8)
        </td>
        <td>
            Length 0-255 bytes. If restricted to a oracle (whitelist) or has transfer restrictions (age, location, investor status): ECDSA+secp256k1 (or the like) signed message provided by an approved/trusted oracle through an API signature of the defined message. If no transfer restrictions(trade restriction/age restriction fields in the Asset Type payload. or restricted to a whitelist by the Contract Auth Flags, it is a NULL field.
            
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
            varchar(8)
        </td>
        <td>
            eg. Special Resolutions, Ordinary Resolutions, Fundamental Matters, General Matters, Directors' Vote, Poll, etc.
             Example: Special Resolutions
        </td>
    </tr>
    <tr>
        <td>VoteType</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            R - Relative Threshold, A - Absolute Threshold, P - Plurality,  (Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast.  Abstentations/spoiled votes do not detract from the liklihood of a vote passing as they are not included in the denominator.  Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens.  Abstentations/spoiled votes detract from the liklihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the vote cannot pass.  50% of all tokens would have had to vote for one vote option for the vote to be successful.
             Example: A
        </td>
    </tr>
    <tr>
        <td>TallyLogic</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            0 - Standard Scoring (+1 * # of tokens owned), 1 - Weighted Scoring (1st choice * Vote Max * # of tokens held, 2nd choice * Vote Max-1 * # of tokens held,..etc.) 
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
            Where an asset has a vote multiplier, true must be set here for the vote multiplier to count, otherwise votes are simply treated as 1x per token.
            
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


