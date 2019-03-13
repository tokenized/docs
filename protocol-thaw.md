

#Thaw Action

Thaw Action -  to be used to comply with contractual obligations or legal requirements.  The Alleged Offender's tokens will be unfrozen to allow them to resume normal exchange and governance activities.

The following breaks down the construction of a Thaw Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="4">Metadata (OP_RETURN Payload)</td>
            <td class="e7" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="e10">Number of Addresses</td>
            <td class="e10">AddressCount</td>
            <td class="e10">2</td>
            <td class="e10" style="word-break:break-all">0</td>
            <td class="e10">0 - 65,535</td>
            <td class="e10">uint16</td>
            <td class="e11"></td>
        </tr>

        <tr><td class="e10">Addresses</td>
            <td class="e10">Addresses</td>
            <td class="e10">0</td>
            <td class="e10" style="word-break:break-all"></td>
            <td class="e10">Addresses holding tokens to be thawed.</td>
            <td class="e10">Address[]</td>
            <td class="e11"></td>
        </tr>

        <tr><td class="e10">Timestamp</td>
            <td class="e10">Timestamp</td>
            <td class="e10">8</td>
            <td class="e10" style="word-break:break-all">1551767413250187179</td>
            <td class="e10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="e10">timestamp</td>
            <td class="e11">Cannot be changed by issuer, operator. Smart contract controls.</td>
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
                <td class="e10">Protocol Identifier</td>
                <td class="e10">ProtocolID</td>
                <td class="e10">13</td>
                <td class="e10" style="word-break:break-all">tokenized.com</td>
                <td class="e10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="e10">string</td>
                <td class="e11"></td>
            </tr>
            <tr>
                <td class="e10">Push Data</td>
                <td class="e10">OpPushdata</td>
                <td class="e10">1</td>
                <td class="e10" style="word-break:break-all">77</td>
                <td class="e10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="e10">opcode</td>
                <td class="e11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="e10">Length of Action Payload</td>
                <td class="e10">LenActionPayload</td>
                <td class="e10">2</td>
                <td class="e10" style="word-break:break-all">409</td>
                <td class="e10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="e10">pushdata_length</td>
                <td class="e11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="e10">Version</td>
                <td class="e10">Version</td>
                <td class="e10">1</td>
                <td class="e10" style="word-break:break-all">0</td>
                <td class="e10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="e10">uint8</td>
                <td class="e11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="e10">Action Prefix</td>
                <td class="e10">ActionPrefix</td>
                <td class="e10">2</td>
                <td class="e10" style="word-break:break-all">C1</td>
                <td class="e10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="e10">string</td>
                <td class="e11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

