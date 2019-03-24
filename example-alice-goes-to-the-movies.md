#Example: Alice Goes to the Movies
Alice and her friends Bob and Carol have agreed to go to the latest hit movie at their local gigaplex.
Alice visits her local cinema and picks a session. The cinema has allocated seats, so for every showing, a ticket is created that is specific to a particular seat. Alice is able to see using the booking system which seats are still available, and is able to pick 3 seats that are next to each other.
Because she likes snacks, Alice also purchases a Popcorn/soda combo for herself. 

The cinema allows Alice to send each of the tickets to a separate wallet, so she enters the handles for Bob and Carol. She also allocates the combo token to her own wallet.

The cinema's interface now builds a transaction template for a 'Transfer' action which sends the three seat tokens to each of Alice, Bob and Carol, the snack combo to Alice, and payment in eAUD (an Australian dollar pegged currency token) to the cinema chain's wallet. The cinema chain generates a new address for each AUD receipt, and aggregates them as needed for its outgoing accounts.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-template.svg?sanitize=true" alt="Cinema's transfer template">

Alice doesn't have any eAUD so her wallet sends a request to her bank's exchange contract requesting a price for the exact amount in AUD. The bank gives her a price, an exchange fee and an address and amount for her to send Bitcoin to, which her wallet inserts into the transaction. This now means that the exchange's contract must also countersign the transaction as it has an output in the token transfer action.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-transfer-final.svg?sanitize=true" alt="Alice's final transfer">
 Alice's wallet then signs her inputs using SIGHASH_ALL and sends the transaction to the exchange. Once the exchange has validated that the output matches its agreement with Alice, it signs its input using SIGHASH_ALL and sends it to the Cinema for final signing. once the Cinema has validated Alice's modifications, it signs the third and final input before passing the whole transaction to the mining network. 

The two contracts involved (Cinema and AUD) both see the transfer request. Because it is the first output in the Transfer request, it is up to the Cinema contract to build a template of the settlement transaction. The AUD contract is well known and the Cinema contract sends its template settlement directly to the contract via an API. In situations where two contracts don't know each other, the template can be delivered to the second contract using an M1 Message action direct to the contract's address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/cinema-settlement-template.svg?sanitize=true" alt="Cinema's settlement template">
The AUD contract receives the settlement action and enters it's own  
