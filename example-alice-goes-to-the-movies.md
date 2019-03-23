#Example: Send a token
Alice wants to send a movie ticket she bought to her friend Bob. He will be late and needs to have it in his wallet so he can enter the cinema separately.

In her wallet, Alice selects the ticket that she wants to send, and enters Bob's receiving address. This could be some kind of representative handle, or a standard Bitcoin address - the wallet will reach out to the nameserver to retrieve Bob's public address so that it can send the transaction in a format the network can understand.

##Building the Send operation
In this instance, the tokenized operation is built by concatenating the neccesary information into a hexadecimal string. The data is as follows:
1. OP_RETURN 			0x6a
2. PUSHDATA 7 			0x07 				// Push 7 bytes of data
3. Protocol identifier	0x00000020
4. Action prefix (T1)	0x5431 				// This is the Send operation
5. Version (0)			0x00
6. Pushdata 43			0x2B 				// 43 Bytes of data
7. Asset type (MOV)		0x4d4f56 			// Movie ticket
8. Asset ID (random)	0x61706d3271737a6e686b7332337a386438337534317338303139687972693369
9. Token Qty			0x01 				// Sending 1 token

When concatenated, this gives an output script as follows:

6a07000000205431002b4d4f5661706d3271737a6e686b7332337a38643833753431733830313968797269336901

##Build the Send operation carrier transaction
Once Alice has entered in the required information, her wallet automatically constructs an unsigned transaction that it holds in memory. This is a send transaction so it has the following inputs and outputs:

###Inputs:
0. A 17,112 (example) UTXO from Alice's Tokenized wallet's address. This is needed by the Contract agent to identify Alice as the party sending the tokens

###Outputs:
0. 3,100 Satoshis to the Contract Agent's Public Address - this covers the cost of the response transaction plus the Smart Contract Operator's fees
1. 546 Satoshis to the Token Receiver's Public Address - this is defined by the Dust limit rule and will eventually be 1 or even 0 Satoshis
2. 12,916 Satoshis to the Token Sender's Public Address - this is their change
3. The OP_RETURN containing the Send Action
Left out of the total outputs is the Miner's Fee which is 550 Satoshis in this example.

##Sending the output
When Alice hits send, her wallet will transmit the transaction onto the Bitcoin network. The transaction will be received by miners and propagated across the network, quickly being relayed to the Smart Contract Agent for analysis.

##Parsing the action
The smart contract agent that manages the movie tickets for the particular cinema Alice's ticket is for will see the transaction arrive in its wallet and will begin by looking at the outputs to ensure the correct fees have been attached. If not, it will send a rejection message. 
If the fees are correct, the agent will then retrieve and unpacking the token operation from the OP_RETURN output.
It will see that Alice is trying to send a movie ticket to Bob and will check the rules for that cinema's smart contract to ensure that
1. The ticket is valid
2. Alice has the right to transfer that ticket (this is an optional rule, specified when the contract for that movie is established)
3. Bob has the right to receive that ticket (this is an optional rule, specified when the contract for that movie is established)

##Settling the transaction
Once the Contract agent has established that Alice's send request is valid, it creates a Settlement Action packet to send onto the blockchain.
etwork can understand.

###Building the Settlement operation
Again, the tokenized operation is built by concatenating the neccesary information into a hexadecimal string. The data is as follows:
1. OP_RETURN 			0x6a
2. PUSHDATA 7 			0x07 				// Push 7 bytes of data
3. Protocol identifier	0x00000020
4. Action prefix (T4)	0x5434				// This is the Settlement operation
5. Version (0)			0x00
6. Pushdata 59			0x3B 				// Push 59 bytes of data
7. Asset type (MOV)		0x4d4f56 			// Movie tickets
8. Asset ID (random)	0x61706d3271737a6e686b7332337a386438337534317338303139687972693369
9. Party 1 Token Qty	0x02 				// Alice's new balance
10. Party 2 Token Qty	0x01 				// Bob's new balance
11. Timestamp 			0x0000016331e3c200 	// The timestamp of the settlement according to the Contract Agent

When concatenated, this gives an output script as follows:

6a07000000205434003b4d4f5661706d3271737a6e686b7332337a38643833753431733830313968797269336902010000016331e3c200

##Build the Send operation carrier transaction
To finalise the settlement action a separate transaction with it's own outputs and separate OP_RETURN packet must be built and sent onto the blockchain. The settlement transaction responds to both Alice and Bob at the same time giving them each an updated balance for their wallets to display.

The Contract Agent builds a new transaction containing the following:

###Inputs:
0. A 3,100 Satoshi UTXO from the Smart Contract agent's address. This confirms to Alice's wallet that the settlement is being received from the contract agent.

###Outputs:
0	546 Satoshis to Alice's address - This is so that her wallet can see the outcome
1	546 Satoshis to Bob's address - This is so that his wallet can see the movie ticket he's received
2	1,458 Satoshis to the Contract Public Address - This is the change
3	OP_RETURN (Settlement Action)	0	Token Sender and Receiver's token balances are adjusted up/down by X tokens in accordance with the Send/Exchange/Swap txn.
Left out of the total outputs is the Miner's Fee which is 550 Satoshis in this example

Bob's wallet now has control over one movie ticket meaning that when Bob arrives at the cinema he can transfer the token to the concierge to redeem access to his seat. 
