

#Swap Action

Swap Action -  Two parties (or more) want to swap a token (Atomic Swap) directly for another token.  At a minimum, Bitcoin is used in the txn for paying the necessary network/transaction fees.

The following breaks down the construction of a Swap Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="19">Metadata (OP_RETURN Payload)</td>
            <td class="t7" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
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
            <td class="t10">To be swapped for Asset2.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>

        <tr><td class="t10">Asset ID 1</td>
            <td class="t10">AssetID1</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">ran2qsznhis53z</td>
            <td class="t10">To be swapped for Asset2.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>

        <tr><td class="t10">Asset Type 2</td>
            <td class="t10">AssetType2</td>
            <td class="t10">3</td>
            <td class="t10" style="word-break:break-all">SHC</td>
            <td class="t10">To be swapped for Asset1.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>

        <tr><td class="t10">Asset ID 2</td>
            <td class="t10">AssetID2</td>
            <td class="t10">32</td>
            <td class="t10" style="word-break:break-all">apm2qsznhks23z</td>
            <td class="t10">To be swapped for Asset1.</td>
            <td class="t10">string</td>
            <td class="t11"></td>
        </tr>

        <tr><td class="t10">Offer Expiry</td>
            <td class="t10">OfferExpiry</td>
            <td class="t10">8</td>
            <td class="t10" style="word-break:break-all">Sun May 06 2018 06:00:00 GMT+1000 (AEST)</td>
            <td class="t10">This prevents either party from holding on to the partially signed message as a form of an option.  Eg. the exchange at this price is valid for 30 mins.</td>
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
            <td class="t10">Fixed fee</td>
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

    </table>
</div>


<div class="ui modal" id="type-Header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="t10">Protocol Identifier</td>
                <td class="t10">ProtocolID</td>
                <td class="t10">13</td>
                <td class="t10" style="word-break:break-all">tokenized.com</td>
                <td class="t10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="t10">string</td>
                <td class="t11"></td>
            </tr>
            <tr>
                <td class="t10">Push Data</td>
                <td class="t10">OpPushdata</td>
                <td class="t10">1</td>
                <td class="t10" style="word-break:break-all">77</td>
                <td class="t10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="t10">opcode</td>
                <td class="t11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="t10">Length of Action Payload</td>
                <td class="t10">LenActionPayload</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all">409</td>
                <td class="t10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="t10">pushdata_length</td>
                <td class="t11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="t10">Version</td>
                <td class="t10">Version</td>
                <td class="t10">1</td>
                <td class="t10" style="word-break:break-all">0</td>
                <td class="t10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="t10">uint8</td>
                <td class="t11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="t10">Action Prefix</td>
                <td class="t10">ActionPrefix</td>
                <td class="t10">2</td>
                <td class="t10" style="word-break:break-all">C1</td>
                <td class="t10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="t10">string</td>
                <td class="t11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

