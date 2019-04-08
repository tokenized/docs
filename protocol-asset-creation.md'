


# Asset Creation Action

Asset Creation Action -  This action creates an Asset in response to the Issuer's instructions in the Definition Action.

The following breaks down the construction of a Asset Creation Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="a10">SHC</td>
            <td class="a10">eg. Share - Common</td>
            <td class="a10">fixedchar</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-AssetCode">
                   Asset Code - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="a9">Asset Authorization Flags</td>
            <td class="a10">AssetAuthFlags</td>
            <td class="a10">8</td>
            <td class="a10"><abbr title="0000000000000000000000000000000000000000000000000001000110111111">Hover for example</abbr></td>
            <td class="a10">Authorization Flags,  bitwise operation</td>
            <td class="a10">varbin</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Transfers Permitted</td>
            <td class="a10">TransfersPermitted</td>
            <td class="a10">0</td>
            <td class="a10">1</td>
            <td class="a10">1 = Transfers are permitted.  0 = Transfers are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-Polity">
                   Trade Restrictions - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="a9">Enforcement Orders Permitted</td>
            <td class="a10">EnforcementOrdersPermitted</td>
            <td class="a10">0</td>
            <td class="a10">1</td>
            <td class="a10">1 = Enforcement Orders are permitted. 0 = Enforcement Orders are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Voting Rights</td>
            <td class="a10">VotingRights</td>
            <td class="a10">0</td>
            <td class="a10"></td>
            <td class="a10"><abbr title="When false holders of this asset will not be able to vote for tokens of this asset even on voting systems in which vote multiplers are not permitted.">When false holders of this asset will not be able to vote for tokens of this asset even on ...</abbr></td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Vote Multiplier</td>
            <td class="a10">VoteMultiplier</td>
            <td class="a10">1</td>
            <td class="a10">3</td>
            <td class="a10"><abbr title="Multiplies the vote by the integer. 1 token = 1 vote with a 1 for vote multipler (normal).  1 token = 3 votes with a multiplier of 3, for example.">Multiplies the vote by the integer. 1 token = 1 vote with a 1 for vote multipler (normal). ...</abbr></td>
            <td class="a10">uint</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Issuer Proposal</td>
            <td class="a10">IssuerProposal</td>
            <td class="a10">0</td>
            <td class="a10">true</td>
            <td class="a10">An Issuer is permitted to make proposals (outside of smart contract scope).</td>
            <td class="a10">bool</td>
            <td class="a10">General Governance</td>
        </tr>
        <tr>
            <td class="a9">Holder Proposal</td>
            <td class="a10">HolderProposal</td>
            <td class="a10">0</td>
            <td class="a10">true</td>
            <td class="a10">A holder is permitted to make proposals (outside of smart contract scope).</td>
            <td class="a10">bool</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Modification Governance</td>
            <td class="a10">AssetModificationGovernance</td>
            <td class="a10">1</td>
            <td class="a10">1</td>
            <td class="a10"><abbr title="1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the asset auth flags, then the vote will either be a contract-wide vote (all assets vote on the referendum/initiative) or an asset-wide vote (only this asset votes on the referendum/initiative) depending on the value in this subfield.  The voting system specifies the voting rules.">1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or  ...</abbr></td>
            <td class="a10">uint</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Qty of Tokens</td>
            <td class="a10">TokenQty</td>
            <td class="a10">8</td>
            <td class="a10">1000000</td>
            <td class="a10"><abbr title="Quantity of token - 0 is valid. Fungible 'shares' of the Asset. 1 is used for non-fungible tokens.  Asset Codes become the non-fungible Asset Code and many Asset Codes can be associated with a particular Contract.">Quantity of token - 0 is valid. Fungible 'shares' of the Asset. 1 is used for non-fungible ...</abbr></td>
            <td class="a10">uint</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Payload</td>
            <td class="a10">AssetPayload</td>
            <td class="a10">16</td>
            <td class="a10">some data</td>
            <td class="a10"><abbr title="Payload length is dependent on the asset type. Each asset is made up of a defined set of information pertaining to the specific asset type, and may contain fields of variable length type (nvarchar8, 16, 32)">Payload length is dependent on the asset type. Each asset is made up of a defined set of i ...</abbr></td>
            <td class="a10">varbin</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a9">Asset Revision</td>
            <td class="a10">Asset Revision</td>
            <td class="a10">4</td>
            <td class="a10"><abbr title="0000000000000000000000000000000000000000000000000001000110111111">Hover for example</abbr></td>
            <td class="a10">Counter 0 to (2^32)-1</td>
            <td class="a10">uint</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Asset Creation Action Transaction Summary

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
            <td class="a5">0</td>
            <td class="a6">Contract Public Address</td>
            <td class="a6"></td>
            <td class="a10">0</td>
            <td class="a10">Contract Public Address</td>
            <td class="a10">Required so that users can monitor transactions to the contract for updates to contract/assets.</td>
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
                <td class="a10">tokenized.com</td>
                <td class="a10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="a10">byte</td>
                <td class="a10"></td>
            </tr>
            <tr>
                <td class="a10">Push Data</td>
                <td class="a10">OpPushdata</td>
                <td class="a10">1</td>
                <td class="a10">0x4d</td>
                <td class="a10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="a10">byte</td>
                <td class="a10"></td>
            </tr>
            <tr>
                <td class="a10">Length of Action Payload</td>
                <td class="a10">LenActionPayload</td>
                <td class="a10"></td>
                <td class="a10">tokenized.com</td>
                <td class="a10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="a10">byte</td>
                <td class="a10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="a10">Version</td>
                <td class="a10">Version</td>
                <td class="a10">1</td>
                <td class="a10">0</td>
                <td class="a10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="a10">uint8</td>
                <td class="a10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="a10">Action Prefix</td>
                <td class="a10">ActionPrefix</td>
                <td class="a10">2</td>
                <td class="a10">A2</td>
                <td class="a10" style="word-break:break-all">// A2 identifies data as a AssetCreation message.</td>
                <td class="a10">string</td>
                <td class="a10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
