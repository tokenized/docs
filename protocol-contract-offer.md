


# Contract Offer Action

The Contract Offer action allows the Issuer to tell the smart contract what they want the details (labels, data, T&C's, etc.) of the Contract to be on-chain in a public and immutable way. The Contract Offer action 'initializes' a generic smart contract that has been spun up by either the Smart Contract Operator or the Issuer. This on-chain action allows for the positive response from the smart contract with either a Contract Formation Action or a Rejection Action.

The following breaks down the construction of a Contract Offer Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="c9">Body of Agreement Type</td>
            <td class="c10">BodyOfAgreementType</td>
            <td class="c10">1</td>
            <td class="c10">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Tokenized Body of Agreement Format</td>
            <td class="c10">uint</td>
            <td class="c10">Body of Agreement - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c9">Body of Agreement</td>
            <td class="c10">BodyOfAgreement</td>
            <td class="c10">32</td>
            <td class="c10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="c10"><abbr title="SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the full terms and conditions of an agreement in the Tokenized Body of Agreement format.  This is specific to the smart contract and relevant Assets.  Legal and technical information.">SHA-256 hash of the body of the agreement (full contract in pdf format or the like) or the ...</abbr></td>
            <td class="c10">varbin</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Type</td>
            <td class="c10">ContractType</td>
            <td class="c10">8</td>
            <td class="c10">Shareholder Agreement</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
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
            <td class="c10">varbin</td>
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
            <td class="c10"><abbr title="Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on-chain information or even a public address (DNS).">Points to an information page that also has a copy of the Contract.  Anyone can go to the  ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Entity">
                   Issuer - Click to show content
                </a>
            </td>
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
            <td class="c9">Contract Operator Included</td>
            <td class="c10">ContractOperatorIncluded</td>
            <td class="c10">0</td>
            <td class="c10"></td>
            <td class="c10"><abbr title="If true, then the second input is a contract operator. If false, then all additional inputs are just funding and "includes" fields are skipped in serialization.">If true, then the second input is a contract operator. If false, then all additional input ...</abbr></td>
            <td class="c10">bool</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Entity">
                   Contract Operator - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Contract Authorization Flags</td>
            <td class="c10">ContractAuthFlags</td>
            <td class="c10">16</td>
            <td class="c10"><abbr title="010010010010010010010010010010010110110110110110110110110110110100100100100110110110110110110110110110110110110110110110110000000">Hover for example</abbr></td>
            <td class="c10"><abbr title="Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other terms and conditions that are out of the smart contract's control are listed in the actual Contract File.">Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other t ...</abbr></td>
            <td class="c10">varbin</td>
            <td class="c10">Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.</td>
        </tr>
        <tr>
            <td class="c9">Contract Fee</td>
            <td class="c10">ContractFee</td>
            <td class="c10">8</td>
            <td class="c10"></td>
            <td class="c10">Satoshis required to be paid to the contract for each asset action.</td>
            <td class="c10">uint</td>
            <td class="c10"></td>
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
            <td class="c9">Issuer Proposal</td>
            <td class="c10">IssuerProposal</td>
            <td class="c10">0</td>
            <td class="c10">true</td>
            <td class="c10">An Issuer is permitted to make proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c10">General Governance</td>
        </tr>
        <tr>
            <td class="c9">Holder Proposal</td>
            <td class="c10">HolderProposal</td>
            <td class="c10">0</td>
            <td class="c10">true</td>
            <td class="c10">A holder is permitted to make proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Register">
                   Registers - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Contract Offer Action Transaction Summary

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
            <td class="c6">Issuer's Public Address</td>
            <td class="c6">The smart contract sets the issuer public address with whatever public address is in Index 0 of the first valid Contract Offer.  From then on, the SC will only respond to 'commands' (request actions) from this address with respect to actions that are issuer controlled according to the protocol.</td>
            <td class="c10">0</td>
            <td class="c10">Contract Public Address</td>
            <td class="c10"></td>
        </tr>

       <tr>
            <td class="c5">1</td>
            <td class="c6">Contract Operator's Public Address (Optional)</td>
            <td class="c6">The one exception to the rule above.  The Contract Operator can nominate a secondary controlling public address that can act on behalf of the issuer for issuer related requests. Typically this will be the Smart Contract Operator. (Optional)</td>
            <td class="c10"></td>
            <td class="c10"></td>
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
            <tr>
                <td class="c10">Protocol Identifier</td>
                <td class="c10">ProtocolID</td>
                <td class="c10">13</td>
                <td class="c10">tokenized.com</td>
                <td class="c10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="c10">byte</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Push Data</td>
                <td class="c10">OpPushdata</td>
                <td class="c10">1</td>
                <td class="c10">0x4d</td>
                <td class="c10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="c10">byte</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Length of Action Payload</td>
                <td class="c10">LenActionPayload</td>
                <td class="c10"></td>
                <td class="c10">tokenized.com</td>
                <td class="c10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="c10">byte</td>
                <td class="c10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="c10">Version</td>
                <td class="c10">Version</td>
                <td class="c10">1</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="c10">uint8</td>
                <td class="c10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="c10">Action Prefix</td>
                <td class="c10">ActionPrefix</td>
                <td class="c10">2</td>
                <td class="c10">C1</td>
                <td class="c10" style="word-break:break-all">// C1 identifies data as a ContractOffer message.</td>
                <td class="c10">string</td>
                <td class="c10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
<div class="ui modal" id="type-Entity">
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
                <td class="c10">Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Tesla Inc.</td>
                <td class="c10">Length 1-255 bytes (0 is not valid). Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. </td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">P</td>
                <td class="c10">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Legal Entity Identifier</td>
                <td class="c10">LEI</td>
                <td class="c10">20</td>
                <td class="c10" style="word-break:break-all">54930084UKLVMY22DS16</td>
                <td class="c10">Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up of a 20-character identifier that identifies distinct legal entities that engage in financial transactions. It is defined by ISO 17442.[1] Natural persons are not required to have an LEI; they’re eligible to have one issued, however, but only if they act in an independent business capacity.[2] The LEI is a global standard, designed to be non-proprietary data that is freely accessible to all.[3] As of December 2018, over 1,300,000 legal entities from more than 200 countries have now been issued with LEIs.</td>
                <td class="c10">fixedchar</td>
                <td class="c10">ISO 17442 - https://en.wikipedia.org/wiki/Legal_Entity_Identifier</td>
            </tr>
            <tr>
                <td class="c10">Address Included</td>
                <td class="c10">AddressIncluded</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all">1</td>
                <td class="c10">Registered/Physical/mailing address(HQ). Y-1/N-0, N means there is no issuer address.</td>
                <td class="c10">bool</td>
                <td class="c10">Entity/Contracting Party X Details</td>
            </tr>
            <tr>
                <td class="c10">Unit Number</td>
                <td class="c10">UnitNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">2</td>
                <td class="c10">Issuer/Entity/Contracting Party X Address Details (eg. HQ)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Building Number</td>
                <td class="c10">BuildingNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">13577</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Street</td>
                <td class="c10">Street</td>
                <td class="c10">16</td>
                <td class="c10" style="word-break:break-all">Fairmont Ave</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Suburb/City</td>
                <td class="c10">SuburbCity</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Robinoh</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Territory/State/Province Code</td>
                <td class="c10">TerritoryStateProvinceCode</td>
                <td class="c10">5</td>
                <td class="c10" style="word-break:break-all">BC</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Country Code</td>
                <td class="c10">CountryCode</td>
                <td class="c10">3</td>
                <td class="c10" style="word-break:break-all">USA</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Postal/ZIP Code</td>
                <td class="c10">PostalZIPCode</td>
                <td class="c10">12</td>
                <td class="c10" style="word-break:break-all">50210</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Email Address</td>
                <td class="c10">EmailAddress</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">satoshi@tokenized.com</td>
                <td class="c10">Length 0-255 bytes. Address for text-based communication: eg. email address, Bitcoin address</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Phone Number</td>
                <td class="c10">PhoneNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">0448484848</td>
                <td class="c10">Length 0-50 bytes. 0 is valid. Phone Number for Entity.</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Administration</td>
                <td class="c10">Administration</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of people that are in Administrative Roles for the Entity.  eg. Chair, Director, Managing Partner, etc.</td>
                <td class="c10">Administrator[]</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Management</td>
                <td class="c10">Management</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of people in Management Roles for the Entity. e.g CEO, COO, CTO, CFO, Secretary, Executive, etc.</td>
                <td class="c10">Manager[]</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Entity">
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
                <td class="c10">Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Tesla Inc.</td>
                <td class="c10">Length 1-255 bytes (0 is not valid). Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. </td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">P</td>
                <td class="c10">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Legal Entity Identifier</td>
                <td class="c10">LEI</td>
                <td class="c10">20</td>
                <td class="c10" style="word-break:break-all">54930084UKLVMY22DS16</td>
                <td class="c10">Null is valid. A Legal Entity Identifier (or LEI) is an international identifier made up of a 20-character identifier that identifies distinct legal entities that engage in financial transactions. It is defined by ISO 17442.[1] Natural persons are not required to have an LEI; they’re eligible to have one issued, however, but only if they act in an independent business capacity.[2] The LEI is a global standard, designed to be non-proprietary data that is freely accessible to all.[3] As of December 2018, over 1,300,000 legal entities from more than 200 countries have now been issued with LEIs.</td>
                <td class="c10">fixedchar</td>
                <td class="c10">ISO 17442 - https://en.wikipedia.org/wiki/Legal_Entity_Identifier</td>
            </tr>
            <tr>
                <td class="c10">Address Included</td>
                <td class="c10">AddressIncluded</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all">1</td>
                <td class="c10">Registered/Physical/mailing address(HQ). Y-1/N-0, N means there is no issuer address.</td>
                <td class="c10">bool</td>
                <td class="c10">Entity/Contracting Party X Details</td>
            </tr>
            <tr>
                <td class="c10">Unit Number</td>
                <td class="c10">UnitNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">2</td>
                <td class="c10">Issuer/Entity/Contracting Party X Address Details (eg. HQ)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Building Number</td>
                <td class="c10">BuildingNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">13577</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Street</td>
                <td class="c10">Street</td>
                <td class="c10">16</td>
                <td class="c10" style="word-break:break-all">Fairmont Ave</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Suburb/City</td>
                <td class="c10">SuburbCity</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Robinoh</td>
                <td class="c10"></td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Territory/State/Province Code</td>
                <td class="c10">TerritoryStateProvinceCode</td>
                <td class="c10">5</td>
                <td class="c10" style="word-break:break-all">BC</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Country Code</td>
                <td class="c10">CountryCode</td>
                <td class="c10">3</td>
                <td class="c10" style="word-break:break-all">USA</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Postal/ZIP Code</td>
                <td class="c10">PostalZIPCode</td>
                <td class="c10">12</td>
                <td class="c10" style="word-break:break-all">50210</td>
                <td class="c10"></td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Email Address</td>
                <td class="c10">EmailAddress</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">satoshi@tokenized.com</td>
                <td class="c10">Length 0-255 bytes. Address for text-based communication: eg. email address, Bitcoin address</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Phone Number</td>
                <td class="c10">PhoneNumber</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">0448484848</td>
                <td class="c10">Length 0-50 bytes. 0 is valid. Phone Number for Entity.</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Administration</td>
                <td class="c10">Administration</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of people that are in Administrative Roles for the Entity.  eg. Chair, Director, Managing Partner, etc.</td>
                <td class="c10">Administrator[]</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Management</td>
                <td class="c10">Management</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of people in Management Roles for the Entity. e.g CEO, COO, CTO, CFO, Secretary, Executive, etc.</td>
                <td class="c10">Manager[]</td>
                <td class="c10"></td>
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
                <td class="c10">Vote Type</td>
                <td class="c10">VoteType</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">A</td>
                <td class="c10">R - Relative Threshold, A - Absolute Threshold, P - Plurality,  (Relative Threshold means the number of counted votes must exceed the threshold % of total ballots cast.  Abstentations/spoiled votes do not detract from the liklihood of a vote passing as they are not included in the denominator.  Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens.  Abstentations/spoiled votes detract from the liklihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50% and 51% of the total outstanding tokens did not vote, then the vote cannot pass.  50% of all tokens would have had to vote for one vote option for the vote to be successful.</td>
                <td class="c10">fixedchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Tally Logic</td>
                <td class="c10">TallyLogic</td>
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
                <td class="c10" style="word-break:break-all">75</td>
                <td class="c10">This field is ignored when VoteType is P (Plurality). Otherwise it is the percentage of ballots required for a proposal to pass. Valid values are greater than 0 and less than 100. 75 means 75% and greater.  Only applicable to Relative and Absolute Threshold vote methods.  The Plurality vote method requires no threshold value (NULL), as the successful vote option is simply selected on the basis of highest ballots cast for it.</td>
                <td class="c10">uint</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">Where an asset has a vote multiplier, true must be set here for the vote multiplier to count, otherwise votes are simply treated as 1x per token.</td>
                <td class="c10">bool</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Holder Proposal Fee for the Voting System</td>
                <td class="c10">HolderProposalFee</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">100</td>
                <td class="c10">Token Owners must pay the fee amount to broadcast a valid Proposal.  If the Proposal action is valid, the smart contract will start a vote. 0 is valid.</td>
                <td class="c10">uint</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Register">
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
                <td class="c10">Register Name</td>
                <td class="c10">Name</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Tokenized</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Register X Name (eg. Coinbase, Tokenized, etc.)</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Register URL</td>
                <td class="c10">URL</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">http://register.tokenized.com/api/3650d9/version2010</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. If applicable: URL for REST/RPC Endpoint</td>
                <td class="c10">varchar</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Register Public Key</td>
                <td class="c10">PublicKey</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">Length 0-255 bytes. 0 is not valid. Register Public Key (eg. Bitcoin Public key), used to confirm digital signed proofs for transfers.  Can also be the same public address that controls a Tokenized Register.</td>
                <td class="c10">varbin</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

