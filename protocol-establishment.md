

#Establishment Action

Establishment Action -  Establishes a register. The register is intended to be used primarily for whitelisting.  However, other types of registers can be used.

The following breaks down the construction of a Establishment Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="7">Metadata (OP_RETURN Payload)</td>
            <td class="r7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
        </tr>
        <tr><td class="r10">Text Encoding</td>
            <td class="r10">TextEncoding</td>
            <td class="r10">1</td>
            <td class="r10" style="word-break:break-all">0</td>
            <td class="r10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="r10">uint8</td>
            <td class="r11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr><td class="r10">Registrar</td>
            <td class="r10">Registrar</td>
            <td class="r10">9</td>
            <td class="r10" style="word-break:break-all">Coinbase</td>
            <td class="r10">Length 0-255 bytes. 0 is acceptable. Registrar Subfield.</td>
            <td class="r10">nvarchar8</td>
            <td class="r11"></td>
        </tr>
        <tr><td class="r10">Register Type</td>
            <td class="r10">RegisterType</td>
            <td class="r10">1</td>
            <td class="r10" style="word-break:break-all"></td>
            <td class="r10">1 - KYC</td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>
        <tr><td class="r10">Jurisdiction</td>
            <td class="r10">Jurisdiction</td>
            <td class="r10">5</td>
            <td class="r10" style="word-break:break-all">AUS</td>
            <td class="r10"></td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>
        <tr><td class="r10">Supporting Documentation Hash</td>
            <td class="r10">SupportingDocumentationHash</td>
            <td class="r10">32</td>
            <td class="r10" style="word-break:break-all">98ea6e4f216f2fb4b69fff9b3a44842c38686ca685f3f55dc48c5d3fb1107be4</td>
            <td class="r10"></td>
            <td class="r10">sha256</td>
            <td class="r11"></td>
        </tr>
        <tr><td class="r10">Message</td>
            <td class="r10">Message</td>
            <td class="r10">25</td>
            <td class="r10" style="word-break:break-all">North America Whitelist</td>
            <td class="r10">Length 0-65,535 bytes. An establishment message can be used to provide more information.</td>
            <td class="r10">nvarchar16</td>
            <td class="r11"></td>
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
                <td class="r5">ProtocolID</td>
                <td class="r6">Protocol Identifier</td>
                <td class="r6">13</td>
                <td class="r6">tokenized.com</td>
                <td class="r6">Tokenized Protocol Identifier</td>
                <td class="r6">string</td>
            </tr>
            <tr>
                <td class="r5">OpPushdata</td>
                <td class="r6">Pushdata Instruction</td>
                <td class="r6">1</td>
                <td class="r6">Varies</td>
                <td class="r6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="r6">opcode</td>
            </tr>
            <tr>
                <td class="r5">LenActionPayload</td>
                <td class="r6">Length of Action Payload</td>
                <td class="r6">0, 1, 2 or 4 bytes</td>
                <td class="r6">0x199</td>
                <td class="r6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="r6">pushdata_length</td>
            </tr>
            <tr>
                <td class="r5">Version</td>
                <td class="r6">Version</td>
                <td class="r6">1</td>
                <td class="r6">0</td>
                <td class="r6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="r6">uint8</td>
            </tr>
            <tr>
                <td class="r5">ActionPrefix</td>
                <td class="r6">Action Prefix</td>
                <td class="r6">2</td>
                <td class="r6">R1</td>
                <td class="r6">The action prefix is what determines the action type.</td>
                <td class="r6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="Establishment">
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
            <td class="r10">Header</td>
            <td class="r10">Header</td>
            <td class="r10">0</td>
            <td class="r10" style="word-break:break-all"></td>
            <td class="r10">Common header data for all messages</td>
            <td class="r10">Header</td>
            <td class="r11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>