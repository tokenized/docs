
<html>
    <head>
        <link rel="stylesheet" href="css/style.css">
        <H1>Send Action</H1>
        <p>
        Send Action -  A Token Owner Sends a Token to a Receiver. The Send Action requires no sign-off by the Token Receiving Party and does not provide any on-chain consideration to the Token Sending Party.  Can be used for User Revocation (remove tokens from wallet by sending back to Issuer).  Can be used for redeeming a ticket, coupon, points, etc.<br><br>
        The following breaks down the construction of a Send Action. The action is constructed by building a single string from each of the elements in order.
        </p>
    </head>
    <div class="ritz grid-container" dir="ltr">
        <body>
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
                    <td class="s5" rowspan="10">Metadata (OP_RETURN Payload)</td>
                    <td class="t6">Header[]</td>
                    <td class="t6">Header Array</td>
                    <td class="t6">-</td>
                    <td class="t6">-</td>
                    <td class="t6">Common header data for all messages</td>
                    <td class="t6">Header</td>
                    <td class="t7"></td>
                </tr>
                    <tr>
                    <td class="t10">Text Encoding</td>
                    <td class="t10">TextEncoding</td>
                    <td class="t10">1</td>
                    <td class="t10" style="word-break:break-all">0</td>
                    <td class="t10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
                    <td class="t10">uint8</td>
                    <td class="t11">Can be changed by Issuer or Operator at their discretion.</td>
                </tr>                <tr>
                    <td class="t10">Asset Type</td>
                    <td class="t10">AssetType</td>
                    <td class="t10">3</td>
                    <td class="t10" style="word-break:break-all">SHC</td>
                    <td class="t10">eg. Share, Bond, Ticket. All characters must be capitalised.</td>
                    <td class="t10">string</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Asset ID</td>
                    <td class="t10">AssetID</td>
                    <td class="t10">32</td>
                    <td class="t10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
                    <td class="t10">Randomly generated base58 string.  Each Asset ID should be unique.  However, a Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.</td>
                    <td class="t10">string</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Quantity of Token Sending Addresses</td>
                    <td class="t10">QtyOfTokenSendingAddresses</td>
                    <td class="t10">1</td>
                    <td class="t10" style="word-break:break-all">2</td>
                    <td class="t10">Number inputs sending tokens. Number equates to the number of inputs starting with index 0. 1-255, 0 is not valid.</td>
                    <td class="t10">uint8</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Token Sending Address X</td>
                    <td class="t10">TokenSendingAddressX</td>
                    <td class="t10">8</td>
                    <td class="t10" style="word-break:break-all">100</td>
                    <td class="t10">Value of tokens to be spent from the address at Input Index X</td>
                    <td class="t10">uint64</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Quantity of Token Receiving Addresses</td>
                    <td class="t10">QtyOfTokenReceivingAddresses</td>
                    <td class="t10">1</td>
                    <td class="t10" style="word-break:break-all">1</td>
                    <td class="t10">Number outputs receiving tokens. Number equates to the number of outputs starting with index 1 (Contract Address is Index 0). 1-255. 0 is not valid.</td>
                    <td class="t10">uint8</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Token Receiving Address X</td>
                    <td class="t10">TokenReceivingAddressX</td>
                    <td class="t10">8</td>
                    <td class="t10" style="word-break:break-all">100</td>
                    <td class="t10">Value of tokens to be received by the address at OutputX</td>
                    <td class="t10">uint64</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Registry Signature Algorithm</td>
                    <td class="t10">RegistrySigAlgoReceivingAddressX</td>
                    <td class="t10">1</td>
                    <td class="t10" style="word-break:break-all">1</td>
                    <td class="t10">0 = No Registry-signed Message, 1 = ECDSA+secp256k1</td>
                    <td class="t10">uint8</td>
                    <td class="t11"></td>
                </tr>                <tr>
                    <td class="t10">Registry Confirmation Signature for Token Receiving X</td>
                    <td class="t10">RegistryConfirmationSigTokenReceivingAddressX</td>
                    <td class="t10">0</td>
                    <td class="t10" style="word-break:break-all">IEwzJB23sFryKMzx5MfBwnt1GMUKNTQnqF8WhsSD1wwtKKg7BoA/5GLeu5Unwar7ZhtR18tdzuIfdXDtU+zMHL8=</td>
                    <td class="t10">Length 0-255 bytes. IF restricted to a registry (whitelist) or has transfer restrictions (age, location, investor status): ECDSA+secp256k1 (or the like) signed message provided by an approved/trusted registry through an API signature of [Contract Address + Asset Code + Public Address + Blockhash of the Latest Block + Block Height + Confirmed/Rejected Bool]. If no transfer restrictions(trade restriction/age restriction fields in the Asset Type payload. or restricted to a whitelist by the Contract Auth Flags, it is a NULL field.</td>
                    <td class="t10">nvarchar8</td>
                    <td class="t11"></td>
                </tr>
            </table>
        </body>
    </div>
</html>