


# Order Action

Order Action -  Issuer to signal to the smart contract that the tokens that a particular public address(es) owns are to be confiscated, frozen, thawed or reconciled.

The following breaks down the construction of a Order Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="e9">Compliance Action</td>
            <td class="e10">ComplianceAction</td>
            <td class="e10">1</td>
            <td class="e10">F</td>
            <td class="e10">Freeze (F), Thaw (T), Confiscate (C), Reconciliation (R)</td>
            <td class="e10">fixedchar</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-TargetAddress">
                   Target Addresses - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-PublicKeyHash">
                   Deposit Address - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Authority Name</td>
            <td class="e10">AuthorityName</td>
            <td class="e10">8</td>
            <td class="e10"><abbr title="Supreme and District Courts Brisbane">Hover for example</abbr></td>
            <td class="e10"><abbr title="Length 0-255 bytes. Enforcement Authority Name (eg. Issuer, Queensland Police Service, Tokenized, etc.)">Length 0-255 bytes. Enforcement Authority Name (eg. Issuer, Queensland Police Service, Tok ...</abbr></td>
            <td class="e10">varchar</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Signature Algorithm for Address List</td>
            <td class="e10">SigAlgoAddressList</td>
            <td class="e10">1</td>
            <td class="e10">1</td>
            <td class="e10">0 = No Registry-signed Message, 1 = ECDSA+secp256k1</td>
            <td class="e10">uint</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Authority Public Key</td>
            <td class="e10">AuthorityPublicKey</td>
            <td class="e10">8</td>
            <td class="e10"></td>
            <td class="e10">Length 0-255 bytes. Public Key associated with the Enforcement Authority</td>
            <td class="e10">varchar</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Authority Order Signature</td>
            <td class="e10">OrderSignature</td>
            <td class="e10">8</td>
            <td class="e10"></td>
            <td class="e10"><abbr title="Length 0-255 bytes. Signature for a message that lists out the target addresses and deposit address. Signature of (Contract Address, Asset Code, Compliance Action, Supporting Evidence Hash, Time Out Expiration, TargetAddress1, TargetAddress1Qty, TargetAddressX, TargetAddressXQty,...,DepositAddress)">Length 0-255 bytes. Signature for a message that lists out the target addresses and deposi ...</abbr></td>
            <td class="e10">varchar</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Supporting Evidence Hash - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Ref Txn ID - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Freeze Period - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Message Period</td>
            <td class="e10">Message</td>
            <td class="e10">32</td>
            <td class="e10"><abbr title="Sorry, but the court order made me.">Hover for example</abbr></td>
            <td class="e10"></td>
            <td class="e10">varchar</td>
            <td class="e10"></td>
        </tr>
    </table>
</div>

##Order Action Transaction Summary

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
            <td class="e5">0</td>
            <td class="e6">Issuer's Public Address</td>
            <td class="e6"></td>
            <td class="e10">0</td>
            <td class="e10">Contract Public Address</td>
            <td class="e10"></td>
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

<div class="ui modal" id="type-TargetAddress">
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
                <td class="e10">0</td>
                <td class="e10" style="word-break:break-all"></td>
                <td class="e10">Public address where the token balance will be changed.</td>
                <td class="e10">PublicKeyHash</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Quantity</td>
                <td class="e10">Quantity</td>
                <td class="e10">8</td>
                <td class="e10" style="word-break:break-all">10000</td>
                <td class="e10">Qty of tokens to be frozen, thawed, confiscated or reconciled. For Contract-wide freezes 0 will be used.</td>
                <td class="e10">uint</td>
                <td class="e10"></td>
            </tr>
        </table>
    </div>
</div>

