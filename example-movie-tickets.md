# Movie Tickets

- [Introduction](#introduction)
- [Booking](#booking)
  - [Pre-paid Ticket Transfer](#pre-paid-ticket-transfer)
  - [Pre-paid Ticket Settlement](#pre-paid-ticket-settlement)
- [Candy Bar](#candy-bar)
  - [Candy Bar Transfer](#candy-bar-transfer)
  - [Candy Bar Settlement](#candy-bar-settlement)
- [Pre-paid Item Redemption](#pre-paid-item-redemption)
  - [Pre-paid Item Transfer](#pre-paid-transfer)
  - [Pre-paid Item Settlement](#pre-paid-settlement)

<a name="introduction"></a>
## Introduction

Alice and her friends, Bob and Carol, have agreed to go to the latest hit movie at their local cinema.

<a name="booking"></a>
## Booking

Alice visits her local cinema's website and picks a session. The cinema has allocated seating, so for every showing, a ticket is created that is specific to a particular seat. The booking system allows Alice to see which seats are still available, and she picks 3 seats that are next to each other.
Alice also purchases a popcorn and soda combo for herself.

The cinema allows Alice to buy tickets for the others by sending tickets to separate wallets in the same transaction.  Since Alice is buying all the tickets for her group of friends, she enters in Bob and Carol's handles. She also allocates the snacks combo coupon token to her own wallet.

<a name="pre-paid-ticket-transfer"></a>
### Pre-paid Ticket Transfer

The cinema's website then builds a transaction template for a 'Transfer' action which sends the three seat tokens to each of Alice, Bob and Carol, the snack combo coupon to Alice, and payment in eAUD (Australian dollar currency token) to the cinema chain's wallet.\

![Cinema's transfer template](https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-template.svg?sanitize=true "Cinema's transfer template") {.frame .centered .padded}

Alice doesn't have any eAUD in her wallet at the moment, so her wallet sends a request to a company that offers BSV to eAUD exchanges as a service.  In response to her request, the exchange company sends her a quote for the exchange rate plus fees for the amount of eAUD she wants to buy with BSV, as well as the company's relevant addresses to facilitate the exchange. She presses accept and her wallet modifies the Transfer action template to include the exchange company's input and output addresses. This now means that the exchange's contract must also countersign the transaction as it has an input in the token transfer action.

![Alice's final transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-final.svg?sanitize=true "Alice's final transfer") {.frame .centered .padded}

Alice's wallet then signs the transaction for her inputs using SIGHASH_ALL and sends the partially-signed transaction to the exchange company. Once the exchange company has validated that the output matches its agreement with Alice, it signs for its input using SIGHASH_ALL and sends it to the cinema for the final signature. Once the cinema has validated Alice's modifications, it signs for the third and final input before sending the whole transaction to the Bitcoin SV network.

<a name="pre-paid-ticket-settlement"></a>
### Pre-paid Ticket Settlement

The two contracts involved (cinema ticketing contract and eAUD contract) both see the transfer request. Because it is the first output in the Transfer request, it is up to the cinema contract to build a template of the settlement transaction. The eAUD contract is well known and the cinema ticketing contract sends its template settlement directly to the contract via a known endpoint. In situations where two contracts don't know each other, the template can be delivered to the second contract using a 'Settlement Request' message contained in a Message action sent directly to the contract's on-chain address.

![Cinema's settlement template](https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-settlement-template.svg?sanitize=true "Cinema's settlement template") {.frame .centered .padded}

The eAUD contract receives the settlement action and fills in the details (eg. final settlement balances of eAUD for each of the addresses) left blank by the cinema before signing the transaction and sending it to the network.

![Final Settlement Transaction](https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-final-settlement.svg?sanitize=true "Final Settlement Transaction") {.frame .centered .padded}

When Alice's, Bob's and Carol's wallets all see the settlement transaction arrive, their token portfolio will be updated to say that they have now received a ticket to that evening's 6pm session of 'Funny Movie', and Alice's wallet also shows that she has a coupon for a 'Medium Popcorn/Soda Combo, Self Serve'.

<a name="candy-bar"></a>
## Candy Bar

Alice, Bob and Carol meet that evening at the cinema. The first thing they do is head to the candy bar.

Bob grabs a medium popcorn combo, and Carol a choc-top and they go to the counter. Their items have embedded RFID tags in the packaging so the system automatically detects the items they have selected and prepares a transfer request.

<a name="candy-bar-transfer"></a>
### Candy Bar Transfer

Carol has eAUD in an account in her Tokenized wallet so the transaction comes together quite simply. Carol provides an input from her eAUD wallet which links the transaction to the eAUD contract. Carols wallet sends a transaction including the template receipt it received from the cinema. 

![Candy Bar Final Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-transfer-final.svg?sanitize=true "Candy Bar Final Transfer") {.frame .centered .padded}

The eAUD Contract sees Carol's transfer action arrive in it's wallet and quickly validates the action. Carol has adequate money in her account so it prepares and sends the on-chain Settlement action.

<a name="candy-bar-settlement"></a>
### Candy Bar Settlement

![Candy Bar Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-settlement.svg?sanitize=true "Candy Bar Settlement") {.frame .centered .padded}

<a name="pre-paid-item-redemption"></a>
## Pre-paid Item Redemption

When Alice goes to the candy bar, she grabs her combo and heads to the checkout. It scans her items and aks Alice how she would like to pay. She selects the 'Pre-Purchased' option to use the coupon she purchased earlier with the tickets.

<a name="pre-paid-transfer"></a>
### Pre-paid Item Transfer

The cinema provides Alice with a template Transfer action including a receiving address and transfer action. This is delivered via NFC to her mobile device.

![Candy Bar Pre-Paid Item Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-transfer-template.svg?sanitize=true "Candy Bar Pre-Paid Item Transfer") {.frame .centered .padded}

Her wallet selects a cash input to pay for the transaction, creates the change output, then signs and broadcasts the Transfer action onwto the Bitcoin SV network.

![Final Candy Bar Pre-Paid Item Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-transfer-final.svg?sanitize=true "Final Candy Bar Pre-Paid Item Transfer") {.frame .centered .padded}

<a name="pre-paid-settlement"></a>
### Pre-paid Item Settlement

The cinema contract sees the Transfer action addressed to it and checks that the action is valid before proceeding to build a Settlement transaction. As only one contract is involved in this Settlement action, it can send this straight to the Bitcoin SV network. The snack combo coupon has been successfully transferred between Alice's wallet and the cinema's wallet as a redemption for the snacks Alice purchased.

![Final Candy Bar Pre-Paid Item Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-settlement.svg?sanitize=true "Final Candy Bar Pre-Paid Item Settlement") {.frame .centered .padded}
