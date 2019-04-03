# Authorization Flags

Authorization flags are contract terms and conditions that are controlled by the smart contract.  Most fields in the Contract Formation and Asset Creation actions are subject to changes by way of an Amendment action or a Modification action.  The authorization flags that are listed in the Contract Formation and Asset Creation actions are capable of specifying whether those fields can be changed, and if so, what conditions they can be changed under.

There are two different authorization flags that are functionally equivalent, they just control the fields of different actions. The first is the contract authorization flags defined in the Contract Offer action and specified in the Contract Formation action.  The second is the asset authorization flags defined in the Asset Definition action and specified in the Asset Creation action.

There are a number of fields that are likely to be subject to an amendment/modification at some point during the life of the contract.  Common examples include the fields that specify the issuer's identifying details (registered address, issuer name, communication details, etc.), the quantity of tokens (eg. share dilution or buy back) or even the terms and conditions of the contract itself.  The fields within an action are ordered and can be referenced by their sequential position called the index value (represented by N below).

The authorization flags are represented by 3 bits (XYZ) per field plus an array of booleans to represent all of the Voting Systems specified in the Contract Formation action of the contract.  

The first bit (X) specifies whether unilateral changes are allowed to be made to the field by the issuer. 1 = Permitted, 0 = Not Permitted.  

The second bit (Y) specifies whether a successful issuer-initiated vote will permit a change to be made. 1 = Issuer Proposals are Permitted, 0 = Issuer Proposals are not Permitted.  

The third bit (Z) specifies whether a successful token holder-initiated vote will permit a change to be made. 1 = Token Holder Proposals are Permitted, 0 = Token Holder Proposals are not Permitted.

The booleans that make up the array of M represent a voting system (by index) and a value of 1 = that voting system controls the field, 0 = that voting system does not control that field.  If a proposal was made to vote on a change for a field, the vote system selected for that field would have to be used, otherwise the smart contract will reject it.

For Field[N]:

ContractAuthFlags = XYZM[] 

AssetAuthFlags = XYZM[]

where X = Permitted, Y = Issuer Proposal, Z = Token Holder Proposal and N = the index of the field within the action, M[] = an array of booleans equal to the # of voting systems in the contract. If Y and Z are false, then M is empty.

When you parse the authorization flags, you get an array of permission objects containing XYZM[] that has a length corresponding the the number of fields in the contract or asset.  The Contract Offer and Asset Creation is used to determine the indexes of the fields.  Index 0 is the field after the header.

## Example

The Contract Name field in the contract is controlled by a permission object within the Contract Authorization Flags.  The contract has 11 voting systems and voting system 5 will be used for any vote proposals put forward to change the Contract Name field.  The Contract Name field cannot be changed except with approval from the token holders by way of a token holder vote proposed by the issuer.  Token holders cannot initiate a vote to change the Contract Name field.

A permission object for the Contract Name field with these settings would look like this:

