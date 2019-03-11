

#Asset Creation Action

Asset Creation Action -  This action creates an Asset in response to the Issuer's instructions in the Definition Action.

The following breaks down the construction of a Asset Creation Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr"> 
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style="height:19px">
            <th style="width:6%" class="s0">Field</th>
            <th style="width:9%" class="s1">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:29%" class="s1">Example Values</th>
            <th style="width:26%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th style="width:14%" class="s2">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="s5" rowspan="20">Metadata (OP_RETURN Payload)</td>
            <td class="a7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
        </tr>
        <tr><td class="a10">Text Encoding</td>
            <td class="a10">TextEncoding</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="a10">uint8</td>
            <td class="a11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr><td class="a10">Asset Type</td>
            <td class="a10">AssetType</td>
            <td class="a10">3</td>
            <td class="a10" style="word-break:break-all">SHC</td>
            <td class="a10">eg. Share - Common</td>
            <td class="a10">string</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset ID</td>
            <td class="a10">Asset ID</td>
            <td class="a10">32</td>
            <td class="a10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="a10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type + Asset ID = Asset Code.  An Asset Code is a human readable idenitfier that can be used in a similar way to a Bitcoin (BSV) address, a vanity identifying label.</td>
            <td class="a10">string</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset Authorization Flags</td>
            <td class="a10">AssetAuthFlags</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">0000000000000000000000000000000000000000000000000001000110111111</td>
            <td class="a10">Authorization Flags,  bitwise operation</td>
            <td class="a10">bin</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Transfers Permitted</td>
            <td class="a10">TransfersPermitted</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">1</td>
            <td class="a10">1 = Transfers are permitted.  0 = Transfers are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Trade Restrictions</td>
            <td class="a10">TradeRestrictions</td>
            <td class="a10">3</td>
            <td class="a10" style="word-break:break-all">GBR</td>
            <td class="a10">Asset can only be traded within the trade restrictions.  Eg. AUS - Australian residents only.  EU - European Union residents only.</td>
            <td class="a10">string</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Enforcement Orders Permitted</td>
            <td class="a10">EnforcementOrdersPermitted</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">1</td>
            <td class="a10">1 = Enforcement Orders are permitted. 0 = Enforcement Orders are not permitted.</td>
            <td class="a10">bool</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Vote Multiplier</td>
            <td class="a10">VoteMultiplier</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">3</td>
            <td class="a10">Multiplies the vote by the integer. 1 token = 1 vote with a 1 for vote multipler (normal).  1 token = 3 votes with a multiplier of 3, for example.</td>
            <td class="a10">uint8</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Referendum Proposal</td>
            <td class="a10">ReferendumProposal</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">1</td>
            <td class="a10">A Referendum is permitted for Asset-Wide Proposals (outside of smart contract scope) if also permitted by the contract. If the contract has proposals by referendum restricted, then this flag is meaningless.</td>
            <td class="a10">bool</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Initiative Proposal</td>
            <td class="a10">InitiativeProposal</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">1</td>
            <td class="a10">An initiative is permitted for Asset-Wide Proposals (outside of smart contract scope) if also permitted by the contract. If the contract has proposals by initiative restricted, then this flag is meaningless.</td>
            <td class="a10">bool</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset Modification Governance</td>
            <td class="a10">AssetModificationGovernance</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">1</td>
            <td class="a10">1 - Contract-wide Asset Governance.  0 - Asset-wide Asset Governance.  If a referendum or initiative is used to propose a modification to a subfield controlled by the asset auth flags, then the vote will either be a contract-wide vote (all assets vote on the referendum/initiative) or an asset-wide vote (all assets vote on the referendum/initiative).  The voting system specifies the voting rules.</td>
            <td class="a10">bool</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Qty of Tokens</td>
            <td class="a10">TokenQty</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">1000000</td>
            <td class="a10">Quantity of token - 0 is valid. Fungible 'shares' of the Asset. 1 is used for non-fungible tokens.  Asset IDs become the non-fungible Asset ID and many Asset IDs can be associated with a particular Contract.</td>
            <td class="a10">uint64</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Contract Fee Currency</td>
            <td class="a10">ContractFeeCurrency</td>
            <td class="a10">3</td>
            <td class="a10" style="word-break:break-all">AUD</td>
            <td class="a10">BSV, USD, AUD, EUR, etc.</td>
            <td class="a10">string</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Contract Fee Var</td>
            <td class="a10">ContractFeeVar</td>
            <td class="a10">4</td>
            <td class="a10" style="word-break:break-all">0.005</td>
            <td class="a10">Percent of the value of the transaction</td>
            <td class="a10">float32</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Contract Fee Fixed</td>
            <td class="a10">ContractFeeFixed</td>
            <td class="a10">4</td>
            <td class="a10" style="word-break:break-all">0.01</td>
            <td class="a10">Fixed fee (payment made in BSV)</td>
            <td class="a10">float32</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset Payload Length</td>
            <td class="a10">AssetPayloadLen</td>
            <td class="a10">2</td>
            <td class="a10" style="word-break:break-all">9</td>
            <td class="a10">Size of the asset payload in bytes.</td>
            <td class="a10">uint16</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset Payload</td>
            <td class="a10">AssetPayload</td>
            <td class="a10">0</td>
            <td class="a10" style="word-break:break-all">some data</td>
            <td class="a10">Payload length is dependent on the asset type. Each asset is made up of a defined set of information pertaining to the specific asset type, and may contain fields of variable length type (nvarchar8, 16, 32)</td>
            <td class="a10">byte[]</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Asset Revision</td>
            <td class="a10">Asset Revision</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">0000000000000000000000000000000000000000000000000001000110111111</td>
            <td class="a10">Counter 0 - 65,535</td>
            <td class="a10">uint64</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Timestamp</td>
            <td class="a10">Timestamp</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">1551767413250187179</td>
            <td class="a10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="a10">timestamp</td>
            <td class="a11">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
        <tr>                <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>

