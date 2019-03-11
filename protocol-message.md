

#Message Action

Message Action -  the message action is a general purpose communication action. 'Twitter/sms' for Issuers/Investors/Users. The message txn can also be used for passing partially signed txns on-chain, establishing private communication channels and EDI (receipting, invoices, PO, and private offers/bids).  The messages are broken down by type for easy filtering in the a user's wallet.  The Message Types are listed in the Message Types table.

The following breaks down the construction of a Message Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="m6" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="m10">Text Encoding</td>
            <td class="m10">TextEncoding</td>
            <td class="m10">1</td>
            <td class="m10" style="word-break:break-all">0</td>
            <td class="m10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="m10">uint8</td>
            <td class="m11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>

        <tr><td class="m10">Qty Receiving Addresses</td>
            <td class="m10">QtyReceivingAddresses</td>
            <td class="m10">1</td>
            <td class="m10" style="word-break:break-all">2</td>
            <td class="m10">0-255 Message Receiving Addresses</td>
            <td class="m10">uint8</td>
            <td class="m11"></td>
        </tr>

        <tr><td class="m10">Address Indexes</td>
            <td class="m10">AddressIndexes</td>
            <td class="m10">0</td>
            <td class="m10" style="word-break:break-all"></td>
            <td class="m10">Associates the message to a particular output by the index.</td>
            <td class="m10">uint16[]</td>
            <td class="m11"></td>
        </tr>

        <tr><td class="m10">Message Type</td>
            <td class="m10">MessageType</td>
            <td class="m10">2</td>
            <td class="m10" style="word-break:break-all">6</td>
            <td class="m10">Potential for up to 65,535 different message types</td>
            <td class="m10">string</td>
            <td class="m11"></td>
        </tr>

        <tr><td class="m10">Message Payload</td>
            <td class="m10">MessagePayload</td>
            <td class="m10">0</td>
            <td class="m10" style="word-break:break-all">Hello world!</td>
            <td class="m10">Length 0-65,535 bytes. Public or private (RSA public key, Diffie-Hellman).  Issuers/Contracts can send the signifying amount of satoshis to themselves for public announcements or private 'notes' if encrypted.  See Message Types for a full list of potential use cases.</td>
            <td class="m10">nvarchar16</td>
            <td class="m11"></td>
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
                <td class="m10">Protocol Identifier</td>
                <td class="m10">ProtocolID</td>
                <td class="m10">13</td>
                <td class="m10" style="word-break:break-all">tokenized.com</td>
                <td class="m10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="m10">string</td>
                <td class="m11"></td>
            </tr>
            <tr>
                <td class="m10">Push Data</td>
                <td class="m10">OpPushdata</td>
                <td class="m10">1</td>
                <td class="m10" style="word-break:break-all">77</td>
                <td class="m10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="m10">opcode</td>
                <td class="m11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="m10">Length of Action Payload</td>
                <td class="m10">LenActionPayload</td>
                <td class="m10">2</td>
                <td class="m10" style="word-break:break-all">409</td>
                <td class="m10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="m10">pushdata_length</td>
                <td class="m11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="m10">Version</td>
                <td class="m10">Version</td>
                <td class="m10">1</td>
                <td class="m10" style="word-break:break-all">0</td>
                <td class="m10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="m10">uint8</td>
                <td class="m11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="m10">Action Prefix</td>
                <td class="m10">ActionPrefix</td>
                <td class="m10">2</td>
                <td class="m10" style="word-break:break-all">C1</td>
                <td class="m10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="m10">string</td>
                <td class="m11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

