


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
            <td class="e9">Asset Type</td>
            <td class="e10">AssetType</td>
            <td class="e10">3</td>
            <td class="e10">SHC</td>
            <td class="e10">eg. Share, Bond, Ticket</td>
            <td class="e10">fixedchar</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-AssetCode">
                   Asset Code - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-QuantityIndex">
                   Quantities - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Deposit Qty</td>
            <td class="e10">DepositQty</td>
            <td class="e10">8</td>
            <td class="e10">10000</td>
            <td class="e10">Deposit address's token balance after confiscation.</td>
            <td class="e10">uint</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
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
            <td class="e5">0</td>
            <td class="e6">Contract Public Address</td>
            <td class="e6"></td>
            <td class="e10">0</td>
            <td class="e10">Target Public Address X</td>
            <td class="e10">Can be the Contract Address for a 'Contract-wide' Confiscation.</td>
        </tr>

       <tr>
            <td class="e5"></td>
            <td class="e6"></td>
            <td class="e6"></td>
            <td class="e10">1</td>
            <td class="e10">Deposit Public Address</td>
            <td class="e10">Dust limit rule minimum value output of 546</td>
        </tr>

       <tr>
            <td class="e5"></td>
            <td class="e6"></td>
            <td class="e6"></td>
            <td class="e10">2</td>
            <td class="e10">Contract Public Address</td>
            <td class="e10">Change</td>
        </tr>

       <tr>
            <td class="e5"></td>
            <td class="e6"></td>
            <td class="e6"></td>
            <td class="e10">3</td>
            <td class="e10">Contract Fee Public Address</td>
            <td class="e10">Contract fee if applicable</td>
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
                <td class="e10">tokenized.com</td>
                <td class="e10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="e10">byte</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Push Data</td>
                <td class="e10">OpPushdata</td>
                <td class="e10">1</td>
                <td class="e10">0x4d</td>
                <td class="e10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="e10">byte</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Length of Action Payload</td>
                <td class="e10">LenActionPayload</td>
                <td class="e10"></td>
                <td class="e10">tokenized.com</td>
                <td class="e10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="e10">byte</td>
                <td class="e10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="e10">Version</td>
                <td class="e10">Version</td>
                <td class="e10">1</td>
                <td class="e10">0</td>
                <td class="e10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="e10">uint8</td>
                <td class="e10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="e10">Action Prefix</td>
                <td class="e10">ActionPrefix</td>
                <td class="e10">2</td>
                <td class="e10">E4</td>
                <td class="e10" style="word-break:break-all">// E4 identifies data as a Confiscation message.</td>
                <td class="e10">string</td>
                <td class="e10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
<div class="ui modal" id="type-QuantityIndex">
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
                <td class="e10">Index</td>
                <td class="e10">Index</td>
                <td class="e10">2</td>
                <td class="e10" style="word-break:break-all">0</td>
                <td class="e10">The index of the input sending the tokens</td>
                <td class="e10">uint</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Quantity</td>
                <td class="e10">Quantity</td>
                <td class="e10">8</td>
                <td class="e10" style="word-break:break-all">100</td>
                <td class="e10">Number of tokens being sent</td>
                <td class="e10">uint</td>
                <td class="e10"></td>
            </tr>
        </table>
    </div>
</div>

