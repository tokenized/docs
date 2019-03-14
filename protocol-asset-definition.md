


# Asset Definition Action

Asset Definition Action -  This action is used by the issuer to define the properties/characteristics of the Asset (token) that it wants to create.

The following breaks down the construction of a Asset Definition Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="a9">Asset Type</td>
            <td class="a10">AssetType</td>
            <td class="a10">3</td>
            <td class="a10">COU</td>
            <td class="a10">eg. Share - Common</td>
            <td class="a10">string</td>
            <td class="a10">Cannot be changed by issuer, operator or smart contract.</td>
        </tr>
        <tr>
            <td class="a9">Asset ID</td>
            <td class="a10">AssetID</td>
            <td class="a10">32</td>
            <td class="a10">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="a10"><abbr title="Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type + Asset ID = Asset Code.  An Asset Code is a human readable idenitfier that can be used in a similar way to a Bitcoin (BSV) address, a vanity identifying label.">Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID i ...</abbr></td>
            <td class="a10">string</td>
            <td class="a10">Cannot be changed by issuer, operator or smart contract.</td>
        </tr>
        <tr>
            <td class="a9">Asset Authorization Flags</td>
            <td class="a10">AssetAuthFlags</td>
            <td class="a10">8</td>
            <td class="a10"><abbr title="0000000000000000000000000000000000000000000000000001000110111111">Hover for example</abbr></td>
            <td class="a10">Authorization Flags,  bitwise operation</td>
            <td class="a10">bin</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Transfers Permitted</td>
            <td class="a10">TransfersPermitted</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10">1 = Transfers are permitted.  0 = Transfers are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Trade Restrictions</td>
            <td class="a10">TradeRestrictions</td>
            <td class="a10">3</td>
            <td class="a10">GBR</td>
            <td class="a10"><abbr title="Asset can only be traded within the trade restrictions.  Eg. AUS - Australian residents only.  EU - European Union residents only.">Asset can only be traded within the trade restrictions.  Eg. AUS - Australian residents on ...</abbr></td>
            <td class="a10">string</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Enforcement Orders Permitted</td>
            <td class="a10">EnforcementOrdersPermitted</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10">1 = Enforcement Orders are permitted. 0 = Enforcement Orders are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Vote Multiplier</td>
            <td class="a10">VoteMultiplier</td>
            <td class="a10">1</td>
            <td class="a10">3</td>
            <td class="a10"><abbr title="Multiplies the vote by the integer. 1 token = 1 vote with a 1 for vote multipler (normal).  1 token = 3 votes with a multiplier of 3, for example.">Multiplies the vote by the integer. 1 token = 1 vote with a 1 for vote multipler (normal). ...</abbr></td>
            <td class="a10">uint8</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Referendum Proposal</td>
            <td class="a10">ReferendumProposal</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10"><abbr title="A Referendum is permitted for Asset-Wide Proposals (outside of smart contract scope) if also permitted by the contract. If the contract has proposals by referendum restricted, then this flag is meaningless.">A Referendum is permitted for Asset-Wide Proposals (outside of smart contract scope) if al ...</abbr></td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Initiative Proposal</td>
            <td class="a10">InitiativeProposal</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10"><abbr title="An initiative is permitted for Asset-Wide Proposals (outside of smart contract scope) if also permitted by the contract. If the contract has proposals by initiative restricted, then this flag is meaningless.">An initiative is permitted for Asset-Wide Proposals (outside of smart contract scope) if a ...</abbr></td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Modification Governance</td>
            <td class="a10">AssetModificationGovernance</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10"><abbr title="1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the asset auth flags, then the vote will either be a contract-wide vote (all assets vote on the referendum/initiative) or an asset-wide vote (all assets vote on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.">1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or  ...</abbr></td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Qty of Tokens</td>
            <td class="a10">TokenQty</td>
            <td class="a10">8</td>
            <td class="a10">1000000</td>
            <td class="a10"><abbr title="Quantity of token - 0 is valid. Fungible 'shares' of the Asset. 1 is used for non-fungible tokens.  Asset IDs become the non-fungible Asset ID and many Asset IDs can be associated with a particular Contract.">Quantity of token - 0 is valid. Fungible 'shares' of the Asset. 1 is used for non-fungible ...</abbr></td>
            <td class="a10">uint64</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Contract Fee Currency</td>
            <td class="a10">ContractFeeCurrency</td>
            <td class="a10">3</td>
            <td class="a10">AUD</td>
            <td class="a10">BSV, USD, AUD, EUR, etc.</td>
            <td class="a10">string</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Contract Fee Var</td>
            <td class="a10">ContractFeeVar</td>
            <td class="a10">4</td>
            <td class="a10">0.005</td>
            <td class="a10">Percent of the value of the transaction</td>
            <td class="a10">float32</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Contract Fee Fixed</td>
            <td class="a10">ContractFeeFixed</td>
            <td class="a10">4</td>
            <td class="a10">0.01</td>
            <td class="a10">Fixed fee (payment made in BSV)</td>
            <td class="a10">float32</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Payload Length</td>
            <td class="a10">AssetPayloadLen</td>
            <td class="a10">2</td>
            <td class="a10">9</td>
            <td class="a10">Size of the asset payload in bytes.</td>
            <td class="a10">uint16</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Payload</td>
            <td class="a10">AssetPayload</td>
            <td class="a10">0</td>
            <td class="a10">some data</td>
            <td class="a10"><abbr title="Payload length is dependent on the asset type. Each asset is made up of a defined set of information pertaining to the specific asset type, and may contain fields of variable length type (nvarchar8, 16, 32)">Payload length is dependent on the asset type. Each asset is made up of a defined set of i ...</abbr></td>
            <td class="a10">byte[]</td>
            <td class="a10"></td>
        </tr>
    </table>
</div>

##Asset Definition Action Transaction Summary

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
            <td class="a5">[{Issuer Issuer's Public Address }]</td>
            <td class="a6">.</td>
            <td class="a6">.</td>
            <td class="a10">.</td>
            <td class="a10">.</td>
            <td class="a10">.</td>
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
                <td class="a10">Protocol Identifier</td>
                <td class="a10">ProtocolID</td>
                <td class="a10">13</td>
                <td class="a10" style="word-break:break-all">tokenized.com</td>
                <td class="a10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="a10">string</td>
                <td class="a10"></td>
            </tr>
            <tr>
                <td class="a10">Push Data</td>
                <td class="a10">OpPushdata</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">77</td>
                <td class="a10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="a10">opcode</td>
                <td class="a10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="a10">Length of Action Payload</td>
                <td class="a10">LenActionPayload</td>
                <td class="a10">2</td>
                <td class="a10" style="word-break:break-all">409</td>
                <td class="a10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="a10">pushdata_length</td>
                <td class="a10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="a10">Version</td>
                <td class="a10">Version</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">0</td>
                <td class="a10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="a10">uint8</td>
                <td class="a10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="a10">Action Prefix</td>
                <td class="a10">ActionPrefix</td>
                <td class="a10">2</td>
                <td class="a10" style="word-break:break-all">A1</td>
                <td class="a10">// A1 identifies data as a AssetDefinition message.</td>
                <td class="a10">string</td>
                <td class="a10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

