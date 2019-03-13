
# Rejection Action

Rejection Action - used to reject request actions that do not comply with the Contract. If money is to be returned to a User then it is used in lieu of the Settlement Action to properly account for token balances. All Issuer/User request Actions must be responded to by the Contract with an Action.  The only exception to this rule is when there is not enough fees in the first Action for the Contract response action to remain revenue neutral.  If not enough fees are attached to pay for the Contract response then the Contract will not respond.

The following breaks down the construction of a Rejection Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="m9">Qty Receiving Addresses</td>
            <td class="m10">QtyReceivingAddresses</td>
            <td class="m10">1</td>
            <td class="m10">2</td>
            <td class="m10">0-255 Message Receiving Addresses</td>
            <td class="m10">uint8</td>
            <td class="m10"></td>
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
            <td class="m9">Rejection Type</td>
            <td class="m10">RejectionType</td>
            <td class="m10">1</td>
            <td class="m10">1</td>
            <td class="m10">Classifies the rejection by a type.</td>
            <td class="m10">uint8</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m9">Message Payload</td>
            <td class="m10">MessagePayload</td>
            <td class="m10">0</td>
            <td class="m10"><abbr title="Sorry, you don't have enough tokens.">Hover for example</abbr></td>
            <td class="m10"><abbr title="Length 0-65,535 bytes. Message that explains the reasoning for a rejection, if needed.  Most rejection types will be captured by the Rejection Type Subfield.">Length 0-65,535 bytes. Message that explains the reasoning for a rejec ... Hover for more</abbr></td>
            <td class="m10">nvarchar32</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m9">Timestamp</td>
            <td class="m10">Timestamp</td>
            <td class="m10">8</td>
            <td class="m10">1551767413250187179</td>
            <td class="m10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="m10">timestamp</td>
            <td class="m10">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>

##Rejection Action Transaction Summary

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
            <td class="m5">[{Contract Contract Public Address }]</td>
            <td class="m6">.</td>
            <td class="m6">.</td>
            <td class="m10">.</td>
            <td class="m10">.</td>
            <td class="m10">.</td>
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
                <td class="m10"></td>
            </tr>
            <tr>
                <td class="m10">Push Data</td>
                <td class="m10">OpPushdata</td>
                <td class="m10">1</td>
                <td class="m10" style="word-break:break-all">77</td>
                <td class="m10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="m10">opcode</td>
                <td class="m10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="m10">Length of Action Payload</td>
                <td class="m10">LenActionPayload</td>
                <td class="m10">2</td>
                <td class="m10" style="word-break:break-all">409</td>
                <td class="m10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="m10">pushdata_length</td>
                <td class="m10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="m10">Version</td>
                <td class="m10">Version</td>
                <td class="m10">1</td>
                <td class="m10" style="word-break:break-all">0</td>
                <td class="m10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="m10">uint8</td>
                <td class="m10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="m10">Action Prefix</td>
                <td class="m10">ActionPrefix</td>
                <td class="m10">2</td>
                <td class="m10" style="word-break:break-all">C1</td>
                <td class="m10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="m10">string</td>
                <td class="m10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

