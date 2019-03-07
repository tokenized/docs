
#Contract Amendment Action

<div class="ui modal" id="header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr>
                <td class="c6">Header[]</td>
                <td class="c6">Header Array</td>
                <td class="c6">-</td>
                <td class="c6">-</td>
                <td class="c6">Common header data for all messages</td>
                <td class="c6">Header</td>
                <td class="c7"></td>
            </tr>
        </table>
    </div>
</div>

Contract Amendment Action -  the issuer can initiate an amendment to the contract establishment metadata.  This can be due to a change of name, change of contract terms, change of authorizations, or change of the URI.  The ability to make an amendment to the contract is limited by the Authorization Flag set on the previous Contract Formation action.  The Authorization Flags can be set to allow Contract Amendments, but only if a Token Owner vote has passed in favour of making the Amendment. Contract revision/protocol identifier and action prefix can't be amended.  The rest of the fields are open to change.  However, the Issuer is responsible for acting lawfully (in their jurisdiction) and in accordance with the terms of the Investment Contract.

The following breaks down the construction of a Contract Amendment Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="c6" colspan="7"><a href="#" data-popover="header">Header[] - Click to show content</a></td>
        </tr>
        <tr>
            <td class="c10">Text Encoding</td>
            <td class="c10">TextEncoding</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="c10">uint8</td>
            <td class="c11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr>
            <td class="c10">Change Issuer Address</td>
            <td class="c10">ChangeIssuerAddress</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">1 - Yes, 0 - No.  Used to change the issuer address.  The new issuer address must be in the input[1] position.</td>
            <td class="c10">bool</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Change Operator Address</td>
            <td class="c10">ChangeOperatorAddress</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">1 - Yes, 0 - No.  Used to change the smart contract operator address.  The new operator address must be in the input[1] position.</td>
            <td class="c10">bool</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">2</td>
            <td class="c10" style="word-break:break-all">42</td>
            <td class="c10">Counter 0 - 65,535</td>
            <td class="c10">uint16</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">AmendmentsCount</td>
            <td class="c10">AmendmentsCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of Amendments. Must be less than the max Subfield Index of CF.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Amendments</td>
            <td class="c10">Amendments</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10"></td>
            <td class="c10">Amendment[]</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Ref Tx-ID</td>
            <td class="c10">RefTxID</td>
            <td class="c10">32</td>
            <td class="c10" style="word-break:break-all">a8700385d4cc62628cc34629862121f84e6237689de8e45e151dcbc8cf30b33d</td>
            <td class="c10">Tx-ID of the associated Result action (governance) that permitted the modifications.</td>
            <td class="c10">SHA256</td>
            <td class="c11"></td>
        </tr>
    </table>
</div>