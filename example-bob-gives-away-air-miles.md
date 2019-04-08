# Transferring tokens

Bob is a frequent flyer of TokenAir for his work and has managed to rack up 4,000,000 air miles, but cannot stand the idea of flying to a holiday destination.

His sister Dianne has never been on a plane so Bob gifts her 2,000,000 air miles to spend on her first overseas holiday.

The conditions of Bob's contract with TokenAir are that he may only pass his miles onto direct family members so before Dianne can receive the miles, she must register with TokenAir's whitelist and establish a family tie to Bob. Bob's airline wallet won't even allow him to build a transfer action with Dianne as the receiver until this is complete.

This is done by Bob contacting the TokenAir registry and supplying the necessary information about Dianne and registering her as his Family member. The registry adds an entry linking Bob and Dianne together as authorised recipients of each other's air miles.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/bob-dianne-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

Now that Bob and Dianne are linked by TokenAir's registry, he is free to transfer Dianne his airline miles.
He does this using his mobile phone app, which now allows him to add Dianne as a recipient when he creates the transfer request.
The app communicates with the TokenAir Points manager back end which is the issuer of the airline mile tokens. TokenAir also run their own instance of the Tokenized platform making them an Issuer/Operator in one. 
Because there is only one contract involved, and Bob has all the details of the transaction including Dianne's receiving address, he can build, sign and send the complete transfer request without having to template anything.

/// INSERT IMAGE

When Dianne opens her TokenAir wallet, it how shows that she has received 2,000,000 air mile tokens from Bob.

Dianne wants to use the points for a trip with her husband Edward and daughter Fran so she accesses the registry site and adds the pair to her family.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-edward-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/dianne-fran-family-addition-action.svg?sanitize=true" alt="Adding a family link" align="middle">

She selects 'Book Travel' in the interface and selects a packaged holiday to Fiji including flights, transfers and hotels. The app uses APIs to feed hotel booking data into the transaction as needed. The total cost of the holiday is 2,400,000 points so Dianne elects to use 'Points + Pay' and to pay the difference using some Bitcoin that Bob gave her a few years earlier.
The hotel that Dianne has booked uses its own smart contract to manage room bookings and transfers, but it has a contract with TokenAir that guarantees them a cash value for the tokens.
TokenAir's app builds a template transfer action for Dianne to sign and sends it to her in a Message action using the 'Offer' message type.
The transfer takes Dianne's 2,000,000 air miles and 0.2324 Bitcoins and distributes them to the hotel and itself. In return, it gives Dianne 3 return tickets to Fiji valid for their selected flights, including bonus Lounge entry coupons.
The hotel contract also gives Dianne an ACC (accomodation) token for 7 nights accomodation in a family suite which is valid for the nights of her stay. Included with this are 7 breakfast coupons, a spa coupon, 3 golf coupons, three luxury dinner package coupons (one each) and membership to the Hotel Rewards scheme for all three family members.

/// INSERT IMAGE

Happy with the deal, Dianne fills in the blank information before signing the transaction and sending it on to the Hotel in a Message action using the 'Signature Request' message type.

/// INSERT IMAGE

The hotel sees the transaction and double checks the figures, before signing and sending the contract back to TokenAir for final signature. Once TokenAir receives the transaction, it checks that the details match what it gave to Dianne, signs and sends onto the network.

Once the transaction has been sent to the blockchain, the TokenAir smart contract pulls open the transaction and checks that it is valid. Once it has determined that the contract can go ahead, it prepares a settlement action. In this it shows that it will award 1.2 million air miles to the hotel, and send three return tickets to each of Dianne, Edward and Fran. It pre-fills the distribution of the room stay, meal and activity vouchers and airport bus transfers into the transfer action and sends the settlement template to the Hotel smart contract for signature. Because they share an API they are able to do this without spending an on-chain transaction.