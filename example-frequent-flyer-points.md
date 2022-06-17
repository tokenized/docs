# Frequent Flyer

- [Introduction](#introduction)
- [Oracle Registry](#oracle-registry)
- [Points Transfer](#points-transfer)
- [Holiday Booking](#holiday-booking)
	- [Transfer Process](#transfer-process)
	- [Settlement](#settlement)

<a name="introduction"></a>
## Introduction

Bob is a travelling salesman and a frequent flyer of TokenAir.  Over the last few years he has managed to rack up 4,139,332 frequent flyer points but, unfortunately, he cannot stand the idea of flying in his free time.

His sister Dianne has never been on a plane so Bob gifts her 2,000,000 frequent flyer points to spend on her first overseas holiday.

<a name="identity-oracle"></a>
## Identity Oracle

TokenAir uses a smart contract to manage the frequent flyer points program and uses the Loyalty Points (LOY) instrument type for its tokens.  The smart contract is called the TokenAir Frequent Flyer contract.  The conditions of the smart contract prevent Bob from transferring his points to addresses that have not been linked to verified real world identities and the contract uses an Identity Oracle to enforce the rule.

An Identity Oracle is a service run by a 3rd party that verifies peoples' identities and links those identities to Bitcoin addresses.  This allows contract administrations to outsource the user identity verification process for their smart contracts.  For Transfer actions that send tokens to a certain address, the smart contract requires authorization from an Identity Oracle.  This authorization comes in the form of a signed message that includes the recipient's address, the InstrumentID, the Contract Address and a permission flag. A user's wallet would request a signed message from the Identity Oracle for an intended token transfer.  The Identity Oracle would check to see if the receiving address is valid in comparison to the terms and conditions of the contract with respect to the identity they have on their records.  The Identity Oracle then sends (off-chain) either a permission granted signed message or a permission denied signed message.  If it was a permission granted then the user would include the signed message in the Transfer action so that the smart contract could verify it.

The TokenAir frequent flyer smart contract uses the company 'Identity Services' as the Identity Oracle.  Dianne registers with Identity Services and goes through their identity verification process.  She also sumbits one of her extended public keys to them and they link her identity to the addresses generated from it.

<a name="points-transfer"></a>
## Points Transfer

Now that Dianne is registered with the Identity Oracle, she can receive the frequent flyer points from Bob.  Bob selects Dianne as a recipient in his wallet and chooses to send 2,000,000 frequent flyer points. Because there is only one contract involved, and Bob has all the details of the transaction including Dianne's receiving address, he can build, sign and send the complete Transfer action without input from any other entity except the Identity Oracle.

![Bob's Airmile Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/bob-airmile-transfer-final.svg?sanitize=true "Bob's Airmile Transfer") {.frame .centered .padded}

The TokenAir smart contract receives the action and unpacks it. After validating the transaction, including the signed message from the Identity Oracle, it broadcasts a Settlement action to complete the transfer of frequent flyer points.

![Bob's Airmile Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/bob-airmile-settlement-final.svg?sanitize=true "Bob's Airmile Settlement") {.frame .centered .padded}

When Dianne opens her wallet, it now shows that she has received 2,000,000 frequent flyer points from Bob.

<a name="holiday-booking"></a>
## Holiday Booking

Dianne wants to use the points for a trip with her husband Edward and daughter Fran. To book her holiday, she goes to TokenAir's online booking service and selects the package holiday she is interested in.  The package is a trip holiday to Fiji including flights, 7 nights at Fiji by the Sea hotel, and a few coupons for meals, activities and services. The app uses APIs to feed hotel booking data into the transaction as needed. The total cost of the holiday is 2,400,000 points so Dianne decides to pay the difference with Bitcoin. She selects 'Points + Pay' in the interface and selects 'Bitcoin' as the currency.

Fiji by the Sea has its own smart contract to manage room bookings and coupons. TokenAir also uses smart contracts to manage their airline tickets. TokenAir also has a separate business arrangement with Fiji by the Sea and acts as a reseller for them.

<a name="transfer-process"></a>
### Transfer Process

TokenAir's app requests an input from Fiji by the Sea hotel and uses it to build a template Transfer action for Dianne to sign. It delivers this directly to her wallet.

The summary of the Transfer action sends 2 million of Dianne's frequent flyer points plus 0.2324 Bitcoins to TokenAir. In return, it gives Dianne 3 return business class tickets to Fiji, 1 coupon for an oversized check in baggage for Edward's golf bag, 6 lounge entry coupons (2 each), accomodation tokens for 7 nights in a family suite, 21 coupons for breakfast at the hotel, a coupon for a spa session for herself, 3 coupons for a round of golf for Edward, kids club entry for three days for Fran, and three gourmet dinner package coupons (one per family member).

![Dianne's Holiday Booking Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-transfer-template.svg?sanitize=true "Dianne's Holiday Booking Transfer") {.frame .centered .padded}

Happy with the deal, Dianne decides to accept. Her wallet adds her input(s) and change output required to pay the 0.2324BSV owing. Her wallet then signs the transaction and sends it back to the TokenAir token sending address in a 'Signature Request' message. TokenAir reviews the Transfer action and adds its signature before sending the fully-signed Transfer action to the Bitcoin SV network.

![Multi-User Transfer Request Order of Operations](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-booking-multi-user-signature-order-of-operations.svg?sanitize=true "Multi-User Transfer Signature Order of Operations") {.frame .centered .padded}

As soon as the two contracts see the Transfer action enter the network, they unpack the transaction and check that everything matches what they expect. 

<a name="settlement"></a>
### Settlement

As part of the Transfer action, Dianne's wallet includes a second output to the TokenAir Frequent Flyer contract, which is for inter-contract communication during the settlement process. 

The TokenAir Frequent Flyer contract constructs a Settlement action and includes settlement balances of the frequent flyer points being transferred which it controls, and packages this into a 'Settlement Request' Message action, which it sends on to the TokenAir Airline Ticketing contract. As part of this message, the Intercontract Messaging Fee is used as the funding input, and its full remaining value is passed on as the only monetary output in the transaction. The TokenAir Booking contract adds a monetary input and the settlement balances for the flight tokens and hotel coupons to the partially built payload, signs its input and uses the Inter-Contract Messaging Fee to send the partially-signed transaction back to the TokenAir Frequent Flyer contract in a 'Signature Request' Message action.

![Dianne's Holiday Booking settlement creation process](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-holiday-multi-contract-settlement-process.svg?sanitize=true "Dianne's Holiday Booking settlement creation process") {.frame .centered .padded}

The TokenAir Frequent Flyer contract signs the final input and sends the transaction onto the Bitcoin network for settlement.

![Dianne's Holiday final settlement, fully signed](https://raw.githubusercontent.com/tokenized/docs/master/images/diannes-holiday-final-settlement.svg?sanitize=true "Dianne's Holiday final settlement, fully signed") {.frame .centered .padded}
