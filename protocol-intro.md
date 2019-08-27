# Protocol Field Types

- [Envelope Fields](#envelope-fields)
- [Common Field Types](#common-field-types)
    - [Primitive Types](#primitive-types)
    - [List Types](#list-types)
    - [Variable Sizes](#variable-sizes)
    - [Basic Types](#basic-types)

<a name="header-fields"></a>
## Envelope Fields

Every protocol action is prepended with a header that specifies the necessary details about the subsequent action contents.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>PayloadVersion</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that determines the structure of the action payload and field definitions.
        </td>
    </tr>
    <tr>
        <td>PayloadIdentifier</td>
        <td>
            fixedchar(2)
        </td>
        <td>
            The Action Code that determines the expected contents of the action payload. Example: C1
        </td>
    </tr>
</table>

<a name="common-field-types"></a>
## Common Field Types

Each field in a protocol action is assigned with a data type. Standard scalar types have a single value, these include primitive and basic types. Fields can also be defined to be a list of objects.

<a name="primitive-types"></a>
### Primitive Types

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
### List Types

Fields within the Tokenized protocol can be defined as a list of a specified data type.
This is done by adding a `[]` to the end of the `type` value.
The maximum number of elements in a list are defined by `listSize` as defined in <a href="#variable-sizes">Variable Sizes</a>.

<a name="variable-sizes"></a>
### Variable Sizes

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