<div class="ui modal" id="header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
        	<tr style='height:19px;'>
	            <th style="width:9%" class="s0">Label</th>
	            <th style="width:9%" class="s1">Name</th>
	            <th style="width:2%" class="s1">Bytes</th>
	            <th style="width:29%" class="s1">Example Values</th>
	            <th style="width:26%" class="s1">Comments</th>
	            <th style="width:5%" class="s1">Data Type</th>
	        </tr>
            <tr>
                <td class="a5">ProtocolID</td>
                <td class="a6">Protocol Identifier</td>
                <td class="a6">13</td>
                <td class="a6">tokenized.com</td>
                <td class="a6">Tokenized Protocol Identifier</td>
                <td class="a6">string</td>
            </tr>
            <tr>
                <td class="a5">OpPushdata</td>
                <td class="a6">Pushdata Instruction</td>
                <td class="a6">1</td>
                <td class="a6">Varies</td>
                <td class="a6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="a6">opcode</td>
            </tr>
            <tr>
                <td class="a5">LenActionPayload</td>
                <td class="a6">Length of Action Payload</td>
                <td class="a6">0, 1, 2 or 4 bytes</td>
                <td class="a6">0x199</td>
                <td class="a6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="a6">pushdata_length</td>
            </tr>
            <tr>
                <td class="a5">Version</td>
                <td class="a6">Version</td>
                <td class="a6">1</td>
                <td class="a6">0</td>
                <td class="a6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="a6">uint8</td>
            </tr>
            <tr>
                <td class="a5">ActionPrefix</td>
                <td class="a6">Action Prefix</td>
                <td class="a6">2</td>
                <td class="a6">A2</td>
                <td class="a6">The action prefix is what determines the action type.</td>
                <td class="a6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="AssetCreation">
    <i class="close icon"></i>
    <table class="ui table">
        <tr style='height:19px;'>
            <th style="width:6%" class="s0">Field</th>
            <th style="width:9%" class="s1">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:29%" class="s1">Example Values</th>
            <th style="width:26%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th style="width:14%" class="s2">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="a10">Header</td>
            <td class="a10">Header</td>
            <td class="a10">0</td>
            <td class="a10" style="word-break:break-all"></td>
            <td class="a10">Common header data for all messages</td>
            <td class="a10">Header</td>
            <td class="a11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>