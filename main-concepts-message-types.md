#Tokenized Messaging
The Tokenized protocol includes a rich and expressive set of messaging actions which allow issuers, operators and users the flexibility to correspond in a way that gives wallets, account management and audit software the ability to record a full set of transactional actions.
Messaging actions are split into two types, the Message action and Rejection action.

##Message action
Message actions are for general purpose messaging between users. The protocol has the means to support pre-defined message types allowing messaging to be used for things such as private messaging between 2 users and the transmission of transaction templates requiring additional data such as inputs, signatures and more.
There are 4 Message types defined in the Tokenized protocol:
1. Public message: Message #0002 - A generic public message or public announcement. Sent to an address(es).  Can be used for an official issuer announcement.
2. Private message" Message #0003 - A generic private message. Sent to another address(es). Encryption is to be used.
3. Offer message: Message #1001 - A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should 
									have all, or nearly all, of the details required for the receiving party to accept the offer.  The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror's payment/receipt details, etc.).  The Offer message is different to a Signature Request message in that it is missing the offeree's payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction.  If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message. 
4. Signature Request message: Message #1002 - Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed 
									around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.

As the Tokenized protocol matures, it is expected that many more message types will be introduced which enable new and exciting functionality to be handled simply and easily. 

##Rejection action
The rejection action is the only message type sent by the smart contract. The Rejection action is used when a user has requested an action that is unable to be completed by the smart contract. All rejection messages include a rejection type, which links to a message telling the user why their request was rejected.
The following rejection messages have been defined:

###Basic Rejection Codes
0. Success - No failure. This code should not be used in a reject message.
1. Message Malformed - The OP_RETURN message is malformed. It doesn't pass data validation or something about it isn't according to protocol.
2. Transaction Malformed - The Bitcoin tx is malformed. Incorrect inputs/outputs or something similar.

###Contract Rejection Cpdes
10. Contract Already Exists - The contract already exists and can't be recreated.
11. Contract Is Not Dynamic - 'Sent when a CO is received, but the contract type is not "D" (Dynamic)'
12. Contract Asset Quantity Reduction - Sent when a CA tries to reduce the number of assets below the number of assets the contract has.
13. Contract Fixed Quantity - Sent when the issuer attempted to increase the quantity of assets in a contract beyond the fixed quantity permitted.
14. Contract Auth Flags Prohibit - The contract auth flags don't permit the action requested.
15. Contract Expired - The contract is expired so can no longer accept requests.
16. Contract Frozen - The contract is frozen and the request is not permitted while frozen.
17. Contract Revision Incorrect - The revision in a contract amendment is incorrect.

###Asset Rejection Codes
20. Asset Code Already Exists - The asset code specified already exists and can't be reused.
21. Asset Not Found - The asset code is not found.
22. Asset Auth Flags Prohibit - The asset auth flags don't permit the action requested.
23. Asset Frozen - The asset is frozen and the request is not permitted while frozen.
24. Asset Revision Incorrect - The revision in an asset amendment is incorrect.

###Transfer Rejection Codes
30. Transfer To Self Prohibited - Transfers with the sender and receiver addresses the same are not permitted.
31. Transfer Expired - The transfer has expired.
32. Holdings Frozen - Holdings are frozen, so the request can't be completed.

###Governance Rejection Codes
40. Holder Proposal Prohibited - Holders are not permitted to make proposals.
41. Proposal Conflicts - The proposal conflicts with an unapplied proposal.
42. Vote Not Found - The vote ID referenced is not found.
43. Vote Closed - The vote has closed and ballots are no longer permitted.
44. Ballot Already Counted - The ballot has already been counted for this address.

###Enforcement Rejection Codes

###Funding  Rejection Codes
60. Insufficient Transaction Fee Funding - Insufficient bitcoin quantities for response transaction fees.
61. Insufficient Value - Insufficient bitcoin quantity in inputs to fund request.
62. InsuInsufficient Quantity - Insufficient token holdings to for request.

###Address Rejection Codes
70. Requestor Is Not Issuer - The requestor is not the issuer and is required to be for this request.
71. Requestor Is Not Operator - The requestor is not the operator and is required to be for this request.
72. Unauthorized Address - The address specified is not permitted for this request.

###Signature Rejection Codes
80. Invalid Signature - The signature provided is not valid. This is for signatures included within OP_RETURN data. Not bitcoin transaction signature scripts.

