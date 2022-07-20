# Family Trust

- [Introduction](#introduction)
- [Creating the Contract](#creating-the-contract)
  - [Contract Offer](#contract-offer)
  - [Contract Formation](#contract-formation)
- [Creating the instruments](#creating-the-instruments)
  - [Instrument Definition](#instrument-definition)
  - [Instrument Creation](#instrument-creation)
- [Instrument Distribution](#instrument-distribution)
  - [Transfer](#transfer)
  - [Settlement](#settlement)

<a name="introduction"></a>

## Introduction

Bill is setting up a family trust to share instruments recently passed to him and his siblings, Angela and Chris, through an estate distribution.

Bill's lawyer, Daniel, establishes a set of contract rules to create a discretionary trust to hold the instruments. The lawyer and Bill's family agree on the terms and the contract is transcribed into the Tokenized Body of Agreement format to be inscribed into the Contract Offer.

In a video conference with all three siblings, Daniel starts to prepare a smart contract using the Tokenized desktop wallet.

<a name="creating-the-contract"></a>

## Creating the Contract

Using the Contract Creation , Daniel creates the Contract Offer using the agreed upon details to build the action. These are as follows:

Contract Name: The BillAngelaChris Trust Smart Contract
Body of Agreement Type: SHA-256 Hash
Body of Agreement: A hash of the document files
Contract Type: Discretionary Trust
Supporting Docs File Type: 7zip
Supporting Docs: A 7zip file containing supporting docs including the contract used to make the body of agreement hash
Governing Law: Australia
Jurisdiction: Australia
Contract Expiration: Contract is set to operate for 10 years
Issuer: Discretionary Trust: The BillAngelaChris Trust
Email: Shared TBACT email
Phone no: Daniel's office phone
Administration - Beneficiary: Bill
Beneficiary: Angela
Beneficiary: Chris
Contract Operator Included?: Yes
Contract Operator: Tokenized
Contract Authorisation Flags: Administration can amend all fields. Referendums and initiatives are unable to be used.
Contract Fee: As per the detail in the Tokenized operator agreement

Once the contract Contract Offer is created it is double checked by Daniel to ensure it will pass the contract validation process used by Tokenized. Daniel creates a Bitcoin address where the contract will receive it's instructions and directs the output of the Contract Offer to this address. He then sends the Contract Offer to Tokenized using the operator endpoint given in the app. Tokenized signs the transaction and the Contract Offer is sent with the necessary fees attached to the smart contract address.

<a name="contract-offer"></a>

### Contract Offer

![The BobAngelaChris Trust Contract Offer](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-contract-offer.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Contract Offer</span>

<a name="contract-formation"></a>

### Contract Formation

The platform receives the Contract Offer and and unpacks the transaction. Once the conditions that are specified for the establishment of the contract are proven to be valid, the platform sends a Contract Formation action from th

![The BobAngelaChris Trust Contract Formation](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-contract-formation.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Contract Formation</span>

<a name="creating-the-instruments"></a>

## Creating the instruments

The only instrument being created under this contract are shares in the trust itself. The trust owns the home and manages it on behalf of the trust beneficiaries. Daniel creates an Instrument Definition to send to the contract using instrument type SHC (Common Shares).
The definition breaks the ownership of the trust down into 300 fungible tokens, to allow the equity to be distributed amongst the trustees.

<a name="instrument-definition"></a>

### Instrument Definition

Once the Instrument Definition is complete, Daniel sends it to the Trust's smart contract:

![The BobAngelaChris Trust Share Definition](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-instrument-definition.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Share Definition</span>

<a name="instrument-creation"></a>

### Instrument Creation

The contract responds with an Instrument Creation action, allocating the 300 shares to the Issuer's wallet.

![The BobAngelaChris Trust Share Creation](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-instrument-creation.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Share Creation</span>

<a name="instrument-distribution"></a>

## Instrument Distribution

Now that the home has been tokenized, the trust is able to distribute it to the trustees. This is done in a single Transfer action, which sends 100/300 of the tokens to each of the trustees:

<a name="transfer"></a>

### Transfer

![The BobAngelaChris Trust Share Transfer](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-instrument-transfer.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Share Transfer</span>

<a name="settlement"></a>

### Settlement

After receiving and evaluating the transfer, the Smart Contract responds with a settlement transaction.

![The BobAngelaChris Trust Share settlement](https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-instrument-settlement.svg?sanitize=true)
<span name="image-label">The BobAngelaChris Trust Share settlement</span>

Now that the ownership of the trust has been established, the Tokenized platform can be used to create dividends for each of the instrument owners when rental income is distributed. The trustees decide to rent the home and their accountant provides quarterly funds for distribution.
