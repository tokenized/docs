
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
            <td class="t9">Asset Count</td>
            <td class="t10">AssetCount</td>
            <td class="t10">1</td>
            <td class="t10">0</td>
            <td class="t10">The number of Assets specified by the Transfer action to be settled.</td>
            <td class="t10">uint8</td>
            <td class="t10"></td>
        </tr>
        <tr>
            <td class="t9">Asset Type X</td>
            <td class="t10">AssetTypeX</td>
            <td class="t10">3</td>
            <td class="t10">RRE</td>
            <td class="t10">eg. Share, Bond, Ticket</td>
            <td class="t10">string</td>
            <td class="t10"></td>
        </tr>
        <tr>
            <td class="t9">Asset ID X</td>
            <td class="t10">AssetIDX</td>
            <td class="t10">32</td>
            <td class="t10">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="t10"><abbr title="Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans. ">Randomly generated base58 string.  Each Asset ID should be unique.  Ho ... Hover for more</abbr></td>
            <td class="t10">string</td>
            <td class="t10"></td>
        </tr>
        <tr>
            <td class="t9">Asset X Settlements Count</td>
            <td class="t10">AssetXSettlementsCount</td>
            <td class="t10">1</td>
            <td class="t10">0</td>
            <td class="t10">Number of settlements for Asset X.</td>
            <td class="t10">uint8</td>
            <td class="t10"></td>
        </tr>
        <tr>
            <td class="t5" colspan="7">
                <a href="javascript:;" data-popover="type-QuantityIndex">
                   Asset X Address X Qty - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="t9">Timestamp</td>
            <td class="t10">Timestamp</td>
            <td class="t10">8</td>
            <td class="t10">1551767413250187179</td>
            <td class="t10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="t10">timestamp</td>
            <td class="t10">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>

##Settlement Action Transaction Summary

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
            <td class="t5">[{AssetXContract Contract Public Address (Asset X) }]</td>
            <td class="t6">.</td>
            <td class="t6">.</td>
            <td class="t10">.</td>
            <td class="t10">.</td>
            <td class="t10">.</td>
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
                <td class="t10">Protocol Identifier</td>
                <td class="t10">ProtocolID</td>
                <td class="t10">13</td>
                <td class="t10" style="word-break:break-all">tokenized.com</td>
                <td class="t10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="t10">string</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Push Data</td>
                <td class="t10">OpPushdata</td>
                <td class="t10">1</td>
                <td class="t10" style="word-break:break-all">77</td>
                <td class="t10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="t10">opcode</td>
                <td class="t10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="t10">Length of Action Payload</td>
                <td class="t10">LenActionPayload</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all">409</td>
                <td class="t10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="t10">pushdata_length</td>
                <td class="t10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="t10">Version</td>
                <td class="t10">Version</td>
                <td class="t10">1</td>
                <td class="t10" style="word-break:break-all">0</td>
                <td class="t10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="t10">uint8</td>
                <td class="t10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="t10">Action Prefix</td>
                <td class="t10">ActionPrefix</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all">C1</td>
                <td class="t10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="t10">string</td>
                <td class="t10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-QuantityIndex">
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
                <td class="t10">Index</td>
                <td class="t10">Index</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all">0</td>
                <td class="t10">The index of the input sending the tokens</td>
                <td class="t10">uint16</td>
                <td class="t10"></td>
            </tr>
            <tr>
                <td class="t10">Quantity</td>
                <td class="t10">Quantity</td>
                <td class="t10">8</td>
                <td class="t10" style="word-break:break-all">100</td>
                <td class="t10">Number of tokens being sent</td>
                <td class="t10">uint64</td>
                <td class="t10"></td>
            </tr>
        </table>
    </div>
</div>

