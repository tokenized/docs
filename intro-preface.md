# Preface

- [Introduction](#introduction)
  - [Key Components](#key-components)
- [Specification](#specification)
- [Support](#support)

<a name="introduction"></a>
## Introduction

The Tokenized Protocol is a system developed to enable businesses and users around the world to create, issue and manage tokens of all kinds using the low-friction and high-reliability of the Bitcoin network as the backbone of their infrastructure.

This documentation is intended to provide a clear and concise set of information on how to use the protocol. It also acts as the reference material for developers who wish to build their own implementation.

<a name="key-components"></a>
#### Key Components

The Tokenized Protocol operates using two key components:

- [Smart Contract](https://github.com/tokenized/smart-contract): An autonomous agent service, hosted by the issuer or a third party provider.

- [Tokenized Wallet](https://github.com/tokenized/wallet): An enhanced bitcoin wallet, operated by the user or administration of the contract issuer.

The smart contract and wallet both operate with the Tokenized Protocol and interact by [broadcasting actions](../protocol/actions) to the Bitcoin network. These actions are commonly prepared in the form of a request, coming from the wallet, and a response, from the smart contract. This provides a cryptographically provable event between two or more parties that is solidified in the immutable blockchain.

<a name="specification"></a>
## Specification

Each action message is defined by the Tokenized Protocol and provides various methods for common use cases, such as governance and compliance. A unique aspect of the Tokenized Protocol is its careful alignment with real world scenarios and coverage of the various requirements when conducting business.

An example of an action message is the creation of an asset token, this is prepared as an [Asset Definition](../protocol/actions#action-asset-definition) request and sent by the wallet to the smart contract. The Asset Definition contains all the information about the asset, including the asset class, number of issued tokens, a unique code, meta data and other details.

Each action message contains a number of fields that are populated to form the final message that is sent over the Bitcoin network. The message contents contain the value of each field where it is then concatenated together. This method provides maximum efficiency for storing the data on the blockchain.

It is important when converting these messages that every implementation uses the same specification. This source of truth for this can be found via the Tokenized GitHub repository:

- [Tokenized Protocol Specification](https://github.com/tokenized/specification)

This repository is a reference for the Tokenized Protocol structure. All definitions for message types and asset types are stored in YAML to be parsed and compiled into various programming languages.

<a name="support"></a>
## Support

The Tokenized team are available to give support for protocol specific queries and requests. If the protocol does not satisfy your needs, use case, or you have constructive feedback, then please feel free to reach out via one of our [community resources](/community) or using the contact details found on this website.
