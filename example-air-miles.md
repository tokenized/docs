# Transferring tokens

Bob is a frequent flyer of TokenAir for his work and has managed to rack up 4,139,332 air miles, but cannot stand the idea of flying to a holiday destination.

His sister Dianne has never been on a plane so Bob gifts her 2,000,000 air miles to spend on her first overseas holiday.

The conditions of Bob's contract with TokenAir are that he may only pass his miles onto direct family members so before Dianne can receive the miles, she must register with TokenAir's whitelist and establish a family tie to Bob. Bob's airline wallet won't even allow him to build a transfer action with Dianne as the receiver until this is complete.

This is done by Bob contacting the TokenAir registry and supplying the necessary information about Dianne and registering her as his Family member. The registry adds an entry linking Bob and Dianne together as authorised recipients of each other's air miles.

![Adding a family link](https://raw.githubusercontent.com/tokenized/docs/master/images/bob-dianne-family-addition-action.svg?sanitize=true "Adding a family link") {.frame .centered .padded}

Now that Bob and Dianne are linked by TokenAir's registry, he is free to transfer Dianne his airline miles.
He does this using his mobile phone app, which now allows him to add Dianne as a recipient when he creates the transfer request.
The app communicates with the TokenAir Points manager back end which is the issuer of the airline mile tokens. TokenAir also run their own instance of the Tokenized platform making them an Issuer/Operator in one.

Now that Bob has registered Dianne as his family member, he is able to reach out to the TokenAir Air Mile Transfer Authorisation Server Oracle (AMTAS Oracle) and get an authorisation to transfer tokens to Dianne. This comes in the form of a signed, limited lifetime message which Bob includes in the transfer action which he sends to the smart contract. Bob's app is connected to AMTAS, and handles this with minimal interface from Bob, and then caches the message, which expires in 48 hours.

Because there is only one contract involved, and Bob has all the details of the transaction including Dianne's receiving address, he can build, sign and send the complete transfer request without having to template anything. The TokenAir system includes a message action with the transfer as a record of exactly what was exchanged with whom, including details from the TokenAir oracle about the transfer approval.

![Bob's Airmile Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/bob-airmile-transfer-final.svg?sanitize=true "Bob's Airmile Transfer") {.frame .centered .padded}

The TokenAir smart contract receives the action and unpacks it. After validating the signed

When Dianne opens her TokenAir wallet, it how shows that she has received 2,000,000 air mile tokens from Bob.

Dianne wants to use the points for a trip with her husband Edward and daughter Fran so she accesses the registry site and adds the pair to her family.

![Adding Edward](https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-edward-family-addition-action.svg?sanitize=true "Adding Edward") {.frame .centered .padded}

![Adding Fran](https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-fran-family-addition-action.svg?sanitize=true "Adding Fran") {.frame .centered .padded}

She selects 'Book Travel' in the interface and selects a packaged holiday to Fiji including flights, transfers and 7 nights at Fiji by the sea hotel. The app uses APIs to feed hotel booking data into the transaction as needed. The total cost of the holiday is 2,400,000 points so Dianne decides to pay using some Bitcoin that Bob gave her some years ago. She selects 'Points + Pay' in the interface and selects 'Bitcoin' as the currency. 
The TokenAir ticketing contract is able to use points plus pay for ticket payment, and the hotel has its own smart contract to manage room bookings and transfers. Through a separate agreement with TokenAir the Hotel is able to exchange the air miles for a guaranteed cash value so Dianne is allowed to pay forthe hotel in air miles.
TokenAir's app requests an input from Fiji by the sea hotel and uses it to build a template transfer action for Dianne to sign. It delivers this directly to her wallet.
The transfer sends 1.2 million of Dianne's air miles to the hotel, and the remaining 800,000 air miles plus 0.2324 Bitcoins to TokenAir. In return, it gives Dianne 3 return tickets, business class, to Fiji valid for their selected flights, check in baggage for each flight plus golf bag for Edward, lounge entry coupons, accomodation tokens for 7 nights in a family suite, 7 breakfast coupons each, a spa coupon for herself, 3 golf coupons for Edward, Kids club entry for three days for Fran, three gourmet dinner package coupons (one per family member) and membership to the Hotel Rewards scheme for all three family members.

![Dianne's Holiday Booking Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-transfer-template.svg?sanitize=true "Dianne's Holiday Booking Transfer") {.frame .centered .padded}

Happy with the deal, Dianne decides to accept. To use air miles for Edward and Fran's bookings, Dianne must receive permission from the AMTAS oracle. This is handled automatically by Dianne's wallet which gets the signed message before gathering 10 UTXOs it needs to pay the 0.2324BSV owing and adding them to the input list. It then signs the transaction and sends it to the TokenAir Air Miles contract in a 'Signature Request' message. The output to TokenAir includes enough cash value for TokenAir to on-send the signed Transfer action to Fiji by the sea Hotel for the final signature.
TokenAir signs its output, then sends the transaction as a Signature Request payload to Fiji by the sea hotel. Fiji by the sea also sign the transaction and send it onto the network.

![Multi-Contract Signature Request Order of Operations](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-multicontract-signature-order-of-operations.svg?sanitize=true "Multi-Contract Signature Request Order of Operations") {.frame .centered .padded}

As soon as the three contracts see the Transfer action enter the network, they unpack the order and check that everything matches what they expect. In particular, the TokenAir contract inspects the messages signed by the AMTAS oracle to ensure that they are valid, unexpired and contain authorisations for the addresses used in the transfer action. Once this has been verified, it begins the process of preparing a Settlement action.
As part of the transfer order, Dianne's wallet includes a second output to the TokenAir Air Miles contract, which is for inter-contract communication during the settlement process. The TokenAir Air Miles contract knows which output this is as it is the first output that is not referenced in the Transfer action payload.
It constructs a Settlement Action including all the assets being transferred which it controls, and packages this into a 'Settlement Request' Message action, which it sends on to the TokenAir Bookings contract. As part of this message, the Intercontract Messaging Coin is used as the funding input, and the full change value as the only monetary output. The TokenAir Bookings contract appends it's settlement information to the partially built payload, and forwards it in a second 'Settlement Request' message to the Fiji by the sea Hotel contract. 
The Fiji by the sea Hotel contract adds the remainder of the settlement items to the list and finalises the settlement action by adding a timestamp. It then uses the three contract outputs from the Transfer action and builds the full Settlement transaction. Included in the Settlement Request action are the necessary fees and output addresses to be paid to the contract operators, and the Fiji by the sea hotel contract uses these in its template.
Once complete, it signs its own input and uses the Inter-Contract messaging coin to send the incomplete transaction back to the TokenAir Booking contract in a 'Signature Request' Message action.
The TokenAir booking contract receives the partially signed message and adds its own signature before passing it on to the TokenAir Air Miles contract for the final signature.

![Dianne's Holiday Booking settlement creation process](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-holiday-multi-contract-settlement-process.svg?sanitize=true "Dianne's Holiday Booking settlement creation process") {.frame .centered .padded}

Now that the transaction is fully complete, the TokenAir Air Miles contract sends it onto the Bitcoin network for settlement.

![Dianne's Holiday final settlement, fully signed](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-holiday-final-settlement.svg?sanitize=true "Dianne's Holiday final settlement, fully signed") {.frame .centered .padded}
