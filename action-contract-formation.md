


# Contract Formation Action

This txn is created by the Contract (smart contract/off-chain agent/token contract) upon receipt of a valid Contract Offer Action from the issuer.  The Smart Contract will execute on a server controlled by the Issuer. or a Smart Contract Operator on their behalf.

The following breaks down the construction of a Contract Formation Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:9%" class="s0">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:25%" class="s1">Example Values</th>
            <th style="width:36%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th class="s1">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="c9">Contract Name</td>
            <td class="c10">ContractName</td>
            <td class="c10">8</td>
            <td class="c10">Tesla - Shareholder Agreement</td>
            <td class="c10"><abbr title="Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public key hash address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.">Can be any unique identifying string, including human readable names for branding/vanity p ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown file</td>
            <td class="c10">uint</td>
            <td class="c10">Contract File - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c9">Contract File</td>
            <td class="c10">ContractFile</td>
            <td class="c10">32</td>
            <td class="c10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="c10"><abbr title="SHA-256 hash of the contract file or markdown data for contract file specific to the smart contract and relevant Assets.  Legal and technical information. (eg. pdf)">SHA-256 hash of the contract file or markdown data for contract file specific to the smart ...</abbr></td>
            <td class="c10">varbin</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Supporting Documentation File Type</td>
            <td class="c10">SupportingDocsFileType</td>
            <td class="c10">1</td>
            <td class="c10">1</td>
            <td class="c10">1 - 7z</td>
            <td class="c10">uint</td>
            <td class="c10">The file type of the supporting documents ('attached') that are important to the contract.</td>
        </tr>
        <tr>
            <td class="c9">Supporting Documentation</td>
            <td class="c10">SupportingDocs</td>
            <td class="c10">32</td>
            <td class="c10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10">File of all supporting documents that are important to the contract.</td>
        </tr>
        <tr>
            <td class="c9">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10">USA</td>
            <td class="c10"><abbr title="5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.">5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are t ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10">Governing Law - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c9">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10">US-CA</td>
            <td class="c10"><abbr title="Legal proceedings/arbitration will take place using the specified Governing Law in this location.">Legal proceedings/arbitration will take place using the specified Governing Law in this lo ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10">Jurisdiction - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Contract Expiration - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Contract URI</td>
            <td class="c10">ContractURI</td>
            <td class="c10">8</td>
            <td class="c10"><abbr title="https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj">Hover for example</abbr></td>
            <td class="c10"><abbr title="Length 0-255 bytes.  0 is valid. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).">Length 0-255 bytes.  0 is valid. Points to an information page that also has a copy of the ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Issuer Name</td>
            <td class="c10">IssuerName</td>
            <td class="c10">8</td>
            <td class="c10">Tesla Inc.</td>
            <td class="c10"><abbr title="Length 0-255 bytes. 0 is not valid. Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. ">Length 0-255 bytes. 0 is not valid. Issuing entity (company, organization, individual).  C ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Issuer Type</td>
            <td class="c10">IssuerType</td>
            <td class="c10">1</td>
            <td class="c10">P</td>
            <td class="c10"><abbr title="P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individua ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10">Issuer Type - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c9">Issuer's Legal Entity Identifier</td>
            <td class="c10">IssuerLEI</td>
            <td class="c10">20</td>
            <td class="c10">54930084UKLVMY22DS16</td>
            <td class="c10"><abbr title="Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up of a 20-character identifier that identifies distinct legal entities that engage in financial transactions. It is defined by ISO 17442.[1] Natural persons are not required to have an LEI; they’re eligible to have one issued, however, but only if they act in an independent business capacity.[2] The LEI is a global standard, designed to be non-proprietary data that is freely accessible to all.[3] As of December 2018, over 1,300,000 legal entities from more than 200 countries have now been issued with LEIs.">Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up o ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10">ISO 17442 - https://en.wikipedia.org/wiki/Legal_Entity_Identifier</td>
        </tr>
        <tr>
            <td class="c9">Issuer Logo URL</td>
            <td class="c10">IssuerLogoURL</td>
            <td class="c10">8</td>
            <td class="c10"><abbr title="https://example.com/images/logo.png">Hover for example</abbr></td>
            <td class="c10">The URL of the Issuers logo.</td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Operator ID</td>
            <td class="c10">ContractOperatorID</td>
            <td class="c10">8</td>
            <td class="c10">Tokenized</td>
            <td class="c10"><abbr title="Length 0-255 bytes. 0 is valid. Smart Contract Operator identifier. Can be any unique identifying string, including human readable names for branding/vanity purposes. Can also be null or the Issuer.">Length 0-255 bytes. 0 is valid. Smart Contract Operator identifier. Can be any unique iden ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Operator's Legal Entity Identifier</td>
            <td class="c10">OperatorLEI</td>
            <td class="c10">20</td>
            <td class="c10">54930084UKLVMY22DS16</td>
            <td class="c10"><abbr title="Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up of a 20-character identifier that identifies distinct legal entities that engage in financial transactions. It is defined by ISO 17442.[1] Natural persons are not required to have an LEI; they’re eligible to have one issued, however, but only if they act in an independent business capacity.[2] The LEI is a global standard, designed to be non-proprietary data that is freely accessible to all.[3] As of December 2018, over 1,300,000 legal entities from more than 200 countries have now been issued with LEIs.">Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up o ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10">ISO 17442 - https://en.wikipedia.org/wiki/Legal_Entity_Identifier</td>
        </tr>
        <tr>
            <td class="c9">Contract Authorization Flags</td>
            <td class="c10">ContractAuthFlags</td>
            <td class="c10">16</td>
            <td class="c10"><abbr title="010010010010010010010010010010010110110110110110110110110110110100100100100110110110110110110110110110110110110110110110110000000">Hover for example</abbr></td>
            <td class="c10"><abbr title="Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other terms and conditions that are out of the smart contract's control are listed in the actual Contract File.">Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other t ...</abbr></td>
            <td class="c10">bin</td>
            <td class="c10">Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.</td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-VotingSystem">
                   Voting Systems - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Restricted Qty of Assets</td>
            <td class="c10">RestrictedQtyAssets</td>
            <td class="c10">8</td>
            <td class="c10">1</td>
            <td class="c10"><abbr title="Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI">Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will disp ...</abbr></td>
            <td class="c10">uint</td>
            <td class="c10">Qty of Assets - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c9">Referendum Proposal</td>
            <td class="c10">ReferendumProposal</td>
            <td class="c10">0</td>
            <td class="c10">1</td>
            <td class="c10">A Referendum is permitted for Contract-Wide Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c10">General Governance</td>
        </tr>
        <tr>
            <td class="c9">Initiative Proposal</td>
            <td class="c10">InitiativeProposal</td>
            <td class="c10">0</td>
            <td class="c10">0</td>
            <td class="c10">An initiative is permitted for Contract-Wide Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Registry">
                   Registries - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Issuer Address</td>
            <td class="c10">IssuerAddress</td>
            <td class="c10">0</td>
            <td class="c10">1</td>
            <td class="c10">Physical/mailing address. Y/N, N means there is no issuer address.</td>
            <td class="c10">bool</td>
            <td class="c10">Issuer Details - Can always be amended by issuer/smart contract operator.</td>
        </tr>
        <tr>
            <td class="c9">Unit Number</td>
            <td class="c10">UnitNumber</td>
            <td class="c10">8</td>
            <td class="c10">2</td>
            <td class="c10">Issuer Address Details (eg. HQ)</td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Building Number</td>
            <td class="c10">BuildingNumber</td>
            <td class="c10">8</td>
            <td class="c10">13577</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Street</td>
            <td class="c10">Street</td>
            <td class="c10">16</td>
            <td class="c10">Fairmont Ave</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Suburb/City</td>
            <td class="c10">SuburbCity</td>
            <td class="c10">8</td>
            <td class="c10">Robinoh</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Territory/State/Province Code</td>
            <td class="c10">TerritoryStateProvinceCode</td>
            <td class="c10">5</td>
            <td class="c10">BC</td>
            <td class="c10"></td>
            <td class="c10">fixedchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Country Code</td>
            <td class="c10">CountryCode</td>
            <td class="c10">3</td>
            <td class="c10">USA</td>
            <td class="c10"></td>
            <td class="c10">fixedchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Postal/ZIP Code</td>
            <td class="c10">PostalZIPCode</td>
            <td class="c10">8</td>
            <td class="c10">50210</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Email Address</td>
            <td class="c10">EmailAddress</td>
            <td class="c10">8</td>
            <td class="c10">james@tokenized.com</td>
            <td class="c10">Address for text-based communication: eg. email address, Bitcoin address</td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Phone Number</td>
            <td class="c10">PhoneNumber</td>
            <td class="c10">8</td>
            <td class="c10">0448484848</td>
            <td class="c10">Phone Number for Entity. Max acceptable size: 50.</td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-KeyRole">
                   Key Roles - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-NotableRole">
                   Notable Roles - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">4</td>
            <td class="c10">0</td>
            <td class="c10"><abbr title="Counter. Cannot be manually changed by issuer.  Can only be incremented by 1 by SC when CF action is published.">Counter. Cannot be manually changed by issuer.  Can only be incremented by 1 by SC when CF ...</abbr></td>
            <td class="c10">uint</td>
            <td class="c10">Can't be changed by issuer or smart contract operator.</td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

