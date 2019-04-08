


# Transfer Action

A Token Owner(s) Sends, Exchanges or Swaps a token(s) or Bitcoin for a token(s) or Bitcoin.  Can be as simple as sending a single token to a receiver.  Or can be as complex as many senders sending many different assets - controlled by many different smart contracts - to a number of receivers.  This action also supports atomic swaps (tokens for tokens).  Since many parties and contracts can be involved in a transfer and the corresponding settlement action, the partially signed T1 and T2 actions will need to be passed around on-chain with an M1 action, or off-chain.

The following breaks down the construction of a Transfer Action. The action is constructed by building a single string from each of the elements in order.

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
                <a href="javascript:;" data-popover="type-AssetTransfer">
                   Assets - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Offer Expiry - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="t9">Exchange Fee</td>
            <td class="t10">ExchangeFee</td>
            <td class="t10">8</td>
            <td class="t10">0.01</td>
            <td class="t10">Fixed amount of bitcoin being paid to an exchange for facilitating a transfer.</td>
            <td class="t10">uint</td>
            <td class="t10"></td>
        </tr>
        <tr>
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-PublicKeyHash">
                   Exchange Fee Address - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Transfer Action Transaction Summary

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
            <td class="t5">0</td>
            <td class="t6">Asset (token) Sending Public Address. Assets[i].AssetSenders[j].Index references these inputs.</td>
            <td class="t6"></td>
            <td class="t10">0</td>
            <td class="t10">Contract Public Address for Asset X</td>
            <td class="t10">Enough for the costs of the responding action, including any bitcoins being transfered, and the Contract Fee.</td>
        </tr>

       <tr>
            <td class="t5"></td>
            <td class="t6"></td>
            <td class="t6"></td>
            <td class="t10">1</td>
            <td class="t10">Asset (token) Receiving Public Address X</td>
            <td class="t10">Token Output Address X (Token Receiver).</td>
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
                <td class="t10">Protocol Identifier</td>
                <td class="t10">ProtocolID</td>
                <td class="t10">13</td>
                <td class="t10">tokenized.com</td>
                <td class="t10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="t10">byte</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Push Data</td>
                <td class="t10">OpPushdata</td>
                <td class="t10">1</td>
                <td class="t10">0x4d</td>
                <td class="t10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="t10">byte</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Length of Action Payload</td>
                <td class="t10">LenActionPayload</td>
                <td class="t10"></td>
                <td class="t10">tokenized.com</td>
                <td class="t10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="t10">byte</td>
                <td class="t10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="t10">Version</td>
                <td class="t10">Version</td>
                <td class="t10">1</td>
                <td class="t10">0</td>
                <td class="t10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="t10">uint8</td>
                <td class="t10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="t10">Action Prefix</td>
                <td class="t10">ActionPrefix</td>
                <td class="t10">2</td>
                <td class="t10">T1</td>
                <td class="t10" style="word-break:break-all">// T1 identifies data as a Transfer message.</td>
                <td class="t10">string</td>
                <td class="t10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
<div class="ui modal" id="type-AssetTransfer">
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
                <td class="t10">Index of output containing the contract's address for this offset</td>
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
                <td class="t10">Asset Senders</td>
                <td class="t10">AssetSenders</td>
                <td class="t10">0</td>
                <td class="t10" style="word-break:break-all"></td>
                <td class="t10">Each element has the value of tokens to be spent from the input address, which is referred to by the index.</td>
                <td class="t10">QuantityIndex[]</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Token Receivers</td>
                <td class="t10">AssetReceivers</td>
                <td class="t10">0</td>
                <td class="t10" style="word-break:break-all"></td>
                <td class="t10">Each element has the value of tokens to be received by the output address, which is referred to by the index.</td>
                <td class="t10">TokenReceiver[]</td>
                <td class="t10"></td>
            </tr>
        </table>
    </div>
</div>

