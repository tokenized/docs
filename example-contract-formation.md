## Bob's Family Trust
Bill is setting up a family trust to share assets recently passed to him and his siblings Angela and Chris through an estate distribution.
Bill's lawyer, Daniel, establishes a set of contract rules to create a contract giving each sibiling an equal stake in the distribution of the assets, but which makes Bill, Angela and Chris equal managers in the issuance of the contract and associated assets.
The lawyer and Bill's family agree on the terms and the contract is clearly described in English with a paper copy signed by all parties including Daniel.
The signed copy is then scanned and a hash of the document created.

Subsequently, a Contract Offer is created that establishes the smart contract incorporating all the rules laid out in the agreement. Because the three family members are the only ones involved in the contract, the rules are set up such that the issuer can make unilateral modifications at any time.

This is done by setting each set of three authorisation flags to 100 for every contract parameter. This setting enables the Issuer to manage all changes without the need for votes.
The contract issuer is listed as the BillAngelaChris Family trust. The definition of the issuer includes details such as an administrative address, and key persons. Bill, Angela and Chris are listed as the directors of the contract, and Daniel as the lawyer. 

Becuase the nature of the contract is simple, the trust uses a third party operator to manage the contract on their behalf. They select Tokenized Contract Operations (TCO) who's details are publicly available and their details are added into the operator definition field.
An issuer proposal is added to the contract which stipulates that the only people authorised to hold assets under the contract are the three directors. To keep it simple, they elect not to use a registry to confirm their own addresses for asset transfers, electing instead to manage it through off-chain means.
The Contract Offer is assembled in full and double checked by Daniel to ensure it will pass the contract validation process used by the Tokenized platform. Once all the details have been double checked, the Contract Offer transaction is packaged into a Message action using the 'Signature Request' message type and sent to the TCO platform. The trust knows what fees it needs to pay based on the public information provided by TCO.

/// INSERT IMAGE

The Contract Offer is sent to an address which is provided to the issuer by TCO. It corresponds to an address controlled by their Tokenized platform which is exclusively for the control of the BillAngelaChris family trust. This is the only contract that will be hosted at this address.

The platform receives the Contract Offer and and unpacks the transaction. Once the conditions that are specified for the establishment of the contract are proven to be valid, the platform sends a Contract Formation action from the contract address. From this moment, the smart contract can be considered live and is ready to create, distribute and manage assets.

/// INSERT IMAGE

Asset Creation - Home
Home Distribution
Asset Creation - Jewellery
Jewellery Distribution
Asset Creation - Bullion
Bullion Distribution
Bullion swap for home
