

#Swap Action

Swap Action -  Two parties want to swap a token(s) (Atomic Swap) directly for another token(s).  Only two asset types per swap action. BSV is used in the txn other than for paying the necessary network/transaction fees.

The following breaks down the construction of a Swap Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="19">Metadata (OP_RETURN Payload)</td>
            <td class="t7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
        </tr>
        <tr><td class="t10">Text Encoding</td>
            <td class="t10">TextEncoding</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="t10">uint8</td>
            <td class="t11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr><td class="t10">Asset Type 1</td>
            <td class="t10">AssetType1</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">RRE</td>
            <td class="t10"></td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset ID 1</td>
            <td class="t10">AssetID1</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">ran2qsznhis53z</td>
            <td class="t10"></td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset Type 2</td>
            <td class="t10">AssetType2</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">SHC</td>
            <td class="t10"></td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset ID 2</td>
            <td class="t10">AssetID2</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z</td>
            <td class="t10"></td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Offer Expiry</td>
            <td class="t10">OfferExpiry</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">Sun May 06 2018 06:00:00 GMT+1000 (AEST)</td>
            <td class="t10">This prevents either party from holding on to the partially signed message as a form of an option.  Eg. the sale of these tokens at this price is valid for 30 mins.</td>
            <td class="t10">time</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Exchange Fee Currency</td>
            <td class="t10">ExchangeFeeCurrency</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">AUD</td>
            <td class="t10">BSV, USD, AUD, EUR, etc.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Exchange Fee Variable</td>
            <td class="t10">ExchangeFeeVar</td>
            <td class="t10">4</td>
            <td class="t10" style="word-break:break-all">0.005</td>
            <td class="t10">Percent of the value of the transaction</td>
            <td class="t10">float32</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Exchange Fee Fixed</td>
            <td class="t10">ExchangeFeeFixed</td>
            <td class="t10">4</td>
            <td class="t10" style="word-break:break-all">0.01</td>
            <td class="t10">Fixed fee (payment made in BSV</td>
            <td class="t10">float32</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Exchange Fee Address</td>
            <td class="t10">ExchangeFeeAddress</td>
            <td class="t10">34</td>
            <td class="t10" style="word-break:break-all">1HQ2ULuD7T5ykaucZ3KmTo4i29925Qa6ic</td>
            <td class="t10">Identifies the public address that the exchange fee should be paid to.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Qty of Asset 1 Sending Addresses</td>
            <td class="t10">Asset1SenderCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10">Asset 1 Sending Addresses</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset 1 Senders</td>
            <td class="t10">Asset1Senders</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element has the quantity of Asset1 tokens to be sent by the input address, which is referred to by the index.</td>
            <td class="t10">QuantityIndex[]</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Qty of Asset 1 Receiving Addresses</td>
            <td class="t10">Asset1ReceiverCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10"></td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset 1 Receivers</td>
            <td class="t10">Asset1Receivers</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element has the quantity of Asset 1 tokens to be received by the output address, which is referred to by the index.</td>
            <td class="t10">TokenReceiver[]</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Qty of Asset 2 Sending Addresses</td>
            <td class="t10">Asset2SenderCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10">Asset 2 Sending Addresses</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset 2 Senders</td>
            <td class="t10">Asset2Senders</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element has the quantity of Asset2 tokens to be sent by the input address, which is referred to by the index.</td>
            <td class="t10">QuantityIndex[]</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Qty of Asset 2 Receiving Addresses</td>
            <td class="t10">Asset2ReceiverCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10"></td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr><td class="t10">Asset 2 Receivers</td>
            <td class="t10">Asset2Receivers</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element contains the quantity of Asset 2 tokens to be received by the output address, which is referred to by the index.</td>
            <td class="t10">TokenReceiver[]</td>
            <td class="t11"></td>
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
                <td class="t5">ProtocolID</td>
                <td class="t6">Protocol Identifier</td>
                <td class="t6">13</td>
                <td class="t6">tokenized.com</td>
                <td class="t6">Tokenized Protocol Identifier</td>
                <td class="t6">string</td>
            </tr>
            <tr>
                <td class="t5">OpPushdata</td>
                <td class="t6">Pushdata Instruction</td>
                <td class="t6">1</td>
                <td class="t6">Varies</td>
                <td class="t6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="t6">opcode</td>
            </tr>
            <tr>
                <td class="t5">LenActionPayload</td>
                <td class="t6">Length of Action Payload</td>
                <td class="t6">0, 1, 2 or 4 bytes</td>
                <td class="t6">0x199</td>
                <td class="t6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="t6">pushdata_length</td>
            </tr>
            <tr>
                <td class="t5">Version</td>
                <td class="t6">Version</td>
                <td class="t6">1</td>
                <td class="t6">0</td>
                <td class="t6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="t6">uint8</td>
            </tr>
            <tr>
                <td class="t5">ActionPrefix</td>
                <td class="t6">Action Prefix</td>
                <td class="t6">2</td>
                <td class="t6">T3</td>
                <td class="t6">The action prefix is what determines the action type.</td>
                <td class="t6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="Swap">
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
            <td class="t10">Header</td>
            <td class="t10">Header</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Common header data for all messages</td>
            <td class="t10">Header</td>
            <td class="t11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>