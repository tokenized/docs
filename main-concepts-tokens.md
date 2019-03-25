## Tokenized Tokens

A Tokenized token can be defined as an asset that has been created and is managed by a Tokenized Smart Contract Agent which is managed using rules that are specified in the formation of the contract.

It is up to the token issuer to ensure that the rules under which tokens are exchanged throught that smart contract are in-line with the legal and regulatory requirements of the jurisdiction in which they are being managed.

This may include the need to whitelist or restrict the users of a token, or to comply with orders from law enforcement that require the asset issuer to freeze or even confiscate tokenized assets.

## Token Types

The Tokenized protocol and platform is predicated on the need to be able to control and manage tokens of all types. Token types are defined by a 3 letter code which is used by the wallet and Smart Contract to as a guide into how the data attached to the token must be parsed and presented.

### Contents of a Token

The identity of a Tokenized Token is centered around its Asset ID which should be unique on the Bitcoin network. This is generated when the tokens are created by the Smart Contract Agent and is carried by the tokens until they are destroyed.

As well as this, all token types carry a 'Payload' containing metadata that is used by the tokenized protocol to manage exchange and other activities.

## Token fungibility

Fungibility is the property of a good or a commodity whose individual units are essentially interchangeable, where each unit is indistinguishable from any other unit. Tokens that are created with the same asset ID are considered fungible tokens. These tokens can be exchanged and will carry the same value as any other token created in the same asset ID.

It is possible to create non-fungible tokens by creating tokens that have unique asset IDs. These tokens can then be imbued with unique qualities such as seat numbers or other details for things such as in-game collectibles or other such items.

## Modifying tokens

Depending on the rules of the Asset and Smart Contract, most tokens can have their metadata modified using on-chain messages to the smart contract agent.

This may include modifications to the asset information, or to the token specific metadata itself.

Modifications can be made to any individual field (within rules) but modifications to the payload require the full data encapsulated within the payload to be overwritten.
