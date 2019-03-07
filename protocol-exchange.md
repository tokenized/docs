
#Exchange Action

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

Exchange Action -  Tokens exchanged for Bitcoin (BSV). Example: Bob (Token Sender) to sell 21,000 tokens to Alice (Token Receiver) for 7 BSV.  Both parties must sign the transaction for it to be valid.

The following breaks down the construction of a Exchange Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="t10" style="word-break:break-all">RRE</td>
            <td class="t10">Asset Type to be exchanged.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Asset ID</td>
            <td class="t10">AssetID</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z</td>
            <td class="t10">ID of the Asset that is being exchanged.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Offer Expiry</td>
            <td class="t10">OfferExpiry</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">Sun May 06 2018 06:00:00 GMT+1000 (AEST)</td>
            <td class="t10">This prevents the token receiver from holding on to the signed message as a type of an option.  Eg. the sale of these tokens at this price is valid for 30 mins.</td>
            <td class="t10">time</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Exchange Fee Currency</td>
            <td class="t10">ExchangeFeeCurrency</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">AUD</td>
            <td class="t10">BSV, USD, AUD, EUR, etc.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Exchange Fee Variable</td>
            <td class="t10">ExchangeFeeVar</td>
            <td class="t10">4</td>
            <td class="t10" style="word-break:break-all">0.005</td>
            <td class="t10">Percent of the value of the transaction</td>
            <td class="t10">float32</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Exchange Fee Fixed</td>
            <td class="t10">ExchangeFeeFixed</td>
            <td class="t10">4</td>
            <td class="t10" style="word-break:break-all">0.01</td>
            <td class="t10">Fixed Fee</td>
            <td class="t10">float32</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Exchange Fee Address</td>
            <td class="t10">ExchangeFeeAddress</td>
            <td class="t10">34</td>
            <td class="t10" style="word-break:break-all">1HQ2ULuD7T5ykaucZ3KmTo4i29925Qa6ic</td>
            <td class="t10">Identifies the public address that the exchange fee should be paid to.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Quantity of Token Sending Addresses</td>
            <td class="t10">TokenSenderCount</td>
            <td class="t10">1</td>
            <td class="t10" style="word-break:break-all">0</td>
            <td class="t10">Number input addresses that are sending tokens. 1-255, 0 is not valid.</td>
            <td class="t10">uint8</td>
            <td class="t11"></td>
        </tr>
        <tr>
            <td class="t10">Token Sender</td>
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