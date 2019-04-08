


# Message Action

Message Action - the message action is a general purpose communication action. 'Twitter/SMS' for Issuers/Investors/Users. The message txn can also be used for passing partially signed txns on-chain, establishing private communication channels and EDI (receipting, invoices, PO, and private offers/bids). The messages are broken down by type for easy filtering in the a user's wallet. The Message Types are listed in the Message Types table.


The following breaks down the construction of a Message Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:9%" class="s0">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:25%" class="s1">Example Values</th>
            <th style="width:36%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th class="s1">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="m5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="m9">Address Indexes</td>
            <td class="m10">AddressIndexes</td>
            <td class="m10">0</td>
            <td class="m10"></td>
            <td class="m10">Associates the message to a particular output by the index.</td>
            <td class="m10">uint16[]</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m9">Message Type</td>
            <td class="m10">MessageType</td>
            <td class="m10">0</td>
            <td class="m10">6000</td>
            <td class="m10">Potential for up to 65,535 different message types. Values from resources/Messages.yaml</td>
            <td class="m10">MessageType</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m9">Message Payload</td>
            <td class="m10">MessagePayload</td>
            <td class="m10">32</td>
            <td class="m10">Hello world!</td>
            <td class="m10"><abbr title="Public or private (RSA public key, Diffie-Hellman). Issuers/Contracts can send the signifying amount of satoshis to themselves for public announcements or private 'notes' if encrypted. See Message Types for a full list of potential use cases.
">Public or private (RSA public key, Diffie-Hellman). Issuers/Contracts can send the signify ...</abbr></td>
            <td class="m10">varbin</td>
            <td class="m10"></td>
        </tr>
    </table>
</div>

##Message Action Transaction Summary

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
       <tr style='height:19px;'>
            <th class="s0" colspan="6">Smart Contract Operator Fee: 0</th>
       </tr>
       <tr style='height:19px;'>
            <th style="width:10%" class="s0">Index (input)</th>
            <th style="width:20%" class="s1">Txn inputs</th>
            <th style="width:20%" class="s1">Comments</th>
            <th style="width:10%" class="s1">Index (output)</th>
            <th style="width:20%" class="s1">Txn outputs</th>
            <th class="s1">Comments</th>
       </tr>


       <tr>
            <td class="m5">0</td>
            <td class="m6">Msg Sender's Public Address</td>
            <td class="m6"></td>
            <td class="m10">0</td>
            <td class="m10">Msg Receiver's Public Address</td>
            <td class="m10">Dust limit rule minimum value output of 546</td>
        </tr>

    </table>
</div>

<div class="ui modal" id="type-Header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="m10">Protocol Identifier</td>
                <td class="m10">ProtocolID</td>
                <td class="m10">13</td>
                <td class="m10">tokenized.com</td>
                <td class="m10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="m10">byte</td>
                <td class="m10"></td>
            </tr>
            <tr>
                <td class="m10">Push Data</td>
                <td class="m10">OpPushdata</td>
                <td class="m10">1</td>
                <td class="m10">0x4d</td>
                <td class="m10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="m10">byte</td>
                <td class="m10"></td>
            </tr>
            <tr>
                <td class="m10">Length of Action Payload</td>
                <td class="m10">LenActionPayload</td>
                <td class="m10"></td>
                <td class="m10">tokenized.com</td>
                <td class="m10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="m10">byte</td>
                <td class="m10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="m10">Version</td>
                <td class="m10">Version</td>
                <td class="m10">1</td>
                <td class="m10">0</td>
                <td class="m10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="m10">uint8</td>
                <td class="m10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="m10">Action Prefix</td>
                <td class="m10">ActionPrefix</td>
                <td class="m10">2</td>
                <td class="m10">M1</td>
                <td class="m10" style="word-break:break-all">// M1 identifies data as a Message message.</td>
                <td class="m10">string</td>
                <td class="m10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
