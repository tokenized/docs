

#Establishment Action

Establishment Action -  Establishes an on-chain register.

The following breaks down the construction of a Establishment Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="3">Metadata (OP_RETURN Payload)</td>
            <td class="r6" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="r10">Text Encoding</td>
            <td class="r10">TextEncoding</td>
            <td class="r10">1</td>
            <td class="r10" style="word-break:break-all">0</td>
            <td class="r10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="r10">uint8</td>
            <td class="r11"></td>
        </tr>

        <tr><td class="r10">Message</td>
            <td class="r10">Message</td>
            <td class="r10">25</td>
            <td class="r10" style="word-break:break-all">North America Whitelist</td>
            <td class="r10">Length only limited by Bitcoin protocol.</td>
            <td class="r10">nvarchar64</td>
            <td class="r11"></td>
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
                <td class="r10">Protocol Identifier</td>
                <td class="r10">ProtocolID</td>
                <td class="r10">13</td>
                <td class="r10" style="word-break:break-all">tokenized.com</td>
                <td class="r10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="r10">string</td>
                <td class="r11"></td>
            </tr>
            <tr>
                <td class="r10">Push Data</td>
                <td class="r10">OpPushdata</td>
                <td class="r10">1</td>
                <td class="r10" style="word-break:break-all">77</td>
                <td class="r10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="r10">opcode</td>
                <td class="r11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="r10">Length of Action Payload</td>
                <td class="r10">LenActionPayload</td>
                <td class="r10">2</td>
                <td class="r10" style="word-break:break-all">409</td>
                <td class="r10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="r10">pushdata_length</td>
                <td class="r11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="r10">Version</td>
                <td class="r10">Version</td>
                <td class="r10">1</td>
                <td class="r10" style="word-break:break-all">0</td>
                <td class="r10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="r10">uint8</td>
                <td class="r11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="r10">Action Prefix</td>
                <td class="r10">ActionPrefix</td>
                <td class="r10">2</td>
                <td class="r10" style="word-break:break-all">C1</td>
                <td class="r10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="r10">string</td>
                <td class="r11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

