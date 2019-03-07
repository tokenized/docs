
#Message Action

<div class="ui modal" id="header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr>
                <td class="m6">Header[]</td>
                <td class="m6">Header Array</td>
                <td class="m6">-</td>
                <td class="m6">-</td>
                <td class="m6">Common header data for all messages</td>
                <td class="m6">Header</td>
                <td class="m7"></td>
            </tr>
        </table>
    </div>
</div>

Message Action -  the message action is a general purpose communication action. 'Twitter/sms' for Issuers/Investors/Users. The message txn can also be used for passing partially signed txns on-chain, establishing private communication channels including receipting, invoices, PO, and private offers/bids.  The messages are broken down by type for easy filtering in the a user’s wallet.  The Message Types are listed in the Message Types table.

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
            <td class="s5" rowspan="20">Metadata (OP_RETURN Payload)</td>
            <td class="m6" colspan="7"><a href="#" data-popover="header">Header[] - Click to show content</a></td>
        </tr>
        <tr>
            <td class="m10">Text Encoding</td>
            <td class="m10">TextEncoding</td>
            <td class="m10">1</td>
            <td class="m10" style="word-break:break-all">0</td>
            <td class="m10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="m10">uint8</td>
            <td class="m11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr>
            <td class="m10">Qty Receiving Addresses</td>
            <td class="m10">QtyReceivingAddresses</td>
            <td class="m10">1</td>
            <td class="m10" style="word-break:break-all">2</td>
            <td class="m10">0-255 Message Receiving Addresses</td>
            <td class="m10">uint8</td>
            <td class="m11"></td>
        </tr>
        <tr>
            <td class="m10">Address Indexes</td>
            <td class="m10">AddressIndexes</td>
            <td class="m10">0</td>
            <td class="m10" style="word-break:break-all"></td>
            <td class="m10">Associates the message to a particular output by the index.</td>
            <td class="m10">uint16[]</td>
            <td class="m11"></td>
        </tr>
        <tr>
            <td class="m10">Message Type</td>
            <td class="m10">MessageType</td>
            <td class="m10">2</td>
            <td class="m10" style="word-break:break-all">6</td>
            <td class="m10">Potential for up to 65,535 different message types</td>
            <td class="m10">string</td>
            <td class="m11"></td>
        </tr>
        <tr>
            <td class="m10">Message Payload</td>
            <td class="m10">MessagePayload</td>
            <td class="m10">0</td>
            <td class="m10" style="word-break:break-all">Hello world!</td>
            <td class="m10">Length 0-65,535 bytes. Public or private (RSA public key, Diffie-Hellman).  Issuers/Contracts can send the signifying amount of satoshis to themselves for public announcements or private 'notes' if encrypted.  See Message Types for a full list of potential use cases.</td>
            <td class="m10">nvarchar16</td>
            <td class="m11"></td>
        </tr>
        <tr>
            <td class="m10">Timestamp</td>
            <td class="m10">Timestamp</td>
            <td class="m10">8</td>
            <td class="m10" style="word-break:break-all">1551767413250187179</td>
            <td class="m10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="m10">timestamp</td>
            <td class="m11">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>