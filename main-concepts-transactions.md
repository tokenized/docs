##Tokenized Transactions
All tokenized transactions are sent by delivering a UTXO to the receiving parties address, accompanied by an OP_RETURN output which describes the action being performed. All user driven actions are initiated by sending a request to the contract agent to perform a certain action. If the request is valid, the agent will respond by sending another transaction (or transactions) containing updated information about the contract or asset (New balances, updated revision data, etc) either to a known public address for all token holders or directly to particular token holders.

Some transactions (contract offer, exchange, atomic swap) require multiple inputs that are signed by different parties to be recognised by the contract agent. If the agent finds that the transaction is valid (within contract rules, adequate balance and fees included) it will process the instruction, and send response transaction onto the blockchain to confirm the action.

Transactions that impact balances or the contract state always include a timestamp to ensure that even in the event of a block re-organisation that the contract actions can be restored in the correct order.

##Building a transaction
Tokenized transactions are build by compiling the token data as a list of fields and appending them to each other as a hexadecimal string. There are multiple different data formats used in Tokenized:
1. String - An ascii string
2. Text - Text in UTF-8 format (the text format is intended to accomodate UTF-8, UTF-16, UTF-32, Unicode and ASCII formats however only UTF-8 is currently supported)
3. uint64 - A 64 bit unsigned integer
4. uint32 - A 32 bit unsigned integer
5. uint16 - A 16 bit unsigned integer
6. uint8 - An 8 bit unsigned integer
7. varchar32 - A variable length datum with a 4 byte field at the beginning that contains its length in uint32 format
8. varchar16 - A variable length datum with a 2 byte field at the beginning that contains its length in uint16 format
9. varchar8 - A variable length datum with a 1 byte field at the beginning that contains its length in uint8 format
10. Float32 - A 32 bit floating point number
11. Time - 64 bit unix epoch time (milliseconds since 0:00:00, Jan 1 1970)
12. Binary - A variable byte length field for supporting binary flags
13. Sha256 - A SHA256 hash
14. OPCODE - Script OPCODES - Limited to push instructions (0-75 byte push, OP_PUSHDATA1, OP_PUSHDATA2, OP_PUSHDATA4)
15. PUSHDATA_LENGTH - Length data for OPCODES that require secondary information regarding the length of the data packet
16. Payload - The token payload is an additional packet of data made that represents the details of the token. Each token type has its own payload.

##Assembling OP_RETURN packet
To assemble an OP_RETURN packet, the first byte is always the OP_RETURN opcode (0x6a)
The second byte is a PUSHDATA instruction. The PUSHDATA instruction can be variable depending on the number of bytes in the data packet being pushed into the output. It is possible to perform multiple pushes in a single OP_RETURN output, allowing the output to have multiple fields of different lengths. There are always 2 pushdata operations in a Tokenized operation. The first carries the "Tokenized" protocol identifer (tokenized.com), and the second carries the remainder of the data in the packet. This can be up to 99kB of data with the current BitcoinSV network capability, but will eventually allow contracts of up to 4GB to be built.

###Using PUSHDATA
For packets with less than 75 bytes of data, the pushdata instruction is simply a single byte containing the length of the packet.
e.g. 0x6a 0x03 0x010203 is a OP_RETURN followed by a PUSHDATA instruction to push 3 bytes, and then 3 bytes of information

For packets containing 76 - 255 bytes of data, the pushdata instruction is the OP_PUSHDATA1 opcode (0x4c) followed by a single byte unsigned integer containing the number of bytes to push in the instruction.
e.g. 0x6a 0x4C 0xD2 <210 bytes of ascii data>
This is OP_RETURN followed by OP_PUSHDATA1 followed by 0xD2 which is a hexadecimal representation of 210, then an uninterrupted 210 byte long string of hexadecimal data.

For packets containing 256 - 65,535 bytes of data, OP_PUSHDATA2 (0x4d) is used, followed by a 2 byte representation of the length of the data packet following.

For packets containing 65,536 - 4,294,967,295 bytes of data, OP_PUSHDATA4 (0x4e) is used, followed by a 4 byte represenation of the length of the data packet following.

##Breaking down the OP_RETURN output
A Tokenized action output is always created with 2 separate push operations. They are split as follows:

###1. Tokenized protocol identifier
The first push is 13 bytes long and contains only the Tokenized protocol identifier which is the string 'tokenized.com'.

###2. Action payload
The action payload is dependent on the action type and may include token specific information as required. It is important that the client and wallet must both know exactly what is expected in the remainder of the packet through a combination of the action prefix and version. If the packet does not conform to the contract agent's expectation of the operation being requested, it will respond with a rejection message.
