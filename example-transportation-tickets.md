# Transportation Tickets

- [Introduction](#introduction)
- [Private Line](#private-line)
  - [Buying Private Line Tickets](#buying-private-line-tickets)
  - [Boarding The Private Line Train](#boarding-private-line-train)
  - [Ticket Inspection](#ticket-inspection)
- [The Metro](#the-metro)

<a name="introduction"></a>
## Introduction

Caitlyn has just relocated to a new home which is a fair distance from the center of the city where she works. As a result, she will need to commute every day from a remote train station to her office in the city. In doing so, she crosses the border between the Private Line train system which is run by a private corporation, and a municipal metro run by the city council. This means that she needs separate tickets for her travel each day.

<a name="buying-private-line-tickets"></a>
## Buying Private Line Tickets

The private line is most cost effective when she buys 10 pass tickets once a week. The tickets are general in nature and allow her to travel on any train between stations within zonal boundaries. Her tickets are 4 zone tickets. To purchase the ticket she uses a ticketing terminal at the train station which accepts tokenized Australian Dollars (eAUD).
She approaches the terminal to buy a new 10 pass. After selecting the appropriate options her wallet is given a Transfer action template via NFC requesting the transfer of $72.50 in exchange for 10 ride tokens.

![Private Line Transfer Template](https://raw.githubusercontent.com/tokenized/docs/master/images/private-line-transfer-template.svg?sanitize=true "Private Line Transfer Template") {.frame .centered .padded}

Caitlyn accepts the offer and her wallet adds some inputs from AUD carrying addresses and signs them. Caitlyn is then instructed to touch the terminal again, and her phone sends the signed transaction back to the interface for final signature and transmission to the network.

![Private Line Final Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/private-line-final-transfer.svg?sanitize=true "Private Line Final Transfer") {.frame .centered .padded}

The ticketing smart contract receives her order and builds a settlement transaction sending the ticket back to her wallet a short time later.

![Private Line Settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/private-line-settlement.svg?sanitize=true "Private Line Settlement") {.frame .centered .padded}

<a name="boarding-private-line-train"></a>
### Boarding the Private Line Train

Now that she has her tickets, Caitlyn walks to the entrance to the platforms. She taps her device on the NFC panel on the turnstyle she wants to use and the following sequence takes place:

![Private Line Turnstile Operation](https://raw.githubusercontent.com/tokenized/docs/master/images/private-line-turnstile.svg?sanitize=true "Private Line Turnstile Operation") {.frame .centered .padded}

Because Caitlyn must transfer a token to the turnstyle each time she boards, the mechanism that manages the number of tokens she has is simply her token balance. If she doesn't have any valid tickets in her wallet, she will be unable to activate the turnstyle and access the platform.

<a name="ticket-inspection"></a>
### Ticket Inspection

About 15 minutes after the train is underway, Caitlyn is approached by a ticket inspector. He proffers her a device that has an NFC pad on the front which she taps with her phone. In order to prevent her from taking a copy of an on-chain transaction, the inspection device requests that the wallet sign a new messsage that includes a full copy of the most recent settlement transaction sent to her wallet from the Private Line smart contract using the same private key used to sign the transfer.

//// Message with signature

The wallet performs the signature and passes it back to the device, which validates it. The device flashes green and the ticket inspector thanks her and moves on.

Upon arriving at the central station, Caitlyn disembarks and walks out of the platform. She has to scan her device on a turnstyle one more time. This makes the same request as the ticket inspector's device, askign the wallet to sign the most recent settlement in her wallet from the smart contract. It sees that this is the settlement of a zone 4 ticket transfer to a turnstyle within a 4 zone radius of Central station, and opens the gate.

<a name="the-metro"></a>
## The Metro

Caitln walks across to the entrance of the subway. She enters the line and when she gets to the turnstyle she taps her device. The following sequence of events takes place:

//// Metro Ticket Check with signature

She checks her wallet and discovers that indeed, her last monthly token expired the day before. Slightly embarrased, and now in a hurry, she walks to a nearby terminal. Tapping the device on the NFC pad, she selects to purchase a monthly ticket. Caitlyn is a local student which allows her to purchase a ticket at concession rates rather than paying full price. The terminal queries her wallet for a student ID key which it sends to the Metro authority concession oracle. The oracle is able to see which institution issued the address and queries its oracle for her enrolment status. The University oracle confirms that she is currently studying there, and the Metro authority signs a message allowing her to purchase a concession price ticket.

//// Transaction Template

This message is packaged into a transaction template and given back to her wallet via the NFC connection after 1.2 seconds, and the screen tells her to confirm the transaction on her device, which she does, before touching it to the NFC pad once more. The signed Transfer transaction is sent to the network where it is settled by the Metro smart contract and the Australian Dollar contract.

//// Settlement Transaction

Now that Caitlyn has a valid ticket, she re-joins the queue and quickly makes her way to the front. Reaching the tursntyle, she touches her device to its NFC pad, and the following actions take place:

![Metro Turnstyle](https://raw.githubusercontent.com/tokenized/docs/master/images/metro-turnstyle.svg?sanitize=true "Metro Turnstyle") {.frame .centered .padded}

The Turnstyle uses several elements to validate Caitlyn's ticket. Firstly, it provides her device with a one-time password which is a hash generated from a combination of the following:
* The Turnstile's ID (Can be a bitcoin address or even a Hierarchically derived address which changes with each request)
* A timestamp of her checkin
* The current block height
* The 6th most recent block hash

Caitlyn's wallet signs the hash using the same private key associated with the address that received the ticket and sends both the signature and the transaction ID from the ticket settlement back to the turnstyle. The Turnstyle sends the signed message, the TXID and the information it used to generate the hash back to the Metro's back end server for validation.
The server checks the signature and responds to the turnstlye, informing it that the ticket is valid.

When Caitlyn's wallet signs the OTP, the resultant signature is passed from the turnstile back to the Oracle server which checks that the ticket that she has provided is valid. It validates the signature against the settlement the contract sent for Caitlyn's ticket purchase and checks that the turnstile ID, timestamp and block hashes are all consistent with its situational view.

### Managing Multi Trip Tickets

Caitlyn's ticket is valid for 10 trips, however the ticket itself is a single token and there is no on-chain action involved in her gaining access to the platform. 

It then stores the details of the signature in a local repository that it manages. 
When a passenger uses the final trip on a given ticket, the oracle instructuct the smart contract to perform a confiscation action on the ticket, and it is recycled into the pool of available tokens.

