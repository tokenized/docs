
#Settlement Action

Settlement Action -  (to be used for finalizing the transfer of bitcoins and tokens from exchange, issuance, swap actions)

The following breaks down the construction of a Settlement Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:6%" class="s0">Field</th>
               <th style="width:9%" class="s1">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:29%" class="s1">Example Values</th>
            <th style="width:26%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th style="width:14%" class="s2">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="s5" rowspan="12">Metadata (OP_RETURN Payload)</td>
            <td class="t6">Header[]</td>
            <td class="t6">Header Array</td>
            <td class="t6">-</td>
            <td class="t6">-</td>
            <td class="t6">Common header data for all messages</td>
            <td class="t6">Header</td>
            <td class="t7"></td>
        </tr>
                <tr>
            <td class="t10">Text Encoding</td>
            <td class="t10">TextEncoding</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="t10">uint8</td>
            <td class="t11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>                <tr>
            <td class="t10">Transfer Type</td>
            <td class="t10">TransferType</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">S</td>
            <td class="t10">S - Send, E - Exchange, X - Swap</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset Type 1</td>
            <td class="t10">AssetType1</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">RRE</td>
            <td class="t10">eg. Share, Bond, Ticket</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset ID 1</td>
            <td class="t10">AssetID1</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="t10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans. </td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset Type 2</td>
            <td class="t10">AssetType2</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">SHC</td>
            <td class="t10">eg. Share, Bond, Ticket. NULL for Send and Exchange Response Type.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset ID 2</td>
            <td class="t10">AssetID2</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="t10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.  NULL for Send and Exchange Response Type.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Qty Asset 1 Settlements</td>
            <td class="t10">QtyAsset1Settlements</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">1</td>
            <td class="t10">Number of settlements for Asset 1.</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset 1 Address X Qty</td>
            <td class="t10">Asset1AddressXQty</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">21000</td>
            <td class="t10">The resulting token balance of Asset 1 for Address X. (X = Output Index)</td>
            <td class="t10">uint64</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Qty Asset 2 Addresses</td>
            <td class="t10">QtyAsset2Addresses</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">1</td>
            <td class="t10">Number of settlements for Asset 1. NULL for Send and Exchange Response Type.</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Asset 2 Address X Qty</td>
            <td class="t10">Asset2AddressXQty</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">1,000,000</td>
            <td class="t10">The resulting token balance of Asset 2 for Address X. (X = Output Index) NULL for Send and Exchange Response Type.</td>
            <td class="t10">uint64</td>
            <td class="t11"></td>
        </tr>                <tr>
            <td class="t10">Timestamp</td>
            <td class="t10">Timestamp</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">1551767413250187179</td>
            <td class="t10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="t10">timestamp</td>
            <td class="t11">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>