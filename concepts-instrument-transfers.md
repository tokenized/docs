# Instrument Transfers

- [Introduction](#introduction)
- [Single Receiver](#single-receiver)
- [Multiple Receivers](#multiple-receiver)
- [Swap Tokens for Bitcoin](#exchange-bitcoins)
- [Cross Contract Atomic Swaps](#atomic-swaps)

<a name="introduction"></a>

## Introduction

The Transfer action is the means by which all instrument transfers are conducted, with the exception of enforcement actions. The action is versatile and allows instruments to be transferred between multiple holders and across multiple smart contracts. The following outlines the main ways in which the Transfer action is used.

The act of transferring tokens can become complicated when there are multiple parties and contracts involved, however, the final outcome is always captured in just two on-chain transactions:

1. Transfer action (Request)
2. Settlement action (Response)

> **Note:** Unlike most other actions, the [Transfer action](../protocol/actions#action-transfer) places the participating addresses inside the message payload as an [Instrument Transfer type](../protocol/actions#type-instrument-transfer) instead of using the transaction inputs and output. This means the recipient of a transfer will be unaware of the transfer until it has settled and helps reduce the number of dust outputs. The same structure applies to the [Enforcement actions](../concepts/enforcement).

<a name="single-receiver"></a>

## Single Receiver

When transferring tokens to a single receiver the transfer is an action between 2 parties which is validated by a smart contract.

In this example, a token issuer will send 100 tokens from its own balance to a receiver. This event is initiated by the the administration of the contract issuer through the creation of a Transfer action detailing the receiver's address and the number of tokens they wish to send.

![A basic transfer action](https://raw.githubusercontent.com/tokenized/docs/master/images/one-receiver-transfer-example.svg?sanitize=true)
<span name="image-label">A basic transfer action</span>

The smart contract receives the request into its wallet and validates that it meets all of the terms and conditions for transfers on the contract. Once evaluated, the contract then builds a Settlement action in response and sends it onto the network.

![A basic transfer action](https://raw.githubusercontent.com/tokenized/docs/master/images/one-receiver-settlement-example.svg?sanitize=true)
<span name="image-label">A basic transfer action</span>

<a name="multiple-receiver"></a>

## Multiple Receivers

Similarly, when transferring tokens to multiple receivers--for an issuer to distribute tokens to more than one person--the transfer is a 2 step process.

In this example, the issuer will now send an additional 100 tokens to the receiver from the example above (receiver 1), and 300 tokens to a second receiver (receiver 2).

Note that the transfer action deals with the number of tokens being sent, but the settlement transaction deals with the final balances of each account.
First, the administration builds a transfer request detailing the number of tokens to be sent and the addresses to send them to:

![A two receiver transfer action](https://raw.githubusercontent.com/tokenized/docs/master/images/two-receivers-transfer-example.svg?sanitize=true)
<span name="image-label">A two receiver transfer action</span>

Next, once the smart contract has checked everything is ok, it sends a settlement transaction that updates the balances of any wallets involved in the transaction.

![A two receiver settlement action](https://raw.githubusercontent.com/tokenized/docs/master/images/two-receivers-settlement-example.svg?sanitize=true)
<span name="image-label">A two receiver settlement action</span>

<a name="exchange-bitcoins"></a>

## Swap Tokens for Bitcoin

The purchase of tokens with Bitcoin (token for bitcoin transfer) is a more complicated interaction as it requires that the Transfer action be signed by two parties before it can be sent onto the network.

This would typically work by the token purchaser entering into an exchange interface or shopfront, and selecting the tokens that they wish to purchase. Typically, the interface will provide them with a cost for the tokens, with a time limit to finalize the purchase at the proposed price.

When the user has assembled the information for their purchase, they are sent a Message action which contains an 'Offer' message type. This includes a transaction template that contains the details of the seller, the amount they are to pay, the instrument and the smart contract that will settle the transaction.

![Transfer request template sent in Message action to purchaser](https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-offer-message.svg?sanitize=true)
<span name="image-label">Transfer request template sent in Message action to purchaser</span>

Depending on the exchange used, there may be additional BSV outputs for the cost of performing the exchange. These details will also be included in the Transfer template. If the buyer changes the contents of the transaction, the exchange can simply elect not to sign, invalidating the transaction.
If the buyer is happy with the proposed exchange, they add appropriate Bitcoin inputs to the transaction, insert their token receiving address into the appropriate locations, and sign the transaction, sending the template back to the Smart Contract in a 'Signature Request' message.

![Transfer template sent in Message action to Merchant/Exchange for final signature](https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-signature-request-message.svg?sanitize=true)
<span name="image-label">Transfer template sent in Message action to Merchant/Exchange for final signature</span>

Once the seller-signed transaction has been received by the merchant/exchange, they have one final opportunity to verify that the contents remain in-line with what they agreed to with the buyer, and can sign and transmit the transaction to the Bitcoin network.

![Final Transfer request signed by buyer and seller](https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-transfer-example.svg?sanitize=true)
<span name="image-label">Final Transfer request signed by buyer and seller</span>

Because only one smart contract is involved, the exchange settlement can be built and sent directly by the smart contract.

![Exchange settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/exchange-settlement-example.svg?sanitize=true)
<span name="image-label">Exchange settlement</span>

<a name="atomic-swaps"></a>

## Cross Contract Atomic Swaps

Conducting an atomic swap (token for token transfer) using Tokenized is another more complicated transaction as it requires the holders of the tokens being exchanged to sign the Transfer action, and for both smart contracts to sign the Settlement action.

![Atomic Swap Transfer Order of Operations](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-process-order-of-operations.svg?sanitize=true)
<span name="image-label">Atomic Swap Transfer Order of Operations</span>

To begin, the two token holders agree to a transaction between themselves. The first token holder builds a partially complete transaction template which has the full details of the exchange except for the second party's receiving addresses and UTXO commitment. This is sent to the second party as a serialized partial transaction inside a Message action, using message type 1001 (Offer).

![Atomic Swap Transfer Offer Message](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-offer-message.svg?sanitize=true)
<span name="image-label">Atomic Swap Transfer Offer Message</span>

The second party then fills in the missing details and signs the transaction before sending it back to the first party in another message using message type 1002 (Signature Request).

![Atomic Swap Transfer Signature Request](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-signature-request-message.svg?sanitize=true)
<span name="image-label">Atomic Swap Transfer Signature Request</span>

The first user then countersigns and sends the transaction to the Bitcoin network.

![Atomic Swap Transfer Action](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-transfer-action.svg?sanitize=true)
<span name="image-label">Atomic Swap Transfer Action</span>

Once it is received by the smart contracts, the first contract listed in the Transfer action builds a settlement action template. Since the first contract doesn't know the balances of the other contract it sends the incomplete settlement action data to the second contract in a message type 1003 (Settlement Request).

![Atomic Swap Settlement Signature Request Exchange](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement-request-message.svg?sanitize=true)
<span name="image-label">Atomic Swap Settlement Request Exchange</span>

The second contract then adds settlement data pertaining to it and since the data is now complete and it knows everything about the settlement, it creates the complete settlement tx (minus signatures), signs its inputs, and sends it back to the first contract in a message type 1002 (Signature Request).

![Atomic Swap Settlement Signature Request Exchange](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement-signature-request-message.svg?sanitize=true)
<span name="image-label">Atomic Swap Settlement Signature Request Exchange</span>

The first contract then double checks the settlement transaction to ensure the second contract didn't modify anything it wasn't supposed to, then signs it and transmits it to the Bitcoin network.
In this example, Participant 1 is sending 100 of its 150 Token 1 to Participant 2 (who previously had none) in exchange for 20 of its Token 2 (all of them). Participant 1 already has 10 of Token 2, leaving its final balance at 30.

![Atomic Swap Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/atomic-swap-settlement-action.svg?sanitize=true)
<span name="image-label">Atomic Swap Settlement"</span>
