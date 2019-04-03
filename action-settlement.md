


# Settlement Action

Settlement Action -  Settles the transfer request of bitcoins and tokens from transfer (T1) actions.

The following breaks down the construction of a Settlement Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-AssetSettlement">
                   Assets - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Settlement Action Transaction Summary

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
            <td class="t5">0</td>
            <td class="t6">Contract Public Address (Asset X)</td>
            <td class="t6">Contract (Asset X) in response to a transfer action with Asset X being sent to another address(es).</td>
            <td class="t10">0</td>
            <td class="t10">Asset 1 Settlement Address X</td>
            <td class="t10">Address X that is being settled for Asset 1.</td>
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

<div class="ui modal" id="type-AssetSettlement">
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
                <td class="t10">Contract Index</td>
                <td class="t10">ContractIndex</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all"></td>
                <td class="t10">Index of input containing the contract's address for this offset</td>
                <td class="t10">uint</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Asset Type</td>
                <td class="t10">AssetType</td>
                <td class="t10">3</td>
                <td class="t10" style="word-break:break-all">SHC</td>
                <td class="t10">eg. Share, Bond, Ticket. All characters must be capitalised.</td>
                <td class="t10">fixedchar</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Asset Code</td>
                <td class="t10">AssetCode</td>
                <td class="t10">0</td>
                <td class="t10" style="word-break:break-all"></td>
                <td class="t10">32 randomly generated bytes.  Each Asset Code should be unique.  However, an Asset Code is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type + Asset Code = Asset Code.  An Asset Code is a human readable identifier that can be used in a similar way to a Bitcoin (BSV) address.</td>
                <td class="t10">AssetCode</td>
                <td class="t10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="t10">Settlements[]</td>
                <td class="t10">Settlements</td>
                <td class="t10">0</td>
                <td class="t10" style="word-break:break-all"></td>
                <td class="t10">Each element contains the resulting token balance of Asset X for the output Address, which is referred to by the index.</td>
                <td class="t10">QuantityIndex[]</td>
                <td class="t10"></td>
            </tr>
        </table>
    </div>
</div>

