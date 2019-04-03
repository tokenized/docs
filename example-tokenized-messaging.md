##Tokenized Messaging
The Tokenized protocol includes the capability for all wallets to send messages using the tokenized protocol. Message actions do not elicit any reaction from the smart contract and are used to convey information not related to changing the status of the smart contract.
There are two Message types used by the protocol:
1. Message Action
2. Rejection Action

###1. Message Actions
The Message Action is an open OP_RETURN which can be used to exchange any type of message on the blockchain. This can be anything from:
* Transaction templates
* Invoices and receipts
* Plaintext messaging services
* Other
Message actions are not read by the smart contract and only serve as a service to record data onto the blockchain. The message action format is standardised to ensure that any wallets which follow the Tokenized protocol will be able to identify and parse messages.
A message may be sent to many addresses at once by appending multiple outputs to the transaction which contains the Message Action.

####Message Types
Messages are identified by Message Type, which is a 32 Byte number allowing for up to 65,535 message types to be developed.
Moving forward, Tokenized plans to release a suite of pre-formatted message types which will allow contract operators to provide a rich set of default options to contract owners.

Current message types include:
* 0002 - Public Message 	Generic public message or public announcement. Sent to an address(es).  Can be used for an official issuer announcement.
* 0003 - Private Message 	Generic private message. Sent to another address(es). Encryption is to be used.
* 1001 - Offer 				A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should have 
							all, or nearly all, of the details required for the receiving party to accept the offer.  The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror's payment/receipt details, etc.).  The Offer message is different to a Signature Request message in that it is missing the offeree's payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction.  If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message.
* 1002 - Signature Request 	Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to 
							the parties (including smart contracts) that still have to sign the transaction.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/message-action.svg?sanitize=true" alt="Message action" align="middle">

###2. Rejection Actions
A rejection action is sent by the smart contract in response to a request action that did not conform to the requirements of the smart contract. Where possible, the rejection action includes infomration about the issues to enable users to remedy the issue before re-attempting the transaction.
The rejection message has 'Type' information which relays to the users why their transaction was rejected. This is accompanied by a detailed message constructed by the smart contract. 
All rejection actions are timestamped.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/rejection-action.svg?sanitize=true" alt="Rejection action" align="middle">