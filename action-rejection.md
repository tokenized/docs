


# Rejection Action

Rejection Action - used to reject request actions that do not comply with the rules of the protocol or terms and conditions or state of the contract. If money is to be returned to a user then it is used in lieu of the Settlement action to properly account for token balances. All issuer/user request actions must be responded to by the smart contract with an action.  The only exception to this rule is when there is not enough fees in the first action for the smart contract to respond and remain revenue neutral.  If not enough fees are attached to pay for the smart contract response then the smart contract will not respond.

The following breaks down the construction of a Rejection action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="m10">uint</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m9">Message Payload</td>
            <td class="m10">MessagePayload</td>
            <td class="m10">32</td>
            <td class="m10"><abbr title="Sorry, you don't have enough tokens.">Hover for example</abbr></td>
            <td class="m10"><abbr title="Length 0-65,535 bytes. Message that explains the reasoning for a rejection, if needed.  Most rejection types will be captured by the Rejection Type Subfield.">Length 0-65,535 bytes. Message that explains the reasoning for a rejection, if needed.  Mo ...</abbr></td>
            <td class="m10">varchar</td>
            <td class="m10"></td>
        </tr>
        <tr>
            <td class="m5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

## Rejection Action Transaction Summary

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th class="s0" colspan="6">smart contract Operator Fee: 0</th>
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
            <td class="m6">Contract Public Address</td>
            <td class="m6"></td>
            <td class="m10">0</td>
            <td class="m10">User's Public Address</td>
            <td class="m10">Return the money less fees</td>
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
        </table>
    </div>
</div>

