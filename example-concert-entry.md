# Concert entry

- [Introduction](#introduction)
- [Ticket Purchase Transfer](#ticket-purchase-transfer)
- [Ticket Purchase Settlement](#ticket-purchase-settlement)
- [4 Months Later](#4-months-later)
- [Entry Pass Redemption Transfer](#entry-redemption-transfer)
- [Entry Pass Redemption Settlement](#entry-redemption-settlement)

<a name="introduction"></a>

## Introduction

Edison is very excited to hear that his favourite band from the late 90's is on it's way to his local entertainment venue and moves immediately to secure a ticket. He goes to the venue's booking interface and selects a VIP ticket including a back stage pass so that he can meet the band members after the show.

<a name="ticket-purchase-transfer"></a>

## Ticket Purchase Transfer

The website provides a Transfer request template for his wallet that purchases a VIP pass in exchange for 0.451BSV.

![Venue's Ticket Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/concert-venue-edison-transfer.svg?sanitize=true)
<span name="image-label">Edison's Ticket Transfer</span>

Edison adds several inputs to the template to reach the 0.451BSV amount needed, plus the cost of the settlement fees before sending the transaction back to the venue for signing. This request/response action is handled off-chain via an API.

<a name="ticket-purchase-settlement"></a>

## Ticket Purchase Settlement

The venue's smart contract responds with a settlement, sending the token to Edison's wallet.

![Venue's Ticket Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/concert-venue-edison-settlement.svg?sanitize=true)
<span name="image-label">Edison's Ticket Settlement</span>

<a name="4-months-later"></a>

## 4 months later

The big night has arrived, and Edison has arrived at the venue where the concert is taking place. He joins the queue for entry into the backstage area and opens his wallet ready to exchange his token for a pass.
When he reaches the front of the queue, he is presented with an address to use to redeem his backstage pass.

<a name="entry-redemption-transfer"></a>

## Entry Pass Redemption Transfer

His wallet prepares a transfer action that requests the token be sent to the given address. The tokens are collected by the security company who are handling the venue entries on the night.

![Edison's Ticket Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/edison-ticket-transfer.svg?sanitize=true)
<span name="image-label">Edison's Ticket Transfer</span>

<a name="entry-redemption-settlement"></a>

## Entry Pass Redemption Settlement

The smart contract receives the transfer order and evaluates it for correctness before building a settlement response. It sends this directly to the network where it is detected by the security company's wallet.

![Edison's Ticket Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/edison-ticket-settlement.svg?sanitize=true)
<span name="image-label">Edison's Ticket Settlement</span>

Edison is given his backstage pass which comes with a commemorative lanyard and is ushered into the waiting area to meet the band...
