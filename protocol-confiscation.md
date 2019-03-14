


# Confiscation Action

Confiscation Action -  to be used to comply with contractual obligations, legal and/or issuer requirements.

The following breaks down the construction of a Confiscation Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="e9">Number of Addresses</td>
            <td class="e10">AddressCount</td>
            <td class="e10">2</td>
            <td class="e10">0</td>
            <td class="e10">0 - 65,535</td>
            <td class="e10">uint16</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-Address">
                   Addresses - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Deposit Qty</td>
            <td class="e10">DepositQty</td>
            <td class="e10">8</td>
            <td class="e10">10000</td>
            <td class="e10">Custodian's token balance after confiscation.</td>
            <td class="e10">uint64</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Timestamp</td>
            <td class="e10">Timestamp</td>
            <td class="e10">8</td>
            <td class="e10">1551767413250187179</td>
            <td class="e10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="e10">timestamp</td>
            <td class="e10">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>

##Confiscation Action Transaction Summary

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
            <td class="e5">[{Contract Contract Public Address }]</td>
            <td class="e6">.</td>
            <td class="e6">.</td>
            <td class="e10">.</td>
            <td class="e10">.</td>
            <td class="e10">.</td>
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
                <td class="e10">Protocol Identifier</td>
                <td class="e10">ProtocolID</td>
                <td class="e10">13</td>
                <td class="e10" style="word-break:break-all">tokenized.com</td>
                <td class="e10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="e10">string</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Push Data</td>
                <td class="e10">OpPushdata</td>
                <td class="e10">1</td>
                <td class="e10" style="word-break:break-all">77</td>
                <td class="e10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="e10">opcode</td>
                <td class="e10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="e10">Length of Action Payload</td>
                <td class="e10">LenActionPayload</td>
                <td class="e10">2</td>
                <td class="e10" style="word-break:break-all">409</td>
                <td class="e10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="e10">pushdata_length</td>
                <td class="e10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="e10">Version</td>
                <td class="e10">Version</td>
                <td class="e10">1</td>
                <td class="e10" style="word-break:break-all">0</td>
                <td class="e10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="e10">uint8</td>
                <td class="e10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="e10">Action Prefix</td>
                <td class="e10">ActionPrefix</td>
                <td class="e10">2</td>
                <td class="e10" style="word-break:break-all">E4</td>
                <td class="e10">// E4 identifies data as a Confiscation message.</td>
                <td class="e10">string</td>
                <td class="e10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Address">
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
                <td class="e10">Address</td>
                <td class="e10">Address</td>
                <td class="e10">34</td>
                <td class="e10" style="word-break:break-all">1HQ2ULuD7T5ykaucZ3KmTo4i29925Qa6ic</td>
                <td class="e10">Public address where the token balance will be changed.</td>
                <td class="e10">string</td>
                <td class="e10"></td>
            </tr>
        </table>
    </div>
</div>