## Contract Formation Action Transaction Summary

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th class="s0" colspan="6">Smart Contract Operator Fee: 0</th>
       </tr>
         <tr style='height:19px;'>
            <th style="width:10%" class="s0">Index (input)</th>
            <th style="width:20%" class="s1">Txn inputs</th>
            <th style="width:20%" class="s1">Comments</th>
            <th style="width:10%" class="s1">Index (output)</th>
            <th style="width:20%" class="s1">Txn outputs</th>
            <th class="s1">Comments</th>
       </tr>


       <tr>
            <td class="c5">0</td>
            <td class="c6">Contract Public Address</td>
            <td class="c6"></td>
            <td class="c10">0</td>
            <td class="c10">Contract Public Address</td>
            <td class="c10"></td>
        </tr>

    </table>
</div>



<div class="ui modal" id="type-Header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-VotingSystem">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Voting System Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Special Resolutions</td>
                <td class="c10">eg. Special Resolutions, Ordinary Resolutions, Fundamental Matters, General Matters, Directors' Vote, Poll, etc.</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Voting System</td>
                <td class="c10">System</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">1010111101011001001010101010111111011000010100010010100000010000</td>
                <td class="c10">Specifies which subfield is subject to this vote system's control.</td>
                <td class="c10">bin</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Vote Method</td>
                <td class="c10">Method</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">A</td>
                <td class="c10">R - Relative Threshold, A - Absolute Threshold, P - Plurality,  (Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast.  Abstentations/spoiled votes do not detract from the liklihood of a vote passing as they are not included in the denominator.  Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens.  Abstentations/spoiled votes detract from the liklihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the vote cannot pass.  50% of all tokens would have had to vote for one vote option for the vote to be successful.</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Vote Logic</td>
                <td class="c10">Logic</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">0 - Standard Scoring (+1 * # of tokens owned), 1 - Weighted Scoring (1st choice * Vote Max * # of tokens held, 2nd choice * Vote Max-1 * # of tokens held,..etc.) </td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Threshold Percentage for the Voting System</td>
                <td class="c10">ThresholdPercentage</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0.75</td>
                <td class="c10">1-100 is valid for relative threshold and absolute threshold. (eg. 75 means 75% and greater). 0 & >=101 is invalid and will be rejected by the smart contract.  Only applicable to Relative and Absolute Threshold vote methods.  The Plurality vote method requires no threshold value (NULL), as the successful vote option is simply selected on the basis of highest ballots cast for it.</td>
                <td class="c10">uint</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">Y/N</td>
                <td class="c10">Y - Yes, N - No. Where an asset has a vote multiplier, Y must be selected here for the vote multiplier to count, otherwise votes are simply treated as 1x per token.</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Initiative Threshold for the Voting System</td>
                <td class="c10">InitiativeThreshold</td>
                <td class="c10">4</td>
                <td class="c10" style="word-break:break-all">100</td>
                <td class="c10">Token Owners must pay the threshold amount to broadcast a valid Initiative.  If the Initiative action is valid, the smart contract will start a vote. 0 is valid.</td>
                <td class="c10">float</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Initiative Threshold Currency for the Voting System</td>
                <td class="c10">InitiativeThresholdCurrency</td>
                <td class="c10">3</td>
                <td class="c10" style="word-break:break-all">AUD</td>
                <td class="c10">Currency.  Always paid in BSV or a currency token (CUR) at current market valuations in the currency listed. NULL is valid.</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Registry">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Registry Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Tokenized</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Registry X Name (eg. Coinbase, Tokenized, etc.)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Registry URL</td>
                <td class="c10">URL</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">http://registry.tokenized.com/api/3650d9/version2010</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. If applicable: URL for REST/RPC Endpoint</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Registry Public Key</td>
                <td class="c10">PublicKey</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">Length 0-255 bytes. 0 is not valid. Registry Public Key (eg. Bitcoin Public key), used to confirm digital signed proofs for transfers.  Can also be the same public address that controls a Tokenized Registry.</td>
                <td class="c10">PublicKeyHash</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-KeyRole">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Key Role Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">7</td>
                <td class="c10">Chairman, Director. Found in 'Roles' in Specification/Resources</td>
                <td class="c10">uint</td>
                <td class="c10">7 - Chairman</td>
            </tr>
            <tr>
                <td class="c10">Key Role Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Satoshi Nakamoto</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-NotableRole">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:5%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:3%" class="s1">Bytes</th>
                <th style="width:33%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Notable Role Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">5</td>
                <td class="c10">Found in 'Roles' in Specification/Resources</td>
                <td class="c10">uint</td>
                <td class="c10">5 - CEO</td>
            </tr>
            <tr>
                <td class="c10">Notable Role Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Satoshi Nakamoto</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

