# Transferring tokens

Bob is a frequent flyer of TokenAir for his work and has managed to rack up 4,139,332 air miles, but cannot stand the idea of flying to a holiday destination.

His sister Dianne has never been on a plane so Bob gifts her 2,000,000 air miles to spend on her first overseas holiday.

The conditions of Bob's contract with TokenAir are that he may only pass his miles onto direct family members so before Dianne can receive the miles, she must register with TokenAir's whitelist and establish a family tie to Bob. Bob's airline wallet won't even allow him to build a transfer action with Dianne as the receiver until this is complete.

This is done by Bob contacting the TokenAir registry and supplying the necessary information about Dianne and registering her as his Family member. The registry adds an entry linking Bob and Dianne together as authorised recipients of each other's air miles.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/bob-dianne-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

Now that Bob and Dianne are linked by TokenAir's registry, he is free to transfer Dianne his airline miles.
He does this using his mobile phone app, which now allows him to add Dianne as a recipient when he creates the transfer request.
The app communicates with the TokenAir Points manager back end which is the issuer of the airline mile tokens. TokenAir also run their own instance of the Tokenized platform making them an Issuer/Operator in one.

Now that Bob has registered Dianne as his family member, he is able to reach out to the TokenAir Air Mile Transfer Authorisation Server Oracle (AMTAS Oracle) and get an authorisation to transfer tokens to Dianne. This comes in the form of a signed, limited lifetime message which Bob includes in the transfer action which he sends to the smart contract. Bob's app is connected to AMTAS, and handles this with minimal interface from Bob, and then caches the message, which expires in 48 hours.

Because there is only one contract involved, and Bob has all the details of the transaction including Dianne's receiving address, he can build, sign and send the complete transfer request without having to template anything. The TokenAir system includes a message action with the transfer as a record of exactly what was exchanged with whom, including details from the TokenAir oracle about the transfer approval.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/bob-airmile-transfer-final.svg?sanitize=true" alt="Bob's Airmile Transfer" align="middle">

The TokenAir smart contract receives the action and unpacks it. After validating the signed

When Dianne opens her TokenAir wallet, it how shows that she has received 2,000,000 air mile tokens from Bob.

Dianne wants to use the points for a trip with her husband Edward and daughter Fran so she accesses the registry site and adds the pair to her family.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-edward-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-fran-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

She selects 'Book Travel' in the interface and selects a packaged holiday to Fiji including flights, transfers and 7 nights at Fiji by the sea hotel. The app uses APIs to feed hotel booking data into the transaction as needed. The total cost of the holiday is 2,400,000 points so Dianne decides to pay using some Bitcoin that Bob gave her some years ago. Sh selects 'Points + Pay' in the interface and selects 'Bitcoin' as the currency. 
The hotel uses its own smart contract to manage room bookings and transfers, and through a separate agreement with TokenAir is able to exchange the air miles for a guaranteed cash value.
TokenAir's app requests an input from Fiji by the sea hotel and uses it to build a template transfer action for Dianne to sign. It delivers this directly to her wallet.
The transfer sends 1.2 million of Dianne's air miles to the hotel, and the remaining 800,000 air miles plus 0.2324 Bitcoins to TokenAir. In return, it gives Dianne 3 return tickets, business class, to Fiji valid for their selected flights, check in baggage for each flight plus golf bag for Edward, lounge entry coupons, accomodation tokens for 7 nights in a family suite, 7 breakfast coupons each, a spa coupon for herself, 3 golf coupons for Edward, Kids club entry for three days for Fran, three gourmet dinner package coupons (one per family member) and membership to the Hotel Rewards scheme for all three family members.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-transfer-template.svg?sanitize=true" alt="Dianne's Holiday Booking Transfer" align="middle">

Happy with the deal, Dianne decides to accept. To use air miles for Edward and Fran's bookings, Dianne must receive permission from the AMTAS oracle. This is handled automatically by Dianne's wallet which gets the signed message before gathering 10 UTXOs it needs to pay the 0.2324BSV owing and adding them to the input list. It then signs the transaction and sends it to Fiji by the sea for their signature.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-transfer-signed.svg?sanitize=true" alt="Dianne's Holiday Booking Transfer, with Dianne's signature" align="middle">

Fiji by the sea looks at the contract and signs it's input before sending it to TokenAir for the final signature and transmission to the network.

As soon as the two contracts see the Transfer action enter the network, they unpack the order and check that everything matches what they expect. In particular, the TokenAir contract inspects the messages signed by the AMTAS oracle to ensure that they are valid, unexpired and contain authorisations for the addresses used in the transfer action. Once this has been verified, it prepares a Settlement action for both itself and the Fiji by the sea hotel contract to sign. Once complete, it signs the template and delivers it to the Fiji by the sea hotel contract.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-settlement-template.svg?sanitize=true" alt="Dianne's Holiday Booking settlement, with TokenAir's signature" align="middle">

The hotel sees the transaction and double checks the figures, before signing and sending the contract onto the network. 

Dianne, Edward and Fran simultaneously receive all of their tokens for the upcoming holiday.