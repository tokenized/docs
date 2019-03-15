


# Addition Action

Addition Action -  Adds an entry to the Register.

The following breaks down the construction of a Addition Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="r5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="r9">Message</td>
            <td class="r10">Message</td>
            <td class="r10">0</td>
            <td class="r10">username</td>
            <td class="r10"></td>
            <td class="r10">nvarchar32</td>
            <td class="r10"></td>
        </tr>
    </table>
</div>

##Addition Action Transaction Summary

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
            <td class="r5">0</td>
            <td class="r6">Register's Public Address</td>
            <td class="r6"></td>
            <td class="r10">0</td>
            <td class="r10">Register's Public Address</td>
            <td class="r10"></td>
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
                <td class="r10">Protocol Identifier</td>
                <td class="r10">ProtocolID</td>
                <td class="r10">13</td>
                <td class="r10" style="word-break:break-all">tokenized.com</td>
                <td class="r10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="r10">string</td>
                <td class="r10"></td>
            </tr>
            <tr>
                <td class="r10">Push Data</td>
                <td class="r10">OpPushdata</td>
                <td class="r10">1</td>
                <td class="r10" style="word-break:break-all">77</td>
                <td class="r10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="r10">opcode</td>
                <td class="r10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="r10">Length of Action Payload</td>
                <td class="r10">LenActionPayload</td>
                <td class="r10">2</td>
                <td class="r10" style="word-break:break-all">409</td>
                <td class="r10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="r10">pushdata_length</td>
                <td class="r10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="r10">Version</td>
                <td class="r10">Version</td>
                <td class="r10">1</td>
                <td class="r10" style="word-break:break-all">0</td>
                <td class="r10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="r10">uint8</td>
                <td class="r10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="r10">Action Prefix</td>
                <td class="r10">ActionPrefix</td>
                <td class="r10">2</td>
                <td class="r10" style="word-break:break-all">R2</td>
                <td class="r10">// R2 identifies data as a Addition message.</td>
                <td class="r10">string</td>
                <td class="r10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

