# Oracles

- [Introduction](#introduction)
- [Identity Oracles](#identity-oracles)
	- [Example](#example)

<a name="introduction"></a>
## Introduction

The Tokenized Protocol allows smart contracts to use oracles.

An oracle, in the context of blockchains and smart contracts, is an agent that monitors, manages and verifies real-world events/people/information (off-chain data) and provides a trusted data feed to a smart contract.  Oracles provide the necessary link from the blockchain to the real-world. Without this, blockchain can't be used to represent/facilitate anything except ownership of bitcoin. The smart contract uses the data feed to manage the performance and administrative tasks of the contract with respect to its terms and conditions.

Currently, the protocol only supports Identity Oracles, but will support other types of oracles in the future.  A user's wallet will send a request message to the oracle and the oracle will respond with a signature (eg. ECDSA) for the parts of the message containing the data or instructions that are relevant to the oracle.

Oracles are included in a smart contract by the administration of the contract issuer in the Contract Offer action.  The administration includes the oracle's name, hostname:port and public key in the Contract Offer, and these will be found in the Contract Formation action for future reference by users and the smart contract.  Wallets can use the hostname:port to request signatures from the oracle, and the smart contract will use the public key to verify the signatures.

Recent block hashes are often included in the signature data to provide an expiration mechanism. The hash for the current tip minus four is used to prevent small reorgs from invalidating signatures. The default behaviour is that when that block is one hour old the signature is no longer valid.

<a name="identity-oracles"></a>
## Identity Oracles

Identity Oracles are entities that manage a database of user identities that they have verified.  They are also supplied with the user's XPUB so that the oracle can link the user's identity to the user's Bitcoin addresses.  The most important use case is to allow for transfer restrictions on financial instruments (security tokens) in the secondary markets. Administrations may want to restrict their tokens to accredited investors, or investors in a certain country or region.  The Identity Oracles are responsible for checking the terms and conditions of the contract and comparing the transfer restrictions/permissions to the requesting users identifying details.  If the user is allowed to receive a token from that contract, then the oracle will respond with a signed message that includes all of the important data and the permission flag set to 1.  If the user is not allowed to receive a token from the contract, then the oracle will respond with a signed message with the permission flag set to 0.

A single smart contract can use many Identity Oracles at the same time, giving their users choice with who they trust to manage their identities.

The use of Identity Oracles can provide smart contracts with the following capabilities:

- Restrict transfers to ID verified users only to meet KYC, AML, GDPR, compliance obligations
- Restrict transfers to accredited investors
- Restrict transfers to users within a certain age group (eg. 18+, 13-15, 21+, etc)
- Only permit transfers to users that are resident to certain countries or regions
- Any combination of the above


<a name="signatures"></a>
### Signatures

Signed data is encoded in a specific way. It is binary. Numbers are encoded in little endian. Bitcoin addresses are encoded as defined in the specification and implemented in the reference implementation packages.

<a name="contract"></a>
#### Contract Approval

A contract approval signature is needed in a contract offer action to verify the identity of the contract administrator. It verifies that the administrator key belongs to the entity listed in the issuer. The identity oracle information, public key, and signature is included in the contract offer and contract formation actions.

The signature hash contains the following data in this order.

- Administrator Addresses
- Entities (protobuf encoded Entity structure defined in specification)
- Recent Block Hash
- Approved Flag (8 bit unsigned integer, 1 = approved, 0 = denied)

This encoded binary data is then hashed with SHA256, then the hash is signed by the identity oracles private key. User's wallet software can verify this signature before interacting with this smart contract.

<a name="transfer"></a>
#### Transfer Approval

A transfer approval signature is needed in a transfer action for assets with identity oracles defined in their contract. They are needed to approve the receiving address as belonging to an identity that meets the ownership requirements of the asset.

The signature hash contains the following data in this order.

- Receiver Address
- Contract Address
- Asset Code
- Quantity (64 bit unsigned integer, number of tokens)
- Recent Block Hash
- Approved Flag (8 bit unsigned integer, 1 = approved, 0 = denied)


This encoded binary data is then hashed with SHA256, then the hash is signed by the identity oracles private key. The smart contract will then verify this signature in the transfer action with the identity oracle public key in the contract formation before approving the transfer of tokens.

<a name="identity"></a>
#### Identity Verification

An identity verification signature can be provided when establishing relationships or in any scenario where identity is needed. A message can be given to another party that includes the entity information, a public key or extended public key, and identity oracle information with the signature.

The signature hash contains the following data in this order.

- Entity (protobuf encoded Entity structure defined in specification)
- Public Key or Extended Public Key
- Recent Block Hash
- Approved Flag (8 bit unsigned integer, 1 = approved, 0 = denied)

This encoded binary data is then hashed with SHA256, then the hash is signed by the identity oracles private key. The message receiver can then verify the signature with the data provided to be confident they are dealing with the appropriate entity.

<a name="example"></a>
### Example

The interaction between the user, the Identity Oracle and the smart contract is best illustrated through a simple example.

A user (Sender) wants to send 100 tokens to another user (Receiver).  The tokens are restricted by the smart contract to transfers to addresses who are associated with users that have had their identity verified to meet KYC and AML compliance obligations.

![Oracle Process](https://raw.githubusercontent.com/tokenized/docs/master/images/concepts-oracles.svg?sanitize=true "Oracle Process") {.frame .centered .padded}
