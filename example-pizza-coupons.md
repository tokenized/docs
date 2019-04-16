# Dominics Pizza Grand Opening

Dominic has spent the last 2 years planning for today. His restaurant fit out is complete, the mortar on his wood fired pizza ovens is dry, and his fridges are chilling a variety of bottled drinks.
The last thing on his list is to configure a smart contract for his membership program and a loyalty point system.
Dominic downloads the Tokenized Nexus wallet and installs it on his PC. He creates a new wallet and makes a safe backup of the master key, then begins configuring his Contract Offer.
Dominic has decided to give his first 100 customers a free slice of pizza for their next visit, and to establish a frequent slice program that gives customers one free slice for every 7 slices they buy.

### Creating the Contract

Dominic names his contract 'Dominic's Pizza Loyalty Program'. He has already prepared a set of terms and conditions for his contract, and has them saved in a PDF file. The PDF file and copies of the flier detailing his Frequent Slice program are stored in a 7Zip file ready to be attached to the contract. 
Using the Contract Creation tool, Dominic creates the following Contract Offer:

Contract Name:					Dominic's Pizza Loyalty Program Smart Contract
Body of Agreement Type:			SHA-256 Hash
Body of Agreement:				The SHA-256 hash of Dominic's terms and conditions
Contract Type:					Loyalty Program
Supporting Docs File Type:		7zip
Supporting Docs:				A 7zip file containing supporting docs including the terms and conditions file and a flier detailing the initial program
Governing Law:					Australia
Jurisdiction:					Australia
Contract Expiration:			Contract is set to operate for 2 years
Contract URI:					A link to Dominic's contract file
Issuer:							Dominic's Pizza Pty Ltd
								Address: Dominics pizza address
								Email: mail@dominicspizza.com
								Phone no: Dominic's Pizza phone number
								Administration -	CEO:			Dominic Spinner
													Manager:		Elton Walker
													Manager:		Fiona Temple
Company Logo:					URL to logo file
Contract Operator Included?:	Yes
Contract Operator:				Tokenized
Contract Authorisation Flags:	Issuer can amend all fields. Referendums and initiatives are unable to be used.
Contract Fee:					As per the detail in the Tokenized operator agreement

/// PUT ALL THAT IN A TEMPLATE

Now that Dominic has filled out all the details, he is ready to create his smart contract.

Nexus does this by generating a Contract Offer transaction which it sends to the Tokenized Platform. For Tokenized to act as the contract operator, it is necessary for Tokenized to sign the Contract Offer, or it will be rejected by the smart contract. This process is handled between Dominic's app and the Tokenized server that runs the smart contract agent. When it receives the template Contract Offer, it creates a new address in a derivative of its own master address and gives the keys to an agent created to run Dominic's smart contract. It sends the Contract Offer to this address.

/// CONTRACT OFFER

The Agent receives the Contract Offer and unpacks it, validating its contents before building a Contract Formation response. The contract formation contains all the same information received in the Contract Offer, plus a version indicator which is set to zero, and a Timestamp that is set to the time the transaction was created. It sends this onto the Bitcoin network where it is cleared to Dominic's wallet a few seconds later.

/// CONTRACT FORMATION

### Creating the assets
Now that Dominic's contract is live, he is able to use it to create the assets that he will use in his loyalty program.
Firstly, he has decided to create a 'Free Slice' coupon which he will give to the first 100 people who buy a whole pizza. He wants people to also have the option to send these coupons to other people so that they can come and try his food. Using the Asset Creation tool, Dominic sets up an asset definition which creates a set of 100 coupons using the following details:

Asset Type:						Coupon
Asset Code:						DOMsPIZZA01swj5sjLP93bQufanHl7NJ
Asset Auth Flags:				Issuer can amend all fields
Transfers Permitted:			True - Users can send the coupon to other users
Enforcement orders permitted:	True - Enabled in case of vouchers being incorrectly distributed
Token Qty:						100
Asset Payload -					Version: 			0
								Redeeming entity:	Dominic's Pizza
								Issue Date:			Today's date
								Expiry Date:		6 months from today
								Description:		One free slice of any pizza

