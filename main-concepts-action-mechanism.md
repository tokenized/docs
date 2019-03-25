## Tokenized Action Mechanism

The Tokenized Smart Contract is a completely passive agent. It does not publish any actions to the blockchain without being first prompted and paid to do so by the requesting party.

In this usage paradigm, the smart contract is the only entity with the ability to directly modify the contract or the assets it controls. Issuers and users interact with the smart contract using a mechanims known as Request/Response.

This essentially means that wallets communicating with a smart contract send requests at the contract and do not need to take any further action. The contract receives request actions into its wallet and evaluates them under the rules of the contract. If the actions being requested are valid, the Smart Contract will build a response transaction and send it onto the network. The users' wallets will see these responses arrive in their accounts, and update each user's wallet accordingly.

When the contract finds that a request is in breach of the rules that govern that contract, it will respond with a rejection response. At this point it is up to the users wallet to notify them of the rejection and for them to re-attempt the action with updated information. Most times a wallet will understand the rules of a contract and should prevent users from sending actions that do not meet the contract's requirement. Rejection actions are expected to be rare.

For a complete list of the different action types, and the applicable responses, please see the image below.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-of-operations.svg?sanitize=true" alt="Order of Operations">
