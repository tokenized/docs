# Example: Alice Goes to the Movies

Alice and her friends Bob and Carol have agreed to go to the latest hit movie at their local gigaplex.

Alice visits her local cinema and picks a session. The cinema has allocated seats, so for every showing, a ticket is created that is specific to a particular seat. Alice is able to see using the booking system which seats are still available, and is able to pick 3 seats that are next to each other.
Because she likes snacks, Alice also purchases a Popcorn/soda combo for herself.

The cinema allows Alice to send each of the tickets to a separate wallet, so she enters the handles for Bob and Carol. She also allocates the combo token to her own wallet.

The cinema's interface now builds a transaction template for a 'Transfer' action which sends the three seat tokens to each of Alice, Bob and Carol, the snack combo to Alice, and payment in eAUD (Australian dollar currency token) to the cinema chain's wallet. The cinema chain generates a new address for each eAUD receipt, and aggregates them as needed for its outgoing accounts.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-template.svg?sanitize=true" alt="Cinema's transfer template" align="middle">

Alice doesn't have any eAUD so her wallet sends a request to her bank's exchange contract requesting a price for the exact amount in eAUD. The bank gives her a price, an exchange fee and an address and amount for her to send Bitcoin to, which her wallet inserts into the transaction. This now means that the exchange's contract must also countersign the transaction as it has an output in the token transfer action.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-final.svg?sanitize=true" alt="Alice's final transfer" align="middle">

Alice's wallet then signs her inputs using SIGHASH_ALL and sends the transaction to the exchange. Once the exchange has validated that the output matches its agreement with Alice, it signs its input using SIGHASH_ALL and sends it to the Cinema for final signing. once the Cinema has validated Alice's modifications, it signs the third and final input before passing the whole transaction to the mining network.

The two contracts involved (Cinema and eAUD) both see the transfer request. Because it is the first output in the Transfer request, it is up to the Cinema contract to build a template of the settlement transaction. The eAUD contract is well known and the Cinema contract sends its template settlement directly to the contract via an API. In situations where two contracts don't know each other, the template can be delivered to the second contract using an M1 Message action direct to the contract's address.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-settlement-template.svg?sanitize=true" alt="Cinema's settlement template" align="middle">

The eAUD contract receives the settlement action and fills in the details left blank by the cinema before signing the transaction and sending it to the network.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-final-settlement.svg?sanitize=true" alt="Final Settlement Transaction" align="middle">

When Alice's, Bob's and Carol's wallets all see the settlement transaction arrive, their token portfolio will be updated to say that they have now received a ticket to that evening's 6pm session of 'Funny Movie', and Alice's wallet also shows that she has a voucher for a 'Medium Popcorn/Soda Combo, Self Serve'.

Alice, Bob and Carol meet that evening at the Gigaplex. The first thing they do is head to the Candy Bar.

Bob grabs a medium Popcorn combo, and Carol a choc-top and they go to the counter. Their items have embedded RFID tags in the packaging so the system automatically detects the items they have selected and prepares a transfer request. The kiosk asks Carol if she would like a receipt for an extra $0.01 and she selects Yes.
The cinema prepares both a Transfer template and a Message action including Carol's receipt. 

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-transfer-template.svg?sanitize=true" alt="Candy Bar Transfer Template" align="middle">

Carol has eAUD in an account in her Tokenized wallet so the transaction comes together quite simply. Carol provides an input from her eAUD wallet which links the transaction to the eAUD contract. Carols wallet sends a transaction including the template receipt it received from the Cinema. 

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-transfer-final.svg?sanitize=true" alt="Candy Bar Final Transfer" align="middle">

The eAUD Contract sees Carol's transfer action arrive in it's wallet and quickly validates the action. Carol has adequate money in her account so it prepares the settlement.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-settlement.svg?sanitize=true" alt="Candy Bar Settlement" align="middle">

When Alice goes to the candy bar, she grabs her combo and heads to the checkout. It scans her items and offers a pre-built transaction, but alice selects the 'Pre-Purchased' option.

The system creates a transfer template that requests the pre-purchased items be delivered to a purchased item wallet which is received into Alice's wallet via NFC.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-transfer-template.svg?sanitize=true" alt="Candy Bar Pre-Paid Item Transfer" align="middle">

Her wallet completes the transfer and sends it to the Cinema contract.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-transfer-final.svg?sanitize=true" alt="Final Candy Bar Pre-Paid Item Transfer" align="middle">

The cinema contract checks that the items are valid and builds a settlement transaction. As no cash is changing hands, it can send this straight onto the network. The combo item is sent back into the same wallet as it was delivered from.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/candy-bar-pre-paid-settlement.svg?sanitize=true" alt="Final Candy Bar Pre-Paid Item Settlement" align="middle">
