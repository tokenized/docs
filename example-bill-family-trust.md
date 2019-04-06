## Bill's Family Trust
Bill is setting up a family trust to share a home recently passed to him and his siblings Angela and Chris through an estate distribution.
Bill's lawyer, Daniel, establishes a set of contract rules to create a contract giving each sibiling an equal stake in the home, but which makes Bill, Angela and Chris equal owners of the contract and associated assets. Daniel also establishes a 2 of 3 multisignature address where each of Bill, Angela and Chris have a signature. This will enable any two of the three beneficiaries to sign issuer instructions to the smart contract.
The lawyer and Bill's family agree on the terms and the contract is clearly described in English with a paper copy signed by all parties including Daniel.
The signed copy is then scanned and a hash of the document created.
This document is used to establish a legal entity called 'The BillAngelaChris trust' (TBACT) which will be the owner of the home.

Subsequently, a Contract Offer is created that establishes the smart contract incorporating all the rules laid out in the agreement. Because the three family members and Daniel are the only ones involved in the contract, the rules are set up such that the issuer can make unilateral modifications at any time.
The contract issuer is listed as the TBACT and includes details such as an administrative address, and key persons. Bill, Angela and Chris are listed as the beneficiaries of the trust, and Daniel as the lawyer. 

Now they begin to assemble the details for the creation of their smart contract. Because the nature of the contract is simple, the trust uses a third party Operator to manage the contract on their behalf. They select Tokenized to be that third party, and use the publicly available details to determine the correct pricing for their contract. Tokenized are are added into the operator definition field. Because they are using Tokenized, they are able to use the Issuer management functions of the Nexus platform to build their smart contract.

An issuer proposal is added to the contract which stipulates that the only people authorised to hold assets under the contract are the three beneficiaries.

Once the Contract Offer is assembled in full it is double checked by Daniel to ensure it will pass the contract validation process used by the Tokenized platform. Daniel then sends the Contract Offer to the Tokenized platform using the Nexus app. As the operator of the smart contract, Tokenized must sign it or the platform will reject the offer transaction. Tokenized signs the transaction and the Contract Offer is sent with the necessary fees attached to the smart contract address.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-contract-offer.svg?sanitize=true" alt="The BobAngelaChris Trust Contract Offer" align="middle">

The Contract Offer is sent to an address which is provided to the issuer by Tokenized. It corresponds to an address controlled by their Tokenized platform which is exclusively for the control of TBACT.

The platform receives the Contract Offer and and unpacks the transaction. Once the conditions that are specified for the establishment of the contract are proven to be valid, the platform sends a Contract Formation action from the contract address. From this moment, the smart contract can be considered live and is ready to create, distribute and manage assets.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-contract-formation.svg?sanitize=true" alt="The BobAngelaChris Trust Contract Formation" align="middle">

The only asset being created under this contract are shares in the trust itself. The trust owns the home and manages it on behalf of the trust beneficiaries. Daniel creates an Asset Definition to send to the contract using asset type SHC (Common Shares).
The definition breaks the ownership of the trust down into 300 fungible tokens, to allow the equity to be distributed amongst the trustees.
Once the Asset Definition is complete, Daniel sends it to the Trust's smart contract:

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-asset-definition.svg?sanitize=true" alt="The BobAngelaChris Trust Share Definition" align="middle">

The contract responds with an Asset Creation action, allocating the 300 shares to the Issuer's wallet.

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-asset-creation.svg?sanitize=true" alt="The BobAngelaChris Trust Share Creation" align="middle">

Now that the home has been tokenized, the trust is able to distribute it to the trustees. This is done in a single Transfer action, which sends 100/300 of the tokens to each of the trustees:

<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-share-transfer.svg?sanitize=true" alt="The BobAngelaChris Trust Share Transfer" align="middle">

After receiving and evaluating the transfer, the Smart Contract responds with a settlement transaction.


<img src="https://raw.githubusercontent.com/tokenized/docs/master/images/tbact-asset-settlement.svg?sanitize=true" alt="The BobAngelaChris Trust Share settlement" align="middle">


Now that the ownership of the trust has been established, the Tokenized platform can be used to create dividends for each of the asset owners when rental income is distributed. The trustees decide to rent the home and their accountant provides quarterly funds for distribution. 