Once Dominic has finished entering the details he instructs his wallet to send the Asset Definition to the smart contract.

The smart contract receives the transaction and unpacks the details. After making sure that the details are valid, the smart contract responds with an Asset Creation action which generates the 100 coupons and gives them to Dominic's wallet. He now has 100 Free Slice coupons which he can hand out to customers as he sees fit.

/// ASSET CREATION

Next Dominic establishes a loyalty coupon which he will hand out with each slice. His plan is to give away a free slice of pizza to any customer who has bought 7 slices, making the 8th slice free.

He uses the following details:

Asset Type:						Loyalty Point
Asset Code:						DOMsPIZZA0293bQswj5sjLPufanHl7NJ
Asset Auth Flags:				Issuer can amend all fields
Transfers Permitted:			False - Users cannot send the asset to accounts not controlled by the Issuer
Enforcement orders permitted:	True - Enabled in case of vouchers being incorrectly distributed
Token Qty:						10,000
Asset Payload -					Version: 			0
								Redeeming entity:	Dominic's Pizza
								Issue Date:			Today's date
								Expiry Date:		2 years from today
								Description:		Loyalty tokens

Once Dominic has finished entering the details he instructs his wallet to send the Asset Definition to the smart contract.

The smart contract receives the transaction and unpacks the details. After making sure that the details are valid, the smart contract responds with an Asset Creation action which generates the points and gives them to Dominic's wallet. He now has 10,000 loyalty points which he can hand out to customers. Because customers will give them back to him to redeem pizza, he only needs as many as might be outstanding at any time. The loyalty program is set to expire with the lease on his restaurant but Dominic plans to modify the asset when he extends so that the program is always in place.

### Doing Business
Dominic opens his store to great fanfare, and has customers lined up on his first night in business. At the door he has a sign instructing people who wish to receive loyalty points to download a Tokenized protocol compatible wallet. He recommends the Tokenized wallet, which uses handles as an address identifier, making it very simple.

His first customer (Harry) purchases a whole pizza and some drinks and asks to pay in eAUD. Dominic sets up the transaction using a Tokenized compatible POS which links to an NFC device on the counter. 
Dominic asks Harry to scan the NFC tag, which gives his handle to the POS system. Using an API, it retrieves an address and a UTXO linked to an address that holds EAUD and uses this to build the payment transaction, creating the following template:

/// TEMPLATE HERE
Transfer action
inputs: dominic's pizza (signed)
		Harry (1) (unsigned)
outputs:dominics pizza Contract 	(contract fees and response costs)
		eAUD Contract 				(contract fees)
		Harry(2) 					(dust)
		dominics pizza contract (intercontract messaging coin)
		<receipt>
		<transfer_action>

Using 		135.32 eAUD			from 	Harry (1)
transfer 	57.23	 			to 		Dominic's Pizza
transfer 	78.09	 			to 		Harry (2)

Using 		10,000 DOMsPIZZA...	from 	Dominic's Pizza
transfer 	1					to 		Harry (2)
transfer 	9999 				to 		Dominic's Pizza

Receipt:
1 Hawaiian Pizza 		$25
1 extra pineapple		$4
2 Craft Beer pint 		$12

1 Free Slice voucher 	Free
7 Dom's Loyalty Points 	Free

Dominic's system now sends this to Harry's wallet in a 'Signature Request' message action. Harry's wallet automatically sees the transaction come in and notifies him of its arrival. He looks at the receipt and the amounts he is transferring and he accepts. The wallet signs his input and sends the transaction onto the network.

/// insert image

The Dominic's Pizza contract sees the transaction arrive and unpacks it to make sure that it's valid. Seeing no issue, it creates a Settlement Action and sends it to the eAUD smart contract using a Message action. The eAUD smart contract checks Harry's balance and creates a transaction using the inputs sent to each contract in the transfer action, and sends this back to the Dominic's Pizza contract in a Signature Request message.

insert image

The Dominics pizza contract signs the transaction and sends it on to the network. Harry and Dominic's Pizza's wallets each see that the transaction has been settled and Harry is served his pizza.

