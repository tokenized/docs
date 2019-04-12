# Governance

- [Introduction](#introduction)
- [Authorisation flags](#auth-flags)
- [Voting Systems](#voting-systems)
- [Creating and Running a Vote](#vote-create)
    - [Proposal](#vote-proposal)
    - [Vote](#vote-vote)
    - [Ballot Cast](#vote-ballot-cast)
    - [Ballot Count](#vote-ballot-count)
    - [Result](#vote-result)

<a name="introduction"></a>
## Introduction

The Tokenized protocol includes a complete governance system that allows for organizational governance to be carried out on-chain and within the rules of the organiztion and within the laws and regulations of any jurisdiction.  The governance tools allow for expressive control over almost any field of data, which can be modified, for a contract or asset. The governance model also extends to organizational matters/proposals that exist outside of the blockchain (eg. a shareholder votes on a company matter).  These settings are all controlled by authorisation flags that are specified in the most recent revision of the Contract Formation or Asset Creation actions issued by the contract.

Where a field in a Contract Formation or Asset Creation has been set to allow for 'unilateral' changes to be made, then the issuer may make changes to this field without needing the authority of affected token holders through a vote process. This means that the fields can be changed at any time without restriction.

Where a field in a Contract Formation or Asset Creation has been set to require a positive outcome from a Referendum, the Contract Amendment or Asset Modification action that contains the change will need to contain a TXID that references a Result action that counts the votes in a link to the modification of that parameter. 

<a name="auth-flags"></a>
## Authorisation flags

When a contract or asset is created, there are a set of authorisation flags which are defined in the Contract Offer or Asset Definition action. These flags determine for each parameter that can be changed what the minimum requirement for making a change is. Each field has three flags, which each define whether or not a particular governance mechanism can be used to modify that field. To enable the mechanism related to each flag they must be set to 'True' (binary 1). The three flags correspond to the enablement of the following change mechanisms:

1. Issuer can change unilaterally
2. Issuer must hold a token holder vote leading to a postive result in line with voting systems (Issuer initiates the proposal)
3. Parameter can only be changed after a token holder requested vote leads to a postive result as defined by voting systems (A token holder initiates the proposal)

Each parameter has a set of three flags which are represented as a sequential set of three bits within the Authorisation Flags element of the contract or asset. Where parameters are a variable length array type, the flag settings apply to the whole array.

<a name="voting-systems"></a>
## Voting Systems

Voting systems can be set up to provide a complex and layered approach to governance. Individual settings within individual assets or contracts can have voting mechanisms that differ from all other voting systems in that contract or asset. The exception to this is that the rules that forbid the creation of a vote through referendum or initiative that apply to a contract also apply to the assets in that contract.
When a vote is performed, the result of each proposed amendment will be counted in-line with the specific voting rules attached to that field. The different ways of counting are as follows:

#### R - Relative Threshold

Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast. Abstentions/spoiled votes do not detract from the liklihood of a motion passing as they are not included in the denominator.  

#### A - Absolute Threshold

Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens. Abstentions/spoiled votes detract from the liklihood of the motion/proposal passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the motion cannot pass.  50% of all tokens would have had to vote for one vote option for the motion to be successful."

#### P - Plurality
In a Plurality vote, the option with the most votes is the winner.  No threshold percentage is required.

#### Tally Logic

- **Standard Scoring:** Choice * # of tokens held * vote multiplier 

- **Weighted Scoring:** 1st choice * 1 * # of tokens held * vote multiplier, 2nd choice * ((Vote Max-1)/Vote Max) * # of tokens held * vote multiplier,..etc. 

> **Note**: Vote multipliers are optional and can be restricted.

<a name="vote-create"></a>
## Creating and Running a Vote

There are two ways for a vote action to be created, both using the Proposal Action.

The following image defines the order of operations in which a vote takes place:

![The order of operations for a Voting process](https://raw.githubusercontent.com/tokenized/docs/master/images/vote-order-of-operations.svg?sanitize=true "The order of operations for a Voting process") {.frame .centered .padded}

<a name="vote-proposal"></a>
### Proposal

A Proposal is the means by which a vote action which is called. Proposals can be created in two ways: 

#### Referendum

A Referendum is called by sending a Proposal action to the smart contract with the issuer signing and sending the action from its public address. Referendums can be called at any time and the cost is only the contract fees needed for the vote, and any transaction fees.

#### Initiative

An Initiative is a vote initiated by a token holder of a token that has initiative rights. Any token holder regardless of the number of tokens they hold can call an initiative, as long as the Initiative Cost is paid. The initiative cost is a threshold that sets a floor on the cost of creating an initiative. It is a fee paid to the contract issuer.  As long as the fee is paid the proposal will be put to all token holders and can be binding depending on the proposal.  The initiative cost is meant to reduce spam/wasting token holder's time.

![A Proposal action](https://raw.githubusercontent.com/tokenized/docs/master/images/proposal-action.svg?sanitize=true "A Proposal action") {.frame .centered .padded}

<a name="vote-vote"></a>
### Vote

Once the smart contract receives the valid Proposal action, it creates a Vote action. The vote action is sent from the contract to itself, which is an indicator to all wallets that it is a message they should read. When user wallets see the vote action, the user is presented with all the options in the vote and can select their choices.

The Vote action itself is very simple, and contains only the timestamp when the vote was created. The action is created by spending the UTXO associated with the Proposal action it is creating the vote for. Wallets refer back to the Proposal action to build the voting interface for the user.

There is no restriction on the number of Vote actions that can be active at once however the contract will reject a vote for a change to a field in a contract or asset that is already under an active Vote action, or which has had a successful Vote action that stipulates a change that has not yet been made. The vote results themselves do not activate any changes to the smart contract. It is still up to the issuer to create and send an Asset Modification or Contract Amendment action that implements the changes that have been voted on. If a Vote action results in the successful passage of an amendment order, the contract will not allow further votes on that field until the changes.

![A Vote action](https://raw.githubusercontent.com/tokenized/docs/master/images/vote-action.svg?sanitize=true "A Vote action") {.frame .centered .padded}

<a name="vote-ballot-cast"></a>
### Ballot Cast

Once the user's wallet sees the Vote action, it can build the ballot for the user. The ballot consists of a set of response fields that display the proposal and voting options detailed in the Proposal action. Once the user has selected their choice(s) the wallet builds a Ballot Cast action. If a user has more than one asset with voting rights in a contract, their votes will be cast against their full asset holdings in aggregate. The counting is performed by the smart contract. 

![A Ballot Cast action](https://raw.githubusercontent.com/tokenized/docs/master/images/ballot-cast-action.svg?sanitize=true "A Ballot Cast action") {.frame .centered .padded}

<a name="vote-ballot-count"></a>
### Ballot Count

When the smart contract sees that the user has cast their vote using a valid Ballot Cast action, it responds with a Ballot Counted action that acknowledges the receipt of the Ballot Cast action. The contract spends the UTXO that carried the Ballot Cast action to enable the wallet to track which vote is being responded to. The action only contains a timestamp from when the Ballot Counted action was created.

![A Ballot Cast action](https://raw.githubusercontent.com/tokenized/docs/master/images/ballot-counted-action.svg?sanitize=true "A Ballot Cast action") {.frame .centered .padded}

<a name="vote-result"></a>
### Result

When the time elapses on the vote, the smart contract tallies the ballots cast against each option. The full details of the changes from the Proposal are repeated with a pass or fail result based on the voting system, and the number of votes received.

![A Result action](https://raw.githubusercontent.com/tokenized/docs/master/images/result-action.svg?sanitize=true "A Result action") {.frame .centered .padded}

Once the result action has been published, the Vote is concluded and the issuer can act on the amendments that have passed.
