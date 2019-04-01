##Transferring Tokens to a Single Receiver
The act of transferring tokens can become fairly complicated when there are multiple parties and contracts involved, however, the final outcome is always captured in just two on-chain transactions:
1. Tranfer Action (Request)
2. Settlement Action (Response)
In its simplest form, a transfer is an action between 2 parties which is validated by a smart contract.
In this example, a token issuer will send 100 tokens from its own balance to a receiver. This event is initiated by the issuer through the creation of a transfer action detailing the receiver's address and the number of tokens they wish to send.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/basic-transfer-example.svg?sanitize=true" alt="A basic transfer action" align="middle">
The smart contract receives the request into its wallet and validates that it meets all of the transfer requirements of the contract. Once evaluated, the contract then builds a settlement action in response and sends it onto the network.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/basic-settlement-example.svg?sanitize=true" alt="A basic transfer action" align="middle">

##Transferring Tokens to Multiple Receivers
Similarly, for an issuer to distribute tokens to more than one person, the transfer is a 2 step process. 
In this example, the issuer will now send an additional 100 tokens to the same receiver, and 300 tokens to a second receiver (receiver 2).
Note that the transfer action deals with the number of tokens being sent, but the settlement transaction deals with the final balances of each account.
First, the issuer builds a transfer request detailing the number of tokens to be sent and the addresses to send them to:
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/two-receiver-transfer-example.svg?sanitize=true" alt="A two receiver transfer action" align="middle">
Next, once the smart contract has checked everything is ok, it sends a settlement transaction that updates the balances of any wallets involved in the transaction.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/two-receiver-settlement-example.svg?sanitize=true" alt="A two receiver settlement action" align="middle">

##Purchasing tokens with Bitcoin (Exchange via Transfer Action)
The purchase of tokens with Bitcoin is a slightly more complicated interaction as it requires that the Transfer action be signed by two parties before it can be sent onto the network.
This would typically work by the token purchaser entering into an exchange interface or shopfront and selecting the tokens that they wish to purchase. Typically, the interface will provide them with a cost for the tokens, with a time limit to finalise the purchase at the proposed price.
Once they user has accepted the seller's contract, they are given a transaction template that contains the details of the seller, the asset and the smart contract that will settle the transaction.
Depending on the exchange used, there may be additional BSV outputs for the cost of performing the exchange. These details will also be included in the tranfer action and validated by the smart contract.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-example-template.svg?sanitize=true" alt="Transfer request template given by token seller to purchaser" align="middle">
The seller can provide this information to the purchaser via standard HTTP delivery methods, or in an on-chain transaction using the Message action. Either method is valid.
Once the purchaser has received the template, their wallet fills in the missing information and signs the transaction with SIGHASH_ALL. If the buyer needs to add more than one input UTXO to the transaction this is possible. The input addresses do not affect the action taken by the contract. 
They must now send the transfer back to the token Seller in order for them to countersign also using SIGHASH_ALL. Once this has been completed, the contract can be sent onto the network for mining.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-example-final.svg?sanitize=true" alt="Final Transfer request signed by buyer and seller" align="middle">
Because only one smart contract is involved, the settlement can be built and sent without having to deliver any templates.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-settlement-example-final.svg?sanitize=true" alt="Exchange settlement" align="middle">

##Tokenized Atomic Swaps
Conducting an atomic swap using tokenized is another more complicated transaction as it requires the holders of the tokens being exchanged to sign the transfer action, and for both contracts to sign the settlement.
To begin, the two token holders agree to a transaction between themselves. The first token holder builds a partially complete transaction which has the full details of the exchange except for the second party's receiving address.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-template.svg?sanitize=true" alt="Atomic Swap Transfer Action Template" align="middle">
The second party then fills in the missing details and signs the transaction before sending it back to the first party, who then countersigns and sends the transaction onto the network.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-final.svg?sanitize=true" alt="Atomic Swap Transfer Action Final" align="middle">
Once it is received by the Smart Contracts, the first contract listed in the Transfer action builds a settlement transaction template. Because it knows which UTXO the other smart contract is going to use, it can pre-sign the entire contract before sending it on, reducing the number of times it needs to be handled to just one. The second smart contract receives the full settlement, signed by the first contract, and must only review that the token quantities in the settlement action match what was agreed to in the transfer action, and that the addresses and fees are all correct. It then signs the transaction and sends it onto the network, completing the swap.
In this example, Participant 1 is is sending 100 of it's 150 Token 1 to Participant 2 (who previously had none) in exchange for 20 of its Token 2 (all of them). Participant 1 already has 10 of Token 2, leaving its final balance at 30.
<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement.svg?sanitize=true" alt="Atomic Swap Settlement" align="middle">


