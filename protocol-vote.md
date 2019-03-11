

#Vote Action

Vote Action -  A vote is created by the Contract in response to a valid Referendum (Issuer) or Initiative (User) Action.  Votes can be made by Token Owners.  

The following breaks down the construction of a Vote Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="2">Metadata (OP_RETURN Payload)</td>
            <td class="g7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
        </tr>
        <tr><td class="g10">Timestamp</td>
            <td class="g10">Timestamp</td>
            <td class="g10">8</td>
            <td class="g10" style="word-break:break-all">1551767413250187179</td>
            <td class="g10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="g10">timestamp</td>
            <td class="g11">Cannot be changed by issuer, operator. Smart contract controls.</td>
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
                <td class="g5">ProtocolID</td>
                <td class="g6">Protocol Identifier</td>
                <td class="g6">13</td>
                <td class="g6">tokenized.com</td>
                <td class="g6">Tokenized Protocol Identifier</td>
                <td class="g6">string</td>
            </tr>
            <tr>
                <td class="g5">OpPushdata</td>
                <td class="g6">Pushdata Instruction</td>
                <td class="g6">1</td>
                <td class="g6">Varies</td>
                <td class="g6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="g6">opcode</td>
            </tr>
            <tr>
                <td class="g5">LenActionPayload</td>
                <td class="g6">Length of Action Payload</td>
                <td class="g6">0, 1, 2 or 4 bytes</td>
                <td class="g6">0x199</td>
                <td class="g6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="g6">pushdata_length</td>
            </tr>
            <tr>
                <td class="g5">Version</td>
                <td class="g6">Version</td>
                <td class="g6">1</td>
                <td class="g6">0</td>
                <td class="g6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="g6">uint8</td>
            </tr>
            <tr>
                <td class="g5">ActionPrefix</td>
                <td class="g6">Action Prefix</td>
                <td class="g6">2</td>
                <td class="g6">G3</td>
                <td class="g6">The action prefix is what determines the action type.</td>
                <td class="g6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="Vote">
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
            <td class="g10">Header</td>
            <td class="g10">Header</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all"></td>
            <td class="g10">Common header data for all messages</td>
            <td class="g10">Header</td>
            <td class="g11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>