# Dominics Pizza Grand Opening

Dominic has spent the last 2 years planning for today. His restaurant fit out is complete, the mortar on his wood fired pizza ovens is dry, and his fridges are chilling a variety of bottled drinks.
The last thing on his list is to configure a smart contract for his membership program and a loyalty point system.
Dominic downloads the Tokenized Nexus wallet and installs it on his PC. He creates a new wallet and makes a safe backup of the master key, then begins configuring his Contract Offer.
Dominic has decided to give his first 100 customers a free slice of pizza for their next visit, and to establish a frequent slice program that gives customers one free slice for every 7 slices they buy.

### Creating the Contract

Dominic names his contract 'Dominic's Pizza Loyalty Program'. He has already prepared a set of terms and conditions for his contract, and has them saved in a PDF file. The PDF file and copies of the flier detailing his Frequent Slice program are stored in a 7Zip file ready to be attached to the contract. 
Using the Contract Creation tool, Dominic creates the following Contract Offer:

Now that Dominic has filled out all the details, he is ready to create his smart contract.

He does this by generating a Contract Offer transaction which it sends to the Tokenized Platform. For Tokenized to act as the contract operator, it is necessary for Tokenized to sign the Contract Offer, or it will be rejected by the smart contract. This process is handled between Dominic's app and the Tokenized server that runs the smart contract agent. When it receives the template Contract Offer, it creates a new address in a derivative of its own master address and gives the keys to an agent created to run Dominic's smart contract. It sends the Contract Offer to this address.

![Dominic's Pizza Contract Offer action](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-contract-offer.svg?sanitize=true "Dominic's Pizza Contract Offer") {.frame .centered .padded}

The Agent receives the Contract Offer and unpacks it, validating its contents before building a Contract Formation response. The contract formation contains all the same information received in the Contract Offer, plus a version indicator which is set to zero, and a Timestamp that is set to the time the transaction was created. It sends this onto the Bitcoin network where it is cleared to Dominic's wallet a few seconds later.

![Dominic's Pizza Contract Formation action](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-contract-formation.svg?sanitize=true "Dominic's Pizza Contract Formation") {.frame .centered .padded}

### Creating the assets
Now that Dominic's contract is live, he is able to use it to create the assets that he will use in his loyalty program.
Firstly, he has decided to create a 'Free Slice' coupon which he will give to the first 100 people who buy a whole pizza. He wants people to also have the option to send these coupons to other people so that they can come and try his food. Using the Asset Creation tool, Dominic sets up an asset definition which creates a set of 100 coupons using the following details:

![Dominic's Pizza Slice Coupon Asset Definition](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-slice-coupons-asset-definition.svg?sanitize=true "Dominic's Pizza slice coupons Asset Definition") {.frame .centered .padded}

Once Dominic has finished entering the details he instructs his wallet to send the Asset Definition to the smart contract.

The smart contract receives the transaction and unpacks the details. After making sure that the details are valid, the smart contract responds with an Asset Creation action which generates the 100 coupons and gives them to Dominic's wallet. He now has 100 Free Slice coupons which he can hand out to customers as he sees fit.

![Dominic's Pizza Slice Coupon Asset Creation](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-slice-coupons-asset-creation.svg?sanitize=true "Dominic's Pizza slice coupons Asset Creation") {.frame .centered .padded}

Next Dominic establishes a loyalty coupon which he will hand out with each slice. His plan is to give away a free slice of pizza to any customer who has bought 7 slices, making the 8th slice free.

He uses the following details:


![Dominic's Pizza loyalty points Asset Definition](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-loyalty-points-asset-definition.svg?sanitize=true "Dominic's Pizza loyalty points Asset Definition") {.frame .centered .padded}

Once Dominic has finished entering the details he instructs his wallet to send the Asset Definition to the smart contract.

The smart contract receives the transaction and unpacks the details. After making sure that the details are valid, the smart contract responds with an Asset Creation action which generates the points and gives them to Dominic's wallet. He now has 10,000 loyalty points which he can hand out to customers. Because customers will give them back to him to redeem pizza, he only needs as many as might be outstanding at any time. The loyalty program is set to expire with the lease on his restaurant but Dominic plans to modify the asset when he extends so that the program is always in place.

### Doing Business
Dominic opens his store to great fanfare, and has people lined up for his first night in business. 

His first customer (Harry) asks to purchase a hawaiian pizza with extra pineapple and two pints of Dominic's locally sourced craft beer, and asks to pay in eAUD. The process uses a point of sale protocol specifically for use in retail. The image below details the order of operations:

![Dominic's Pizza - Harry's transfer, order of operations](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-harry-transfer-order-of-operations.svg?sanitize=true "Dominic's Pizza - Harry's transfer, order of operations") {.frame .centered .padded}

This is the detail of the transfer operation which is sent to the network:

![Dominic's Pizza - Harry's transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/dominics-pizza-harry-transfer.svg?sanitize=true "Dominic's Pizza - Harry's transfer") {.frame .centered .padded}

The Dominic's Pizza contract sees the transaction arrive and unpacks it to make sure that it's valid. Seeing no issue, it creates a Settlement Action and sends it to the eAUD smart contract using a Message action. The eAUD smart contract checks Harry's balance and creates a transaction using the inputs sent to each contract in the transfer action, and sends this back to the Dominic's Pizza contract in a Signature Request message.

insert image

The Dominics pizza contract signs the transaction and sends it on to the network. Harry and Dominic's Pizza's wallets each see that the transaction has been settled and Harry is served his pizza.

