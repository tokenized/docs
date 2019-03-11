

#Asset Modification Action

Asset Modification Action -  Token Dilutions, Call Backs/Revocations, burning etc.

The following breaks down the construction of a Asset Modification Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="6">Metadata (OP_RETURN Payload)</td>
            <td class="a6" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="a10">Text Encoding</td>
            <td class="a10">TextEncoding</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="a10">uint8</td>
            <td class="a11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>

        <tr><td class="a10">Asset Revision</td>
            <td class="a10">AssetRevision</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10">Counter. (Subfield cannot be manually changed by Asset Modification Action.  Only SC can increment by 1 with each AC action. SC will reject AM actions where the wrong asset revision has been selected. </td>
            <td class="a10">uint64</td>
            <td class="a11">Cannot be Amended</td>
        </tr>

        <tr><td class="a10">ModificationCount</td>
            <td class="a10">ModificationCount</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10">Number of Modifications. Must be less than the max Subfield Index of CF.</td>
            <td class="a10">uint8</td>
            <td class="a11"></td>
        </tr>

        <tr><td class="a10">Modifications</td>
            <td class="a10">Modifications</td>
            <td class="a10">0</td>
            <td class="a10" style="word-break:break-all"></td>
            <td class="a10"></td>
            <td class="a10">Amendment[]</td>
            <td class="a11"></td>
        </tr>

        <tr><td class="a10">Ref Tx-ID</td>
            <td class="a10">RefTxID</td>
            <td class="a10">32</td>
            <td class="a10" style="word-break:break-all">a8700385d4cc62628cc34629862121f84e6237689de8e45e151dcbc8cf30b33d</td>
            <td class="a10">Tx-ID of the associated Result action (governance) that permitted the modifications.</td>
            <td class="a10">sha256</td>
            <td class="a11"></td>
        </tr>

    </table>
</div>


<div class="ui modal" id="type-Header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="a10">Protocol Identifier</td>
                <td class="a10">ProtocolID</td>
                <td class="a10">13</td>
                <td class="a10" style="word-break:break-all">tokenized.com</td>
                <td class="a10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="a10">string</td>
                <td class="a11"></td>
            </tr>
            <tr>
                <td class="a10">Push Data</td>
                <td class="a10">OpPushdata</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">77</td>
                <td class="a10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="a10">opcode</td>
                <td class="a11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="a10">Length of Action Payload</td>
                <td class="a10">LenActionPayload</td>
                <td class="a10">2</td>
                <td class="a10" style="word-break:break-all">409</td>
                <td class="a10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="a10">pushdata_length</td>
                <td class="a11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="a10">Version</td>
                <td class="a10">Version</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">0</td>
                <td class="a10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="a10">uint8</td>
                <td class="a11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="a10">Action Prefix</td>
                <td class="a10">ActionPrefix</td>
                <td class="a10">2</td>
                <td class="a10" style="word-break:break-all">C1</td>
                <td class="a10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="a10">string</td>
                <td class="a11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

