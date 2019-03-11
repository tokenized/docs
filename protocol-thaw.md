

#Thaw Action

Thaw Action -  to be used to comply with contractual obligations or legal requirements.  The Alleged Offender's tokens will be unfrozen to allow them to resume normal exchange and governance activities.

The following breaks down the construction of a Thaw Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="4">Metadata (OP_RETURN Payload)</td>
            <td class="e7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
        </tr>
        <tr><td class="e10">Number of Addresses</td>
            <td class="e10">AddressCount</td>
            <td class="e10">2</td>
            <td class="e10" style="word-break:break-all">0</td>
            <td class="e10">0 - 65,535</td>
            <td class="e10">uint16</td>
            <td class="e11"></td>
        </tr>
        <tr><td class="e10">Addresses</td>
            <td class="e10">Addresses</td>
            <td class="e10">0</td>
            <td class="e10" style="word-break:break-all"></td>
            <td class="e10">Addresses holding tokens to be thawed.</td>
            <td class="e10">Address[]</td>
            <td class="e11"></td>
        </tr>
        <tr><td class="e10">Timestamp</td>
            <td class="e10">Timestamp</td>
            <td class="e10">8</td>
            <td class="e10" style="word-break:break-all">1551767413250187179</td>
            <td class="e10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="e10">timestamp</td>
            <td class="e11">Cannot be changed by issuer, operator. Smart contract controls.</td>
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
                <td class="e5">ProtocolID</td>
                <td class="e6">Protocol Identifier</td>
                <td class="e6">13</td>
                <td class="e6">tokenized.com</td>
                <td class="e6">Tokenized Protocol Identifier</td>
                <td class="e6">string</td>
            </tr>
            <tr>
                <td class="e5">OpPushdata</td>
                <td class="e6">Pushdata Instruction</td>
                <td class="e6">1</td>
                <td class="e6">Varies</td>
                <td class="e6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="e6">opcode</td>
            </tr>
            <tr>
                <td class="e5">LenActionPayload</td>
                <td class="e6">Length of Action Payload</td>
                <td class="e6">0, 1, 2 or 4 bytes</td>
                <td class="e6">0x199</td>
                <td class="e6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="e6">pushdata_length</td>
            </tr>
            <tr>
                <td class="e5">Version</td>
                <td class="e6">Version</td>
                <td class="e6">1</td>
                <td class="e6">0</td>
                <td class="e6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="e6">uint8</td>
            </tr>
            <tr>
                <td class="e5">ActionPrefix</td>
                <td class="e6">Action Prefix</td>
                <td class="e6">2</td>
                <td class="e6">E3</td>
                <td class="e6">The action prefix is what determines the action type.</td>
                <td class="e6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="Thaw">
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
            <td class="e10">Header</td>
            <td class="e10">Header</td>
            <td class="e10">0</td>
            <td class="e10" style="word-break:break-all"></td>
            <td class="e10">Common header data for all messages</td>
            <td class="e10">Header</td>
            <td class="e11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>