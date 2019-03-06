
<html>
	<head>
		<link rel="stylesheet" href="css/style.css">
		<H1>Swap Action</H1>
		<p>
		Swap Action -  Two parties want to swap a token (Atomic Swap) directly for another token.  BSV is used in the txn other than for paying the necessary network/transaction fees.<br><br>
		The following breaks down the construction of a Swap Action. The action is constructed by building a single string from each of the elements in order.
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
					<td class="s5" rowspan="23">Metadata (OP_RETURN Payload)</td>
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
				</tr>				<tr>
			    	<td class="t10">Asset Type 1</td>
			    	<td class="t10">AssetType1</td>
			    	<td class="t10">3</td>
			    	<td class="t10" style="word-break:break-all">RRE</td>
			    	<td class="t10">The Asset Type and Asset ID are used by wallets/Contracts/users to link the Action to the Asset Creation Action. All Actions reference the Asset Creation Action.  The Asset Creation Txn-ID is not used because Asset Amendments would result in all Token Owners would need to have their tokens 'updated'.</td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Asset ID 1</td>
			    	<td class="t10">AssetID1</td>
			    	<td class="t10">32</td>
			    	<td class="t10" style="word-break:break-all">ran2qsznhis53z</td>
			    	<td class="t10"></td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Asset Type 2</td>
			    	<td class="t10">AssetType2</td>
			    	<td class="t10">3</td>
			    	<td class="t10" style="word-break:break-all">SHC</td>
			    	<td class="t10">In an Atomic Swap the Party2Asset(Type/ID/TokenQty) is what the Contracting Party 2 is putting up for exchange in the swap.  That is they own the Party2Asset before the exchange and will own Party1Asset after the exchange, if approved by the smart contract.</td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Asset ID 2</td>
			    	<td class="t10">AssetID2</td>
			    	<td class="t10">32</td>
			    	<td class="t10" style="word-break:break-all">apm2qsznhks23z</td>
			    	<td class="t10"></td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Offer Expiry</td>
			    	<td class="t10">OfferExpiry</td>
			    	<td class="t10">8</td>
			    	<td class="t10" style="word-break:break-all">Sun May 06 2018 06:00:00 GMT+1000 (AEST)</td>
			    	<td class="t10">This prevents either party from holding on to the partially signed message as a form of an option.  Eg. the sale of these tokens at this price is valid for 30 mins.</td>
			    	<td class="t10">time</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Exchange Fee Currency</td>
			    	<td class="t10">ExchangeFeeCurrency</td>
			    	<td class="t10">3</td>
			    	<td class="t10" style="word-break:break-all">AUD</td>
			    	<td class="t10">BSV, USD, AUD, EUR, etc.</td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Exchange Fee Variable</td>
			    	<td class="t10">ExchangeFeeVar</td>
			    	<td class="t10">4</td>
			    	<td class="t10" style="word-break:break-all">0.005</td>
			    	<td class="t10">Percent of the value of the transaction</td>
			    	<td class="t10">float32</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Exchange Fee Fixed</td>
			    	<td class="t10">ExchangeFeeFixed</td>
			    	<td class="t10">4</td>
			    	<td class="t10" style="word-break:break-all">0.01</td>
			    	<td class="t10">Fixed fee (payment made in BSV</td>
			    	<td class="t10">float32</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Exchange Fee Address</td>
			    	<td class="t10">ExchangeFeeAddress</td>
			    	<td class="t10">34</td>
			    	<td class="t10" style="word-break:break-all">1HQ2ULuD7T5ykaucZ3KmTo4i29925Qa6ic</td>
			    	<td class="t10">Identifies the public address that the exchange fee should be paid to.</td>
			    	<td class="t10">string</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Qty of Asset 1 Sending Addresses</td>
			    	<td class="t10">QtyOfAsset1SendingAddresses</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">1</td>
			    	<td class="t10">Asset 1 Sending Addresses</td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Address X Asset 1 Sending Qty</td>
			    	<td class="t10">AddressXAsset1SendingQty</td>
			    	<td class="t10">8</td>
			    	<td class="t10" style="word-break:break-all">200</td>
			    	<td class="t10">Qty of Asset1 tokens to be sent by the address at Index X (Address X) position of the inputs</td>
			    	<td class="t10">uint64</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Qty of Asset 1 Receiving Addresses</td>
			    	<td class="t10">QtyOfAsset1ReceivingAddresses</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">0</td>
			    	<td class="t10"></td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Address X Asset 1 Receiving Qty</td>
			    	<td class="t10">AddressXAsset1ReceivingQty</td>
			    	<td class="t10">8</td>
			    	<td class="t10" style="word-break:break-all">200</td>
			    	<td class="t10">Qty of Asset 1 tokens to be received by the address at Index X (Address X) position of the outputs.</td>
			    	<td class="t10">uint64</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Registry Signature Algorithm for Asset 1 Receiving Address X</td>
			    	<td class="t10">RegistrySigAlgoAsset1ReceivingAddressX</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">1</td>
			    	<td class="t10">0 = No Registry-signed Message, 1 = ECDSA+secp256k1</td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Registry Confirmation Signature for Address X Asset 1 Receiving</td>
			    	<td class="t10">RegistryConfirmationSigAddressXAsset1Receiving</td>
			    	<td class="t10">89</td>
			    	<td class="t10" style="word-break:break-all">IEwzJB23sFryKMzx5MfBwnt1GMUKNTQnqF8WhsSD1wwtKKg7BoA/5GLeu5Unwar7ZhtR18tdzuIfdXDtU+zMHL8=</td>
			    	<td class="t10">Length 0-255 bytes. IF restricted to a registry (whitelist) or has transfer restrictions (age, location, investor status): ECDSA+secp256k1 (or the like) signed message provided by an approved/trusted registry through an API signature of [Contract Address + Asset Code + Public Address + Blockhash of the Latest Block + Block Height + Confirmed/Rejected Bool]. If no transfer restrictions(trade restriction/age restriction fields in the Asset Type payload. or restricted to a whitelist by the Contract Auth Flags, it is a NULL field.</td>
			    	<td class="t10">nvarchar8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Qty of Asset 2 Sending Addresses</td>
			    	<td class="t10">QtyOfAsset2SendingAddresses</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">1</td>
			    	<td class="t10">Asset 2 Sending Addresses</td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Address X Asset 2 Sending Qty</td>
			    	<td class="t10">AddressXAsset2SendingQty</td>
			    	<td class="t10">8</td>
			    	<td class="t10" style="word-break:break-all">200</td>
			    	<td class="t10">Qty of Asset2 tokens to be sent by the address at Index X (Address X) position of the inputs</td>
			    	<td class="t10">uint64</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Qty of Asset 2 Receiving Addresses</td>
			    	<td class="t10">QtyOfAsset2ReceivingAddresses</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">0</td>
			    	<td class="t10"></td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Address X Asset 2 Receiving Qty</td>
			    	<td class="t10">AddressXAsset2ReceivingQty</td>
			    	<td class="t10">8</td>
			    	<td class="t10" style="word-break:break-all">200</td>
			    	<td class="t10">Qty of Asset 2 tokens to be received by the address at Index X (Address X) position of the outputs.</td>
			    	<td class="t10">uint64</td>
			    	<td class="t11"></td>
				</tr>				<tr>
			    	<td class="t10">Registry Signature Algorithm for Asset 2 Receiving Address X</td>
			    	<td class="t10">RegistrySigAlgoAsset2ReceivingAddressX</td>
			    	<td class="t10">1</td>
			    	<td class="t10" style="word-break:break-all">1</td>
			    	<td class="t10">0 = No Registry-signed Message, 1 = ECDSA+secp256k1</td>
			    	<td class="t10">uint8</td>
			    	<td class="t11"></td>
				</tr>				<tr>
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