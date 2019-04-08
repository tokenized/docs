


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
            <td class="e9">Compliance Action</td>
            <td class="e10">ComplianceAction</td>
            <td class="e10">1</td>
            <td class="e10">F</td>
            <td class="e10">Freeze (F), Thaw (T), Confiscate (C), Reconcile (R)</td>
            <td class="e10">fixedchar</td>
            <td class="e10"></td>
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
                <a href="javascript:;" data-popover="type-TargetAddress">
                   Target Addresses - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Freeze Tx Id - Click to show content
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
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-PublicKeyHash">
                   Deposit Address - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Authority Included</td>
            <td class="e10">AuthorityIncluded</td>
            <td class="e10">0</td>
            <td class="e10"></td>
            <td class="e10"><abbr title="Specifies if an authority signature is included. For Reconcialitaion actions all authority signature related fields are skipped during serialization.">Specifies if an authority signature is included. For Reconcialitaion actions all authority ...</abbr></td>
            <td class="e10">bool</td>
            <td class="e10"></td>
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
            <td class="e9">Authority Public Key</td>
            <td class="e10">AuthorityPublicKey</td>
            <td class="e10">8</td>
            <td class="e10"></td>
            <td class="e10">Length 0-255 bytes. Public Key associated with the Enforcement Authority</td>
            <td class="e10">varbin</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Signature Algorithm</td>
            <td class="e10">SignatureAlgorithm</td>
            <td class="e10">1</td>
            <td class="e10">1</td>
            <td class="e10">Algorithm used for order signature. Only valid value is currently 1 = ECDSA+secp256k1</td>
            <td class="e10">uint</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Authority Order Signature</td>
            <td class="e10">OrderSignature</td>
            <td class="e10">8</td>
            <td class="e10"></td>
            <td class="e10"><abbr title="Length 0-255 bytes. Signature for a message that lists out the target addresses and deposit address. Signature of (Contract PKH, Compliance Action, Authority Name, Asset Code, Supporting Evidence Hash, FreezePeriod, TargetAddresses, and DepositAddress)">Length 0-255 bytes. Signature for a message that lists out the target addresses and deposi ...</abbr></td>
            <td class="e10">varbin</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Supporting Evidence Hash</td>
            <td class="e10">SupportingEvidenceHash</td>
            <td class="e10">32</td>
            <td class="e10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="e10">SHA-256: warrant, court order, etc.</td>
            <td class="e10">bin</td>
            <td class="e10"></td>
        </tr>
        <tr>
            <td class="e9">Ref Txs</td>
            <td class="e10">RefTxs</td>
            <td class="e10">32</td>
            <td class="e10"></td>
            <td class="e10"><abbr title="The request/response actions that were dropped.  The entire txn for both actions is included as evidence that the actions were accepted into the mempool at one point and that the senders (token/Bitcoin) signed their intent to transfer.  The management of this record keeping is off-chain and managed by the issuer or operator to preserve the integrity of the state of the tokens. Only applicable for reconcilliation actions.  No subfield when F, T, R is selected as the Compliance Action subfield.">The request/response actions that were dropped.  The entire txn for both actions is includ ...</abbr></td>
            <td class="e10">varbin</td>
            <td class="e10">Can be null.  Dropped actions that require a reconciliation action to fix the break in the chain are considered to be an extremely rare event.</td>
        </tr>
        <tr>
            <td class="e5" colspan="7">
                <a href="javascript:;" data-popover="type-QuantityIndex">
                   Bitcoin Dispersions - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="e9">Message</td>
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
            <td class="e6">Issuer's Public Address</td>
            <td class="e6"></td>
            <td class="e10">0</td>
            <td class="e10">Contract Public Address</td>
            <td class="e10">Contract fee and funding for response tx</td>
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
                <td class="e10">E1</td>
                <td class="e10" style="word-break:break-all">// E1 identifies data as a Order message.</td>
                <td class="e10">string</td>
                <td class="e10">Cannot be changed by issuer, operator or smart contract..</td>
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

