


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
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-PublicKeyHash">
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

## Confiscation Action Transaction Summary

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

