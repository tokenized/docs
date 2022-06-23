# Protocol Messages

- [Introduction](#introduction)
- [Available Messages](#all-messages)

<a name="introduction"></a>

## Introduction

The Tokenized protocol features a complete messaging suite for all types of messaging including general purpose private and public messaging, as well as commercial, financial and legal messaging in accordance with a variety of established Electronic Data Interchange (EDI) standards. They are also used to allow smart contracts to share information and orchestrate multiple signature transactions, such as atomic swaps.

<a name="all-messages"></a>

## Available Messages

<div class="content-list collection-method-list" markdown="1">
- [Public Message](#public-message)
- [Private Message](#private-message)
- [Reverted Tx](#reverted-tx)
- [Offer](#offer)
- [Signature Request](#signature-request)
- [Settlement Request](#settlement-request)
- [Output Metadata](#output-metadata)
- [Distribution](#distribution)
- [Initiate Relationship](#initiate-relationship)
- [Pending Accept Relationship](#pending-accept-relationship)
- [Accept Relationship](#accept-relationship)
- [Relationship Amendment](#relationship-amendment)
- [Initiate Thread](#initiate-thread)
</div>

<a name="public-message"></a>

#### Public Message

Generic public message or public announcement. Sent to an address(es). Can be used for an official issuer announcement.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>0002</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender creates the transaction.
                
            </td>
        </tr>
        <tr>
            <td>Subject</td>
            <td>
                varchar
            </td>
            <td>
                The subject / topic of the message.
                
            </td>
        </tr>
        <tr>
            <td>Regarding</td>
            <td>
                <a href="#type-outpoint">Outpoint</a>
            </td>
            <td>
                The output of the message that this message is regarding (responding to).
                
            </td>
        </tr>
        <tr>
            <td>PublicMessage</td>
            <td>
                <a href="#type-document">Document</a>
            </td>
            <td>
                Tokenized Ltd. announces product launch.
                
            </td>
        </tr>
        <tr>
            <td>Attachments</td>
            <td>
                <a href="#type-document">Document[0]</a>
            </td>
            <td>
                Documents attached to the message.
                
            </td>
        </tr>
</table>

<a name="private-message"></a>

#### Private Message

Generic private message. Sent to another address(es). Encryption is to be used.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>0003</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender creates the transaction.
                
            </td>
        </tr>
        <tr>
            <td>Subject</td>
            <td>
                varchar
            </td>
            <td>
                The subject / topic of the message.
                
            </td>
        </tr>
        <tr>
            <td>Regarding</td>
            <td>
                <a href="#type-outpoint">Outpoint</a>
            </td>
            <td>
                The output of the message that this message is regarding (responding to).
                
            </td>
        </tr>
        <tr>
            <td>PrivateMessage</td>
            <td>
                <a href="#type-document">Document</a>
            </td>
            <td>
                Tokenized Ltd announces product launch.
                
            </td>
        </tr>
        <tr>
            <td>Attachments</td>
            <td>
                <a href="#type-document">Document[0]</a>
            </td>
            <td>
                Documents attached to the message.
                
            </td>
        </tr>
</table>

<a name="reverted-tx"></a>

#### Reverted Tx

A message that contains a bitcoin transaction that was accepted by the network or an agent and then invalidated by a reorg, or zero conf double spend. This serves as on chain evidence of the sending party&#39;s signatures and approval for the given transaction.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>0004</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender creates the transaction.
                
            </td>
        </tr>
        <tr>
            <td>Transaction</td>
            <td>
                varbin
            </td>
            <td>
                Serialized bitcoin transaction that was reverted/invalidated after being accepted.
                
            </td>
        </tr>
</table>

<a name="offer"></a>

#### Offer

A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should have all, or nearly all, of the details required for the receiving party to accept the offer. The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror&#39;s payment/receipt details, etc.). The Offer message is different to a Signature Request message in that it is missing the offeree&#39;s payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction. If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>1001</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender created the offer.
                
            </td>
        </tr>
        <tr>
            <td>Payload</td>
            <td>
                varbin
            </td>
            <td>
                Serialized Bitcoin transaction. The transaction needs data added by another party upon acceptance of offer.
                
            </td>
        </tr>
</table>

<a name="signature-request"></a>

#### Signature Request

Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>1002</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender creates the transaction.
                
            </td>
        </tr>
        <tr>
            <td>Payload</td>
            <td>
                varbin
            </td>
            <td>
                Full serialized bitcoin tx with multiple inputs from different wallets/users.
                
            </td>
        </tr>
</table>

<a name="settlement-request"></a>

#### Settlement Request

A message that contains a multi-contract settlement that needs settlement data added by another contract. Sent to another contract to request data be added.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>1003</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds for when the message sender creates the transaction.
                
            </td>
        </tr>
        <tr>
            <td>TransferTxId</td>
            <td>
                <a href="#alias-bin">TxId</a>
            </td>
            <td>
                Tx Id of the transfer request transaction that triggered this message.
                
            </td>
        </tr>
        <tr>
            <td>ContractFees</td>
            <td>
                <a href="#type-target-address">TargetAddress[0]</a>
            </td>
            <td>
                Contract fees (in bitcoin) and addresses(PKHs) where fees should be paid. Added by each contract as settlement data is added.
                
            </td>
        </tr>
        <tr>
            <td>Settlement</td>
            <td>
                varbin
            </td>
            <td>
                Serialized settlement OP_RETURN that needs data added by another contract.
                
            </td>
        </tr>
</table>

<a name="output-metadata"></a>

#### Output Metadata

Metadata associated with the output. Aka Transaction details. It is used to describe the purpose of the transaction and add other relevant information. Often encrypted (DH, RSA) to make it private for one or more parties. DH for b2b where multiple parties can see the description. RSA or the like for descriptions only visible to one of the transacting parties. Optional

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>1004</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>OutputDescription</td>
            <td>
                varchar
            </td>
            <td>
                A Description that accompanies the output. A transaction description.
                  Can be NULL Example: eg. Invoice 3024, Pay Mike back for camping.
            </td>
        </tr>
        <tr>
            <td>Tags</td>
            <td>
                <a href="#alias-uint">uint[0]</a>
            </td>
            <td>
                Predefined values for describing the output.
                
            </td>
        </tr>
        <tr>
            <td>CustomTags</td>
            <td>
                <a href="#type-output-tag">OutputTag[0]</a>
            </td>
            <td>
                Free form text fields for describing the output. Groceries, Moomba Gas Compressor Project, Cash Register 3, Fitness, Entertainment, Special, VIP Section, North Carolina Store, Waitress: Cindy Smith, etc.
                
            </td>
        </tr>
</table>

<a name="distribution"></a>

#### Distribution

An administrator is making a distribution/payout. Used to publicly declare these payments and allow holders to be notified of them via the smart contract agent.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>1005</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>InstrumentCode</td>
            <td>
                <a href="#alias-bin">InstrumentCode</a>
            </td>
            <td>
                A unique code that is used to identify the instrument. It is generated by hashing the contract public key hash and the instrument index. SHA256(contract PKH &#43; instrument index)

                Cannot be changed by the administration, operator or smart contract. This field is always required.
            </td>
        </tr>
        <tr>
            <td>Timestamp</td>
            <td>
                <a href="#alias-uint">Timestamp</a>
            </td>
            <td>
                Timestamp in nanoseconds of when the administrator initiated the distribution.

            </td>
        </tr>

</table>

<a name="initiate-relationship"></a>

#### Initiate Relationship

A message used to initiate a new relationship between 2 or more parties. The M1 container specifies the sender tx input and requested participant tx outputs. If there are more than 2 parties the encryption secret provided in the envelope protocol is used as the base encryption secret. If there are only 2 parties, then the ECDH secret of each key pair is used to encrypt each message.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>2001</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Type</td>
            <td>
                uint(1)
            </td>
            <td>
                The type or purposed of the relationship. 0 - Conversation (direct messages), 1 - Channel (entity/business to entity/business)
                
            </td>
        </tr>
        <tr>
            <td>Seed</td>
            <td>
                varbin
            </td>
            <td>
                The seed used to derive keys for the relationship.
                
            </td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>
                varbin
            </td>
            <td>
                The flag can optionally be used to identify messages in the relationship so that all members don&#39;t have to be tagged in each message. It isn&#39;t needed for two party relationships, but is recommended for relationships with more members. It will be included in it&#39;s own op return for all message transactions. It is recommended to be a random 20 byte value similar to public key hashes. The flag will be the Payload of an Envelope protocol message with a Payload Protocol ID of &#34;F&#34;. If this value is not specified then there must be an output to the next key in the relationship chain for every member in the group.
                
            </td>
        </tr>
        <tr>
            <td>EncryptionType</td>
            <td>
                uint(1)
            </td>
            <td>
                Type of encryption used for messages within the relationship. 0 - Encryption keys embedded in envelope protocol. 1 - Encryption key embedded in this message is used as base key for future messages. Used for relationships with more than 2 members so the encryption key doesn&#39;t have to be encrypted to each member in every message.
                
            </td>
        </tr>
        <tr>
            <td>ProofOfIdentityType</td>
            <td>
                <a href="#alias-uint">ProofOfIdentityType</a>
            </td>
            <td>
                The type/format of the sender&#39;s proof of identity.
                
            </td>
        </tr>
        <tr>
            <td>ProofOfIdentity</td>
            <td>
                varbin
            </td>
            <td>
                Sender&#39;s proof of identity.
                
            </td>
        </tr>
        <tr>
            <td>ChannelParties</td>
            <td>
                <a href="#type-channel-party">ChannelParty[0]</a>
            </td>
            <td>
                Information about the entities in the channel. Not included if this is not a channel initiation. These represent the companies in a channel. A channel is recommended to have 2 entities and several individual members per party. The individual members can discuss terms while the parties are used for official actions.
                
            </td>
        </tr>
</table>

<a name="pending-accept-relationship"></a>

#### Pending Accept Relationship

A pending accept to a relationship that provides information about a requested participant.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>2002</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>ProofOfIdentityType</td>
            <td>
                <a href="#alias-uint">ProofOfIdentityType</a>
            </td>
            <td>
                The type/format of the sender&#39;s proof of identity.
                
            </td>
        </tr>
        <tr>
            <td>ProofOfIdentity</td>
            <td>
                varbin
            </td>
            <td>
                Sender&#39;s proof of identity.
                
            </td>
        </tr>
</table>

<a name="accept-relationship"></a>

#### Accept Relationship

Accept a relationship.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>2003</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>ProofOfIdentityType</td>
            <td>
                <a href="#alias-uint">ProofOfIdentityType</a>
            </td>
            <td>
                The type/format of the sender&#39;s proof of identity.
                
            </td>
        </tr>
        <tr>
            <td>ProofOfIdentity</td>
            <td>
                varbin
            </td>
            <td>
                Sender&#39;s proof of identity.
                
            </td>
        </tr>
</table>

<a name="relationship-amendment"></a>

#### Relationship Amendment

Amend a relationship. Add/Remove members. Modify permissions. This is encrypted with the current base encryption secret, but can provide a new base encryption secret that starts after this message.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>2004</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Seed</td>
            <td>
                varbin
            </td>
            <td>
                The new seed used to derive keys for the relationship after this message.
                
            </td>
        </tr>
        <tr>
            <td>BaseEncryptionSecret</td>
            <td>
                varbin
            </td>
            <td>
                The new base encryption secret used to derive encryption secrets for the relationship after this message. Each time a message is sent, the current seed hash is added to the base encryption secret and that value is used to encrypt the message.
                
            </td>
        </tr>
        <tr>
            <td>AddMemberIndexes</td>
            <td>
                uint(4)
            </td>
            <td>
                Indexes to the outputs of the members that are being added to the group.
                
            </td>
        </tr>
        <tr>
            <td>DropMemberIndexes</td>
            <td>
                uint(4)
            </td>
            <td>
                Indexes to the outputs of the members that are being removed from the group.
                
            </td>
        </tr>
</table>

<a name="initiate-thread"></a>

#### Initiate Thread

Start a thread from within a conversation or channel.

<table>
    <tr>
        <th style="width:15%">Message Code</th>
        <td>2005</td>
    </tr>
</table>

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr>
            <td>Flag</td>
            <td>
                varbin
            </td>
            <td>
                The flag is required to identify messages in the thread so that all members don&#39;t have to be tagged in each message. It is recommended to be a random 20 byte value similar to public key hashes. The flag will be the Payload of an Envelope protocol message with a Payload Protocol ID of &#34;F&#34;
                
            </td>
        </tr>
        <tr>
            <td>Seed</td>
            <td>
                varbin
            </td>
            <td>
                The seed used to derive keys for the thread. If this value is not specified, then the original seed value from the parent conversation or channel is used.
                
            </td>
        </tr>
</table>
