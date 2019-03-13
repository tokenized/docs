
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
            <td class="e10">string</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Asset ID</td>
            <td class="e10">AssetID</td>
            <td class="e10">32</td>
            <td class="e10">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="e10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.</td>
            <td class="e10">string</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Compliance Action</td>
            <td class="e10">ComplianceAction</td>
            <td class="e10">1</td>
            <td class="e10">F</td>
            <td class="e10">Freeze (F), Thaw (T), Confiscate (C), Reconciliation (R)</td>
            <td class="e10">string</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Number of Target Addresses</td>
            <td class="e10">TargetAddressCount</td>
            <td class="e10">2</td>
            <td class="e10">0</td>
            <td class="e10">0 - 65,535</td>
            <td class="e10">uint16</td>
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
            <td class="e9">Deposit Address</td>
            <td class="e10">DepositAddress</td>
            <td class="e10">0</td>
            <td class="e10"><abbr title="17zAWabipcUHn5XP9w8GEc3PKvG5bYGBMe">Hover for example</abbr></td>
            <td class="e10">Length 1-255 bytes. The public address for confiscated tokens to be deposited in.  Null for Freeze, Thaw, actions. For Reconciliation actions the deposit address is who receives bitcoin.</td>
            <td class="e10">nvarchar8</td>
            <td class="e10">Eventually the supporting evidence/explanation can be supported by a Subfield that has the public address (and a signed message) owned by a legal authority for ID verification/certification purposes.</td>
        </tr>

        <tr>
            <td class="e9">Authority Name</td>
            <td class="e10">AuthorityName</td>
            <td class="e10">0</td>
            <td class="e10"><abbr title="Supreme and District Courts Brisbane">Hover for example</abbr></td>
            <td class="e10">Length 0-255 bytes. Enforcement Authority Name (eg. Issuer, Queensland Police Service, Tokenized, etc.)</td>
            <td class="e10">nvarchar8</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Signature Algorithm for Address List</td>
            <td class="e10">SigAlgoAddressList</td>
            <td class="e10">1</td>
            <td class="e10">1</td>
            <td class="e10">0 = No Registry-signed Message, 1 = ECDSA+secp256k1</td>
            <td class="e10">uint8</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Authority Public Key</td>
            <td class="e10">AuthorityPublicKey</td>
            <td class="e10">0</td>
            <td class="e10"></td>
            <td class="e10">Length 0-255 bytes. Public Key associated with the Enforcement Authority</td>
            <td class="e10">nvarchar8</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Authority Order Signature</td>
            <td class="e10">OrderSignature</td>
            <td class="e10">0</td>
            <td class="e10"></td>
            <td class="e10">Length 0-255 bytes. Signature for a message that lists out the target addresses and deposit address. Signature of (Contract Address, Asset Code, Compliance Action, Supporting Evidence Hash, Time Out Expiration, TargetAddress1, TargetAddress1Qty, TargetAddressX, TargetAddressXQty,...,DepositAddress)</td>
            <td class="e10">nvarchar8</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Supporting Evidence Hash</td>
            <td class="e10">SupportingEvidenceHash</td>
            <td class="e10">32</td>
            <td class="e10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="e10">SHA-256: warrant, court order, etc.</td>
            <td class="e10">sha256</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Ref Txn ID</td>
            <td class="e10">RefTxnID</td>
            <td class="e10">32</td>
            <td class="e10"><abbr title="f3318be9fb3f73e53b29868beae46b42911c2116f979a5d3284face90746cb37">Hover for example</abbr></td>
            <td class="e10">The settlement action that was dropped from the network.  Not applicable for Freeze, Thaw, and Confiscation orders.  Only applicable for reconcilliation actions.  No subfield when F, T, R is selected as the Compliance Action subfield.</td>
            <td class="e10">sha256</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Freeze Period</td>
            <td class="e10">FreezePeriod</td>
            <td class="e10">8</td>
            <td class="e10"><abbr title="Tue Oct 09 2018 05:00:00 GMT+1000 (AEST)">Hover for example</abbr></td>
            <td class="e10">Used for a 'time out'.  Tokens are automatically unfrozen after the expiration timestamp without requiring a Thaw Action. Null value for Thaw, Confiscation and Reconciallitaion orders.</td>
            <td class="e10">time</td>
            <td class="e10"></td>
        </tr>

        <tr>
            <td class="e9">Message Period</td>
            <td class="e10">Message</td>
            <td class="e10">0</td>
            <td class="e10"><abbr title="Sorry, but the court order made me.">Hover for example</abbr></td>
            <td class="e10"></td>
            <td class="e10">nvarchar32</td>
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
            <td class="e5">.</td>
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
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
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
                <td class="e10" style="word-break:break-all">C1</td>
                <td class="e10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="e10">string</td>
                <td class="e10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-TargetAddress">
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
                <td class="e10">Address</td>
                <td class="e10">Address</td>
                <td class="e10">34</td>
                <td class="e10" style="word-break:break-all">1HQ2ULuD7T5ykaucZ3KmTo4i29925Qa6ic</td>
                <td class="e10">Public address where the token balance will be changed.</td>
                <td class="e10">string</td>
                <td class="e10"></td>
            </tr>
            <tr>
                <td class="e10">Quantity</td>
                <td class="e10">Quantity</td>
                <td class="e10">8</td>
                <td class="e10" style="word-break:break-all">10000</td>
                <td class="e10">Qty of tokens to be frozen, thawed, confiscated or reconciled. For Contract-wide freezes 0 will be used.</td>
                <td class="e10">uint64</td>
                <td class="e10"></td>
            </tr>
        </table>
    </div>
</div>

