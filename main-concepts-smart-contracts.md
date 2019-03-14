##Tokenized Smart Contracts
Tokenized smart contracts are new way for corporations, businesses and individuals to manage the ownership and distribution of goods and services, and the division of a large asset such as a company or holding into pieces for the purposes of distributing ownership and capital raising.

A tokenized smart contract carries with it the full weight of a legal document or structure that would achieve the same thing in an off-chain environment.

###Contract Parties
There are two parties involved in the creation of a tokenized smart contract. These are:
1. The issuer
2. The Smart Contract Operator
It is possible for the issuer and the smart contract operator to be the same entity, however it is expected that this will only be the case for a minority of contracts that operate using platforms based on the Tokenized protocol.
In most cases, the Issuer will make use of a smart contract agent and services provided by a third party to build and operate their smart contract. These third party providers will likely also provide the necessary legal and financial knowledge to ensure that tokens issued on their platform are done in such a way that they are valid, legal and meaningful.

For this reason, building contracts using Tokenized requires the same level of foresight and preparation as that required for the creation of a similarly structured off-chain device. 

##Tokenized Smart Contract Agent
The Tokenized Smart Contract Agent is a fully autonomous agent that runs using microservices instance in a cloud system such as Amazon Lambda. The smart contract has a private key that is backed up securely and can be used to re-create a contract in the event of a loss of service. 
The agent can only respond to instructions it receives as Tokenized transactions into its own wallet. All responses from the agent are sent onto the blockchain as per the order of operations needed for the action taking place.
The Tokenized Smart Contract Agent is written in Go and is fully open source. Details of the agent can be found in the <a href="https://github.com/tokenized/specification">Tokenized Smart Agent Github repository</a>.
