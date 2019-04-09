## Transfers
The Transfer action is the means by which all asset transfers (Outside of enforcement actions) are conducted. The action is versatile and allows assets to be transferred between multiple holders and across multiple smart contracts. The following outlines the main ways in which the Transfer action is used.

1. [Transferring tokens to a single receiver](#single-receiver)
2. [Transferring tokens to a multiple receivers](#multiple-receiver)
3. [Purchasing tokens with bitcoin](#exchange)
4. [Cross contract atomic swaps](#atomic-swaps)

<a name="single-receiver"></a>
### Transferring Tokens to a Single Receiver

The act of transferring tokens can become fairly complicated when there are multiple parties and contracts involved, however, the final outcome is always captured in just two on-chain transactions:

1. Transfer action (Request)
2. Settlement action (Response)

In its simplest form, a transfer is an action between 2 parties which is validated by a smart contract.
In this example, a token issuer will send 100 tokens from its own balance to a receiver. This event is initiated by the issuer through the creation of a Transfer action detailing the receiver's address and the number of tokens they wish to send.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/one-receiver-transfer-example.svg?sanitize=true" alt="A basic transfer action" align="center" align="middle"></p>
<br>
The smart contract receives the request into its wallet and validates that it meets all of the terms and conditions for transfers on the contract. Once evaluated, the contract then builds a Settlement action in response and sends it onto the network.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/one-receiver-settlement-example.svg?sanitize=true" alt="A basic transfer action" align="center" align="middle"></p>
<br>
<a name="multiple-receiver"></a>
### Transferring Tokens to Multiple Receivers
Similarly, for an issuer to distribute tokens to more than one person, the transfer is a 2 step process. 
In this example, the issuer will now send an additional 100 tokens to the receiver from the example above (receiver 1), and 300 tokens to a second receiver (receiver 2).
Note that the transfer action deals with the number of tokens being sent, but the settlement transaction deals with the final balances of each account.
First, the issuer builds a transfer request detailing the number of tokens to be sent and the addresses to send them to:
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/two-receivers-transfer-example.svg?sanitize=true" alt="A two receiver transfer action" align="center" align="middle"></p>
<br>
Next, once the smart contract has checked everything is ok, it sends a settlement transaction that updates the balances of any wallets involved in the transaction.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/two-receivers-settlement-example.svg?sanitize=true" alt="A two receiver settlement action" align="center" align="middle"></p>
<br>
<a name="exchange"></a>
### Purchasing Tokens with Bitcoin (Exchange via Transfer Action)
The purchase of tokens with Bitcoin is a slightly more complicated interaction as it requires that the Transfer action be signed by two parties before it can be sent onto the network.
This would typically work by the token purchaser entering into an exchange interface or shopfront, and selecting the tokens that they wish to purchase. Typically, the interface will provide them with a cost for the tokens, with a time limit to finalize the purchase at the proposed price.
When the user has assembled the information for their purchase, they are sent a Message action which contains an 'Offer' message type. This includes a transaction template that contains the details of the seller, the amount they are to pay, the asset and the smart contract that will settle the transaction.
<br><br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-offer-message.svg?sanitize=true" alt="Transfer request template sent in Message action to purchaser" align="center" align="middle"></p>
<br>
Depending on the exchange used, there may be additional BSV outputs for the cost of performing the exchange. These details will also be included in the Transfer template. If the buyer changes the contents of the transaction, the exchange can simply elect not to sign, invalidating the transaction.
If the buyer is happy with the proposed exchange, they add appropriate Bitcoin inputs to the transaction, insert their token receiving address into the appropriate locations, and sign the transaction, sending the template back to the Smart Contract in a 'Signature Request' message.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-signature-request-message.svg?sanitize=true" alt="Transfer template sent in Message action to Merchant/Exchange for final signature" align="center" align="middle"></p>
<br>
Once the seller-signed transatction has been received by the merchant/exchange, they have one final opportunity to verify that the contents remain in-line with what they agreed to with the buyer, and can sign and transmit the transaction to the Bitcoin network. 
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-example.svg?sanitize=true" alt="Final Transfer request signed by buyer and seller" align="center" align="middle"></p>
<br>
Because only one smart contract is involved, the exchange settlement can be built and sent directly by the smart contract.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-settlement-example.svg?sanitize=true" alt="Exchange settlement" align="center" align="middle"></p>
<br>
<a name="atomic-swaps"></a>
### Atomic Swaps
Conducting an atomic swap (token for token transfer) using Tokenized is another more complicated transaction as it requires the holders of the tokens being exchanged to sign the Transfer action, and for both smart contracts to sign the Settlement action.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-process-order-of-operations.svg?sanitize=true" alt="Atomic Swap Transfer Order of Operations" align="center" align="middle"></p>
<br>
To begin, the two token holders agree to a transaction between themselves. The first token holder builds a partially complete transaction template which has the full details of the exchange except for the second party's receiving addresses and UTXO commitment. This is sent to the second party as a serialized partial transaction inside a Message action, using message type 1001 (Offer).
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-offer-message.svg?sanitize=true" alt="Atomic Swap Transfer Offer Message" align="center" align="middle"></p>
<br>
The second party then fills in the missing details and signs the transaction before sending it back to the first party in another message using message type 1002 (Signature Request).
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-signature-request-message.svg?sanitize=true" alt="Atomic Swap Transfer Signature Request" align="center" align="middle"></p>
<br>
The first user then countersigns and sends the transaction to the Bitcoin network.
<br><br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-action.svg?sanitize=true" alt="Atomic Swap Transfer Action" align="center" align="middle"></p>
<br>
Once it is received by the smart contracts, the first contract listed in the Transfer action builds a settlement transaction template. Because it knows which UTXO the other smart contract is going to use, it can pre-sign the entire contract before sending it on, reducing the number of times it needs to be handled to just one. The transaction is exchanged using message type 1002 (Signature Request).
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement-signature-request-message.svg?sanitize=true" alt="Atomic Swap Settlement Signature Request Exchange" align="center" align="middle"></p>
<br>
The second smart contract receives the full settlement, signed by the first contract, and must only review that the token quantities in the Settlement action match what was agreed to in the Transfer action, and that the addresses and fees are all correct. It then signs the transaction and sends it onto the network, completing the swap.
In this example, Participant 1 is is sending 100 of it's 150 Token 1 to Participant 2 (who previously had none) in exchange for 20 of its Token 2 (all of them). Participant 1 already has 10 of Token 2, leaving its final balance at 30.
<br>
<p align="center"><img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement-action.svg?sanitize=true" alt="Atomic Swap Settlement" align="center" align="middle"></p>
<br>

