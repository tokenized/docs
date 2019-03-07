
#Send Action

<div class="ui modal" id="header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr>
                <td class="t6">Header[]</td>
                <td class="t6">Header Array</td>
                <td class="t6">-</td>
                <td class="t6">-</td>
                <td class="t6">Common header data for all messages</td>
                <td class="t6">Header</td>
                <td class="t7"></td>
            </tr>
        </table>
    </div>
</div>

Send Action -  A Token Owner Sends a Token to a Receiver. The Send Action requires no sign-off by the Token Receiving Party and does not provide any on-chain consideration to the Token Sending Party.  Can be used for redeeming a ticket, coupon, points, etc.

The following breaks down the construction of a Send Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr"> 
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
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
            <td class="s5" rowspan="20">Metadata (OP_RETURN Payload)</td>
            <td class="t6" colspan="7"><a href="#" data-popover="header">Header[] - Click to show content</a></td>
        </tr>
        <tr>
            <td class="t10">Text Encoding</td>
            <td class="t10">TextEncoding</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="t10">uint8</td>
            <td class="t11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr>
            <td class="t10">Asset Type</td>
            <td class="t10">AssetType</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">SHC</td>
            <td class="t10">eg. Share, Bond, Ticket. All characters must be capitalised.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Asset ID</td>
            <td class="t10">AssetID</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="t10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Token Sender Count</td>
            <td class="t10">TokenSenderCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10">Number inputs sending tokens. 1-255, 0 is not valid.</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Token Senders</td>
            <td class="t10">TokenSenders</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element has the value of tokens to be spent from the input address, which is referred to by the index.</td>
            <td class="t10">QuantityIndex[]</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">The number of token receivers</td>
            <td class="t10">TokenReceiverCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10">Number of outputs receiving tokens. 1-255. 0 is not valid.</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Token Receivers</td>
            <td class="t10">TokenReceivers</td>
            <td class="t10">0</td>
            <td class="t10" style="word-break:break-all"></td>
            <td class="t10">Each element has the value of tokens to be received by the output address, which is referred to by the index.</td>
            <td class="t10">TokenReceiver[]</td>
            <td class="t11"></td>
        </tr>
    </table>
</div>