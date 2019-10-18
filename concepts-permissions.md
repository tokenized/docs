# Permissions

- [Introduction](#introduction)
- [Representation](#representation)
- [Reference](#reference)

<a name="introduction"></a>
## Introduction

Permissions are contract terms and conditions that are controlled by the smart contract. Most fields in the Contract Formation and Asset Creation actions are subject to changes by way of an Amendment action or a Modification action. The permissions that are listed in the Contract Formation and Asset Creation actions are capable of specifying whether those fields may be changed, and if so, under which conditions they may be changed.

There are two different permission sets that are functionally equivalent, they just control the fields of different actions. The first is the contract permissions defined in the Contract Offer action and specified in the Contract Formation action. The second is the asset permissions defined in the Asset Definition action and specified in the Asset Creation action.

There are a number of fields that are likely to be subject to an amendment/modification at some point during the life of the contract. Common examples include the fields that specify the issuer's identifying details (registered address, issuer name, communication details, etc.), the quantity of tokens (eg. share dilution or buy back) or even the terms and conditions of the contract itself. The fields within an action are ordered and can be referenced by their sequential position called the index value (represented by N below).

<a name="representation"></a>
## Representation

The permissions are represented by 4 bits (WXYZ) plus an array of bits (M). The array of bits represent all of the Voting Systems specified in the Contract Formation action of the contract.

The first bit (W) specifies whether unilateral changes by the administration of the contract issuer are permitted to the field. 1 = Permitted, 0 = Not Permitted.

The second bit (X) specifies whether a successful administration initiated vote will permit a change to the field. 1 = Administration Proposals are Permitted, 0 = Administration Proposals are not Permitted.

The third bit (Y) specifies whether a successful token holder initiated vote will permit a change to the field. 1 = Token Holder Proposals are Permitted, 0 = Token Holder Proposals are not Permitted.

The fourth bit (Z) specifies whether a successful administrative vote will permit a change to the field. 1 = Administrative Votes are Permitted, 0 = Administrative Votes are not Permitted. An administrative vote only allows holders of special Membership tokens where MembershipClass is Owner or Administrator. Only one such asset is allowed per contract. This allows votes by board members or whatever group of people control the contract.

The booleans that make up the array of (M) represent a voting system (by index) and a value of 1 = that voting system may control the field, 0 = that voting system does not control that field. If a proposal is made to vote on a change for a field, one of the voting systems enabled for that field would have to be used, otherwise the smart contract will reject it.

Each WXYZM value defines a permission. Each permission is then followed by a list of fields (F[]) that it applies to. The list of fields is encoded with "base 128 var ints" as defined [here](https://developers.google.com/protocol-buffers/docs/encoding#varints). These values can represent very large numbers, but only use as many bytes as necessary. So smaller values only use one byte, while still leaving the option to specify larger numbers. The first value represents how many fields are associated with the permission, then each field is encoded after that.

Each field is represented by a list of indexes specifying the path to the field. The first index is the index of the field in the top level object like the contract or asset. Then, if that field is "complex" (containing multiple fields within it), the next index is a index of a field in that object. This can be continued for as deep as the structure is. The first value in a field index is the number of indexes that it specifies, or its depth. Then each index value follows.

    F[] = (field count(index count(indexes)))

    ContractPermissions = (WXYZMF[])[]

    AssetPermissions = (WXYZMF[])[]

where W = Permitted, X = Administration Proposal, Y = Token Holder Proposal, Z = Administrative Vote, and N = the index of the field within the action, M[] = an array of booleans equal to the # of voting systems in the contract. If X, Y, and Z are false, then M is empty (zero length).

When you parse the permissions, you get an array of permission objects containing (XYZMF[])[]. The Contract Offer and Asset Creation is used to determine the indexes of the fields. Index 1 is the field after the header.

<a name="reference"></a>
## Reference

Helper functions for serializing, field indexes, and templates are provided as part of the reference implementation. 

Serializing functions are in [permission.go](https://github.com/tokenized/specification/blob/master/dist/golang/actions/permission.go)

The field indexes are in [amendments.go](https://github.com/tokenized/specification/blob/master/dist/golang/actions/amendments.go). The same values are used for specifying fields in amendments.

In practice, permission settings for Contracts and Assets won't vary too much. Laws require companies to manage certain aspects of the company in certain ways. For example, in the UK, changes to the name of a company require a special resolution (shareholder vote) and a minimum approval threshold of 75% to be lawful. Permission templates are in [permission_templates.go](https://github.com/tokenized/specification/blob/master/dist/golang/actions/permission_templates.go).
