# Preface

- [Introduction](#introduction)
  - [Key Components](#key-components)
- [Specification](#specification)
- [Support](#support)

<a name="introduction"></a>

## Introduction

The Tokenized Protocol is an open source application layer protocol that utilizes the Bitcoin SV network for passing and storing messages. The protocol focuses on data (aka records) captured from financial, legal, commercial and accounting activities for all types of legal entities and ownership structures. It aims to replace current financial messaging (eg. bank to bank (SWIFT), security exchanges (FIX) and fiat payment systems (credit cards, e-money, etc.), as well as other EDI standards like X12, etc. However, it also provides the framework for issuing any kind of token for any type of use case.

The protocol utilizes smart contracts, tokens, registers and messages as the building blocks to provide users and issuers with all of the tools required to manage their financial and legal lives in a more secure, private and low-cost way - while at the same time providing a streamlined user experience.

This documentation is intended to provide a clear and concise set of information on how to use the protocol. It also acts as the reference material for developers who wish to build an implementation.

<a name="key-components"></a>

### Key Components

The Tokenized Protocol operates using two key components:

- [Smart Contract](https://github.com/tokenized/smart-contract): An autonomous agent service, hosted by the issuer or a third party provider on behalf of the issuer.

- [Tokenized Wallet](https://github.com/tokenized/wallet): An enhanced bitcoin wallet, operated by the user or administration of the contract issuer.

The smart contract and wallet both operate with the Tokenized Protocol and interact by [broadcasting actions](../protocol/actions) to the Bitcoin network. These actions are commonly prepared in the form of a request, coming from the wallet, and a response, from the smart contract — each providing a cryptographically proven event between two or more parties, solidified in the immutable blockchain.

<a name="specification"></a>

## Specification

The Tokenized Protocol defines action messages that provide various methods for common use cases, such as governance and compliance. A unique aspect of the Tokenized Protocol is its precise alignment with real-world scenarios and coverage of the various requirements when conducting business.

An example of an action message is the creation of an instrument token, prepared as an [Instrument Definition](../protocol/actions#action-instrument-definition) request and sent by the wallet to the smart contract. The Instrument Definition contains all the information about the instrument, including the instrument class, the number of issued tokens, a unique code, metadata and other details.

Each action message contains many data fields that are populated to form the final protocol message, sent across the Bitcoin network. The message contents include the value of each data field concatenated together. This method provides maximum efficiency for storing the data on the blockchain.

It is crucial when converting these messages that every implementation uses the same specification. Find the source of truth for the Tokenized specification via the Tokenized GitHub repository:

- [Tokenized Protocol Specification](https://github.com/tokenized/specification)

This repository is a reference for the Tokenized Protocol structure. All definitions for message types and instrument types are stored in YAML to be parsed and compiled into various programming languages.

<a name="support"></a>

## Support

The Tokenized team are available to give support for protocol-specific queries and requests. If the protocol does not satisfy your needs, use case, or you have constructive feedback, then please feel free to reach out via one of our [community resources](/community) or using the contact details found on this website.
