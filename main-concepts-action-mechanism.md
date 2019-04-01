##  Action Mechanism

The smart contract is an agent that listens to the Bitcoin (BSV) network for commands (request actions) addressed to it from users and issuers. It does not publish any actions to the blockchain without being first prompted and paid to do so by the requesting party.

The smart contract is the only entity with the ability to directly modify the contract or the assets it controls. Issuers and users interact with the smart contract using a mechanism known as request and response.

This means that wallets communicating with a smart contract send requests to the contract, by way of the Bitcoin blockchain, and do not need to take any further action. The contract receives request actions into its wallet and evaluates them under the rules/terms and state of the contract. If the actions being requested are valid, the smart contract will build a response transaction and send it to the Bitcoin network. The users' wallets will see these responses arrive in their addresses, and update each user's wallet accordingly.

When the contract finds that a request is in breach of the rules that govern that contract, it will respond with a rejection message. At this point it is up to the user's wallet to notify them of the rejection and for them to re-attempt the action with the correct information. Most wallets that are configured to work with the Tokenized protocol, will be able to prevent users from sending actions that do not meet the contract's requirement. Rejection messages are expected to be rare.

For a complete list of the different action types, and the applicable responses, please see the image below.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/order-of-operations.svg?sanitize=true" alt="Order of Operations">
