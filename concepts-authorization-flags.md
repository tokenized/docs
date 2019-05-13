# Authorization Flags

- [Introduction](#introduction)
  - [Representation](#representation)
- [Example](#example)

<a name="introduction"></a>
## Introduction

Authorization flags are contract terms and conditions that are controlled by the smart contract. Most fields in the Contract Formation and Asset Creation actions are subject to changes by way of an Amendment action or a Modification action. The authorization flags that are listed in the Contract Formation and Asset Creation actions are capable of specifying whether those fields may be changed, and if so, under which conditions they may be changed.

There are two different authorization flags that are functionally equivalent, they just control the fields of different actions. The first is the contract authorization flags defined in the Contract Offer action and specified in the Contract Formation action. The second is the asset authorization flags defined in the Asset Definition action and specified in the Asset Creation action.

There are a number of fields that are likely to be subject to an amendment/modification at some point during the life of the contract. Common examples include the fields that specify the issuer's identifying details (registered address, issuer name, communication details, etc.), the quantity of tokens (eg. share dilution or buy back) or even the terms and conditions of the contract itself. The fields within an action are ordered and can be referenced by their sequential position called the index value (represented by N below).

<a name="representation"></a>
### Representation

The authorization flags are represented by 3 bits (XYZ) plus an array of bits per field. The array of bits represent all of the Voting Systems specified in the Contract Formation action of the contract.

The first bit (X) specifies whether unilateral changes by the administration of the contract issuer are permitted to the field. 1 = Permitted, 0 = Not Permitted.

The second bit (Y) specifies whether a successful administration initiated vote will permit a change to the field. 1 = administration Proposals are Permitted, 0 = administration Proposals are not Permitted.

The third bit (Z) specifies whether a successful token holder initiated vote will permit a change to the field. 1 = Token Holder Proposals are Permitted, 0 = Token Holder Proposals are not Permitted.
so 
The booleans that make up the array of M represent a voting system (by index) and a value of 1 = that voting system may control the field, 0 = that voting system does not control that field. If a proposal is made to vote on a change for a field, one of the voting systems enabled for that field would have to be used, otherwise the smart contract will reject it.

    For Field[N]:

    ContractAuthFlags = XYZM[]

    AssetAuthFlags = XYZM[]

where X = Permitted, Y = administration Proposal, Z = Token Holder Proposal and N = the index of the field within the action, M[] = an array of booleans equal to the # of voting systems in the contract. If Y and Z are false, then M is empty (zero length).

When you parse the authorization flags, you get an array of permission objects containing XYZM[] that has a length corresponding the the number of fields in the contract or asset. The Contract Offer and Asset Creation is used to determine the indexes of the fields. Index 0 is the field after the header.

Helper functions are provided in the reference implementation to help with serializing auth flags.
[authorization.go](https://github.com/tokenized/specification/blob/master/dist/golang/protocol/authorization.go)

<a name="example"></a>
## Example

In practice, authorization flag settings for Contracts and Assets won't vary too much. Laws require companies to manage certain aspects of the company in certain ways. For example, in the UK, changes to the name of a company require a special resolution (shareholder vote) and a minimum approval threshold of 75% to be lawful.

The contract authorization flags for a typical private company's shareholder agreement might look something like this:

![Authorization Flags](https://raw.githubusercontent.com/tokenized/docs/master/images/authorization-flags.svg?sanitize=true "Authorization Flags") {.frame .centered .padded}
