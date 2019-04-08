# Oracles

The Tokenized protocol allows smart contracts to use oracles.  

An oracle, in the context of blockchains and smart contracts, is an agent that monitors, manages and verifies real-world events/people/information (off-chain data) and provides a trusted data feed to a smart contract.  The smart contract uses the data feed to manage the performance and administrative tasks of the contract with respect to its terms and conditions.

Currently, the protocol only supports Identity Oracles, but will support other types of oracles in the future.  A user's wallet will send a request message to the oracle and the oracle will respond with a signature (eg. ECDSA) for the message containing the data or instructions the smart contract is interested in.

Oracles are included in a smart contract by the issuer in the Contract Offer action.  The issuer includes the oracle's name, hostname:port and public key in the Contract Offer, and these will be found in the Contract Formation action for future reference by users and the smart contract.  Wallets can use the hostname:port to request signatures from the oracle, and the smart contract will use the public key to verify the signatures.

## Identity Oracles

Identity Oracles are entities that manage a database of user identities that they have verified.  They are also supplied with the user's XPUB so that the oracle can link the user's identity to the user's Bitcoin addresses.  The most important use case is to allow for transfer restrictions on financial instruments (security tokens) in the secondary markets.  Issuers may want to restrict their tokens to accredited investors, or investors in a certain country or region.  The Identity Oracles are responsible for checking the terms and conditions of the contract and comparing the transfer restrictions/permissions to the requesting users identifying details.  If the user is allowed to receive a token from that contract, then the oracle will respond with a signed message that includes all of the important data and the permission flag set to 1.  If the user is not allowed to receive a token from the contract, then the oracle will respond with a signed message with the permission flag set to 0.

A single smart contract can use many Identity Oracles at the same time, giving their users choice with who they trust to manage their identities.

The use of Identity Oracles can provide smart contracts with the following capabilities:

• Restrict transfers to ID verified users only to meet KYC, AML, GDPR, compliance obligations

• Restrict transfers to accredited investors

• Restrict transfers to users within a certain age group (eg. 18+, 13-15, 21+, etc)

• Only permit transfers to users that are resident to certain countries or regions

• Any combination of the above

### Process

The basic process is best described through a simple example.  

A user (Sender) wants to send 100 tokens to another user (Receiver).  The tokens are restricted by the smart contract to transfers to addresses who are associated with users that have had their identity verified to meet KYC and AML compliace obligations.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/main-concepts-oracles.svg?sanitize=true" alt="Oracle Process" align="middle">
