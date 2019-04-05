## Bill's Family Trust
Bill is setting up a family trust to share a home recently passed to him and his siblings Angela and Chris through an estate distribution.
Bill's lawyer, Daniel, establishes a set of contract rules to create a contract giving each sibiling an equal stake in the home, but which makes Bill, Angela and Chris equal managers in the issuance of the contract and associated assets.
The lawyer and Bill's family agree on the terms and the contract is clearly described in English with a paper copy signed by all parties including Daniel.
The signed copy is then scanned and a hash of the document created.
This document is used to establish a legal entity called 'The BillAngelaChris trust' (TBACT) which will be the owner of the home.

Subsequently, a Contract Offer is created that establishes the smart contract incorporating all the rules laid out in the agreement. Because the three family members and Daniel are the only ones involved in the contract, the rules are set up such that the issuer can make unilateral modifications at any time.
The contract issuer is listed as the TBACT and includes details such as an administrative address, and key persons. Bill, Angela and Chris are listed as the directors of the contract, and Daniel as the lawyer. 

Becuase the nature of the contract is simple, the trust uses a third party operator to manage the contract on their behalf. They select Tokenized Contract Operations (TCO) who's details are publicly available and their details are added into the operator definition field.
An issuer proposal is added to the contract which stipulates that the only people authorised to hold assets under the contract are the three beneficiaries.
The Contract Offer is assembled in full and double checked by Daniel to ensure it will pass the contract validation process used by the Tokenized platform. Once all the details have been double checked, the Contract Offer transaction is packaged into a Message action using the 'Signature Request' message type and sent to the TCO platform. The offer transaction is sent with the necessary fees attached which are based on the public information provided by TCO.

/// INSERT IMAGE

The Contract Offer is sent to an address which is provided to the issuer by TCO. It corresponds to an address controlled by their Tokenized platform which is exclusively for the control of TBACT.

The platform receives the Contract Offer and and unpacks the transaction. Once the conditions that are specified for the establishment of the contract are proven to be valid, the platform sends a Contract Formation action from the contract address. From this moment, the smart contract can be considered live and is ready to create, distribute and manage assets.

/// INSERT IMAGE

The only asset being created under this contract for now is the family home. Daniel creates an Asset Definition to send to the contract using asset type RRE (Residential Real Estate - release pending) which creates a Tokenized asset that represents the home. Included in the Asset Definition action are details such as the home's address, property title, links to photographs and scanned copies of the deed, council allotments and surveying data. The files are all loaded onto the Blockchain ensuring that the full detail of the contract will always be available.
The definition also breaks the asset down into 300 fungible tokens, to allow the equity to be distributed amongst the trustees.
Once the Asset Definition is complete, Daniel sends it to the Trust's smart contract:

/// INSERT IMAGE

Now that the home has been tokenized, the trust is able to distribute it to the trustees. This is done in a single Transfer action, which sends 100/300 of the tokens to each of the trustees:

/// INSERT IMAGE

Now that the ownership of the home has been established, the Tokenized platform can be used to create dividends for each of the asset owners when rental income is distributed. The trustees decide to rent the home and their accountant provides quarterly funds for distribution.
