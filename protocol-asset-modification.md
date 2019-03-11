

#Asset Modification Action

Asset Modification Action -  Token Dilutions, Call Backs/Revocations, burning etc. Any field can be amended except for the Asset Revision field (incremental counter based on the previous Asset Creation Txn) and the Action Prefix. Asset Types specific payloads are locked to the Asset Type.  Asset Type specific payload amendments must be done as a protocol Version upgrade.  Authorization flags can restrict some fields or all fields from being amended. Some amendments require a Token Owner vote for the smart contract to permit.

The following breaks down the construction of a Asset Modification Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="6">Metadata (OP_RETURN Payload)</td>
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
        <tr><td class="a10">Asset Revision</td>
            <td class="a10">AssetRevision</td>
            <td class="a10">8</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10">Counter. (Subfield cannot be manually changed by Asset Modification Action.  Only SC can increment by 1 with each AC action. SC will reject AM actions where the wrong asset revision has been selected. </td>
            <td class="a10">uint64</td>
            <td class="a11">Cannot be Amended</td>
        </tr>
        <tr><td class="a10">ModificationCount</td>
            <td class="a10">ModificationCount</td>
            <td class="a10">1</td>
            <td class="a10" style="word-break:break-all">0</td>
            <td class="a10">Number of Modifications. Must be less than the max Subfield Index of CF.</td>
            <td class="a10">uint8</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Modifications</td>
            <td class="a10">Modifications</td>
            <td class="a10">0</td>
            <td class="a10" style="word-break:break-all"></td>
            <td class="a10"></td>
            <td class="a10">Amendment[]</td>
            <td class="a11"></td>
        </tr>
        <tr><td class="a10">Ref Tx-ID</td>
            <td class="a10">RefTxID</td>
            <td class="a10">32</td>
            <td class="a10" style="word-break:break-all">a8700385d4cc62628cc34629862121f84e6237689de8e45e151dcbc8cf30b33d</td>
            <td class="a10">Tx-ID of the associated Result action (governance) that permitted the modifications.</td>
            <td class="a10">sha256</td>
            <td class="a11"></td>
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
                <td class="a6">A3</td>
                <td class="a6">The action prefix is what determines the action type.</td>
                <td class="a6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="AssetModification">
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