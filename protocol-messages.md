# Protocol Messages

- [Introduction](#introduction)
- [Available Messages](#all-messages)

<a name="introduction"></a>
## Introduction

The Tokenized protocol features a complete messaging suite for all types of messaging including general purpose private and public messaging, as well as commercial, financial and legal messaging in accordance with a variety of established Electronic Data Interchange (EDI) standards. They are also used to allow smart contracts to share information and orchestrate multiple signature transactions, such as atomic swaps.

<a name="all-messages"></a>
## Available Messages

<div class="content-list collection-method-list" markdown="1">
- [Offer](#message-offer)
- [Signature Request](#message-signature-request)
- [Public Message](#message-public-message)
- [Private Message](#message-private-message)
</div>

<a name="message-offer"></a>
#### Offer

A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should have all, or nearly all, of the details required for the receiving party to accept the offer.  The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror's payment/receipt details, etc.).  The Offer message is different to a Signature Request message in that it is missing the offeree's payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction.  If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>Timestamp in nanoseconds for when the message sender creates the transaction. </td>
    </tr>
    <tr>
        <td>RefTxId</td>
        <td>
            <a href="field-types#type-tx-id">TxId</a>
        </td>
        <td>Tx Id of the request transaction referenced by the offer. For a multi-contract settlement, the Payload will be a Settlement op return script and the RefTxId will be the id of the tx containing the Transfer.</td>
    </tr>
    <tr>
        <td>Payload</td>
        <td>
            varbin(32)
        </td>
        <td>Full serialized op return script containing an offer to another party, usually to exchange tokens/bitcoin. The message needs data added by another party. </td>
    </tr>
</table>



<a name="message-signature-request"></a>
#### Signature Request

Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>Timestamp in nanoseconds for when the message sender creates the transaction. </td>
    </tr>
    <tr>
        <td>Payload</td>
        <td>
            varbin(32)
        </td>
        <td>Full serialized bitcoin tx with multiple inputs from different wallets/users. </td>
    </tr>
</table>



<a name="message-public-message"></a>
#### Public Message

Generic public message or public announcement. Sent to an address(es).  Can be used for an official issuer announcement.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>Timestamp in nanoseconds for when the message sender creates the transaction. </td>
    </tr>
    <tr>
        <td>PublicMessage</td>
        <td>
            varchar(32)
        </td>
        <td>Tokenized Ltd. announces product launch. </td>
    </tr>
</table>



<a name="message-private-message"></a>
#### Private Message

Generic private message. Sent to another address(es). Encryption is to be used.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>Timestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>Timestamp in nanoseconds for when the message sender creates the transaction. </td>
    </tr>
    <tr>
        <td>PrivateMessage</td>
        <td>
            varbin(32)
        </td>
        <td>Tokenized Ltd announces product launch. </td>
    </tr>
</table>


