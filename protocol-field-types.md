# Protocol Field Types

- [Primitive Types](#primitive-types)
- [List Types](#list-types)
- [Variable Sizes](#variable-sizes)
- [Basic Types](#basic-types)

Each field in a protocol action is assigned with a data type. Standard scalar types have a single value, these include primitive and basic types. Fields can also be defined to be a list of objects.

<a name="primitive-types"></a>
## Primitive Types

<table>
   <tr>
        <th style="width:15%">Type</th>
        <th>Description</th>
   </tr>
    <tr><td>int</td><td>A signed integer. <code>size</code> is the number of bytes for the integer. Valid values for <code>size</code> are 1, 2, 4, 8.</td></tr>
    <tr><td>uint</td><td>An unsigned integer. <code>size</code> is the number of bytes for the integer. Valid values for <code>size</code> are 1, 2, 4, 8.</td></tr>
    <tr><td>float</td><td>A floating point number. <code>size</code> is the number of bytes for the float. Valid values for <code>size</code> are 4 and 8.</td></tr>
    <tr><td>bool</td><td>A boolean stored as 1 byte. Zero is false, non-zero is true.</td></tr>
    <tr><td>bin</td><td>Fixed length binary data. <code>size</code> is the length in bytes of the data.</td></tr>
    <tr>
        <td>varbin</td>
        <td>
            Variable length binary data.
            <code>varSize</code> defines the maximum size of the data as defined in <a href="#variable-sizes">Variable Sizes</a>.
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
            <code>varSize</code> defines the maximum size of the data as defined in <a href="#variable-sizes">Variable Sizes</a>.
        </td>
    </tr>
</table>

<a name="list-types"></a>
## List Types

Fields within the Tokenized protocol can be defined as a list of a specified data type.
This is done by adding a `[]` to the end of the `type` value.
The maximum number of elements in a list are defined by `listSize` as defined in <a href="#variable-sizes">Variable Sizes</a>.

<a name="variable-sizes"></a>
## Variable Sizes

Fields within the Tokenized protocol can be lists of objects or variable length objects.
The maximum number of elements in a list are defined by `listSize`.
The maximum size of a variable sized object are defined by `varSize`.
The valid values for `listSize` and `varSize` are as follows.
If no value is specified for `listSize` or `varSize` then `tiny` is used.

<table>
    <tr>
        <th style="width:15%">Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>tiny</td>
        <td>Defines a max size of 2^8^-1 or 255.</td>
    </tr>
    <tr>
        <td>small</td>
        <td>Defines a max size of 2^16^-1 or 65,535.</td>
    </tr>
    <tr>
        <td>medium</td>
        <td>Defines a max size of 2^32^-1 or 4,294,967,295.</td>
    </tr>
    <tr>
        <td>large</td>
        <td>Defines a max size of 2^64^-1 or approximately 1.8x10^19^.</td>
    </tr>
</table>

<a name="basic-types"></a>
## Basic Types

<a name="type-action"></a>
### Action

`Action` implements a base interface for all message types.

Provides the ability to serialize the data as a Bitcoin OP_RETURN script.

<a name="type-asset"></a>
### Asset

`Asset` is the interface for asset payloads.

Provides the ability to serialize asset data.

<a name="type-message"></a>
### Message

`Message` is the interface for message payloads.

Provides the ability to serialize message data.

<a name="type-tx-id"></a>
### Tx Id

`TxId` represents a Bitcoin transaction ID.

It is the double SHA256 hash of the serialized transaction.

`size` does not need to be specified and is always 32 bytes.

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

`Timestamp` represents a time. It is encoded as a 64 bit unsigned integer representing the number of nanoseconds since the Unix epoch.

The `size` does not need to be specified and is always 8 bytes.
