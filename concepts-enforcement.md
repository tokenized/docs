# Enforcement

- [Introduction](#introduction)
- [Freezing Tokens](#freeze-tokens)
  - [Order (Freeze)](#order-freeze)
  - [Freeze](#freeze)
- [Thawing Tokens](#thawing-tokens)
  - [Order (Thaw)](#order-thaw)
  - [Thaw](#thaw)
- [Confiscating Tokens](#confiscating-tokens)
  - [Order (Confiscation)](#order-confiscation)
  - [Confiscation](#confiscation)
- [Reconciling Tokens](#reconciling-tokens)
  - [Order (Reconciliation)](#order-reconciliation)
  - [Reconciliation](#reconciliation)

<a name="introduction"></a>

## Introduction

The Tokenized Protocol includes a complete set of enforcement capabilities including the ability to:

- Freeze tokens
- Thaw tokens
- Confiscate tokens
- Reconcile token balance errors

These actions allow token issuers to manage their outstanding tokens for compliance with internal policies, contract terms and conditions, or lawful orders from enforcement or regulatory agencies.

To enact an enforcement order, the administration of the contract issuer uses the 'Order' action. In the action, the administration specifies the instrument the order is to be enacted on, what type of order it is and any other specific information relating to that order. There is also a field in the action that allows a hash or copy of an enforcecment order issued by a legal/law enforcement authority (court order, warrant, etc.) or decision which relates to the action being performed.

There are also fields that allow for an legal/law enforcement authority to sign a message (ECDSA) of the addresses, instruments and quantities that are to be frozen, thawed, or confiscated. This allows for issuers to comply with legal authorities with signed on-chain proof, and for the pseudonymity of token holders to be preserved as administrations/contract opertors won't be able to link real world identities with addresses, if that is desired for some use cases.

<a name="freeze-tokens"></a>

## Freezing Tokens

When tokens are frozen, they cannot be moved and the associated voting rights are disabled, however, the frozen tokens remain the property of the owner of the address that holds them.
When an address holds frozen tokens, it is not prevented from receiving more tokens. It is possible for a Freeze order to freeze a larger quantity of tokens than the account holds to prevent the account from receiving new tokens and spending them. Zero token freeze actions are invalid.
An address may be subject to multiple freeze orders. The number of tokens which are frozen is the aggregate quantity specified by all of the active Freeze actions. E.g. if an address has one active Freeze order that freezes 10,000 tokens and a second Freeze order that freezes 20,000 tokens is put in place, the account may only transfer whatever balance it has in excess of 30,000 tokens. Freeze actions can only be undone through a Thaw or a Confiscation action.

Freezing tokens is a two step process.

<a name="order-freeze"></a>

### Order (Freeze)

A Freeze order causes a specified quantity of tokens in each listed address to be frozen. A Freeze order can be applied to multiple addresses at once and can freeze any number of tokens held by a given address.

If the Freeze order is applied to an instrument but the contract's address is the given as the target, the Freeze order will apply to the entire instrument class, freezing all tokens.

![Order action (Freeze)](https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-freeze.svg?sanitize=true)

<span name="image-label">Order action (Freeze)</span>

<a name="freeze"></a>

### Freeze

After the smart contract has determined that the freeze order is valid, it responds by issuing a Freeze action. The action is sent to all addresses that the freeze order applies to. Once the Freeze action has been issued, any transfer orders that try to move frozen tokens will be rejected.
An issuer can place multiple freeze orders on a single address. In this case, the number of tokens frozen is the aggregate count of freeze orders on the address.

![Freeze action](https://raw.githubusercontent.com/tokenized/docs/master/images/freeze-action.svg?sanitize=true)

<span name="image-label">Freeze action</span>

<a name="thawing-tokens"></a>

## Thawing Tokens

Thawing tokens with a Thaw action, reverses a Freeze order that has been put in place. One Thaw action can only reverse one Freeze action. If an instrument is frozen by two separate Freeze orders, there must be two separate Thaw Orders applied to it before it can be traded, one per Freeze.
Thawing tokens is a two step process.

<a name="order-thaw"></a>

### Order (Thaw)

A Thaw Order reverses a single Freeze action.

![Order action (Thaw)](https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-thaw.svg?sanitize=true)
<span name="image-label">Order action (Thaw)</span>

<a name="thaw"></a>

### Thaw

After the smart contract has determined that the thaw order is valid, it responds by issuing a Thaw action. The action is sent to all addresses that the thaw order applies to. As soon as the Thaw action is sent, the smart contract will begin processing transfers for the previously frozen tokens.

![Thaw action](https://raw.githubusercontent.com/tokenized/docs/master/images/thaw-action.svg?sanitize=true)
<span name="image-label">Thaw action</span>

<a name="confiscating-tokens"></a>

## Confiscating Tokens

Token confiscation actions are used to move tokens from an address without the need for a signed message from the token owner. A confiscation action can be applied to tokens from multiple addresses at once, however all confiscated tokens must be sent to a single 'deposit' address. A confiscation action can be performed on frozen tokens. Once moved into the new address, those tokens can be moved unless a pre-emptive Freeze order is placed on the receiving address to lock down the soon to be received tokens.
Confiscating tokens is a two step process.

<a name="order-confiscation"></a>

### Order (Confiscation)

A Confiscation order can be used to move tokens without the need for a signature from the private key of the address that holds the tokens. A confiscation can be applied to multiple addresses in a single action, however, all confiscated tokens must be delivered to a single deposit address.

![Order action (Confiscation)](https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-confiscation.svg?sanitize=true)
<span name="image-label">Order action (Confiscation)</span>

<a name="confiscation"></a>

### Confiscation

After the smart contract has determined that the Confiscation Order is valid, it responds by issuing a Confiscation action. The action is sent to all addresses that the Confiscation Order applies to. The Confiscation Order sets a new balance for each of the target address(es) in the order, as well as for the deposit address, in the same way that a Settlement action would.

![Confiscation action](https://raw.githubusercontent.com/tokenized/docs/master/images/confiscation-action.svg?sanitize=true)
<span name="image-label">Confiscation action</span>

<a name="Reconciling Tokens"></a>

## Reconciling Tokens

A Reconciliation action is needed when there has been a break in a chain of token transfers that were not linked by dependent UTXOs. Tokens are owned by an address, not a UTXO. It is possible for child tokens transactions to not share the same Bitcoin parents as the token parent transactions. Therefore, if a token parent transaction is dropped from the network after the child transaction has been settled by the smart contract, then there will be a break in the token transfer chain, and the total outstanding tokens for that instrument will increase to an invalid quantity.

This is considered to be an extremely rare event, and the risk can be further reduced with different smart contract fee policies, response timing rules, double spend detection algorithms and sampling mempools of other nodes in the network to confirm the acceptance of transactions.

The Reconciliation action decrements the balance of tokens at the target address(es). This action effectively removes those tokens from existence and is basically a correction to the ledger. There can also be a discrepancy with bitcoin when a break in the token chain occurs, if the parent transaction that was dropped was an exchange of tokens for bitcoin. The bitcoin discrepancy will have to be dealt with at a commercial level by the administration or the contract operator.

Reconciliation is a two step process.

<a name="order-reconciliation"></a>

#### Order (Reconciliation)

A Reconciliation Order can be used to decrement the extraneous token balance of a particular instrument at an address(es). A Reconciliation can be applied to multiple addresses in a single action.

![Order action (Thaw)](https://raw.githubusercontent.com/tokenized/docs/master/images/order-action-reconciliation.svg?sanitize=true)
<span name="image-label">Order action (Thaw)</span>

<a name="reconciliation"></a>

### Reconciliation

After the smart contract has determined that the Reconciliation Order is valid, it responds by issuing a Reconciliation action. The action is sent to all addresses that the Reconciliation Order applies to. The Reconciliation order sets a new balance for each address in the same way as a Settlement action would.

![Reconciliation action](https://raw.githubusercontent.com/tokenized/docs/master/images/reconciliation-action.svg?sanitize=true)
<span name="image-label">Reconciliation action</span>
