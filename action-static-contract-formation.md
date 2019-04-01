


# Static Contract Formation Action

Static Contract Formation Action

The following breaks down the construction of a Static Contract Formation Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="c10"><abbr title="Length 0-255 bytes. Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.">Length 0-255 bytes. Can be any unique identifying string, including human readable names f ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Type</td>
            <td class="c10">ContractType</td>
            <td class="c10">8</td>
            <td class="c10">Non-Disclosure Agreement</td>
            <td class="c10"></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-ContractCode">
                   Contract Code - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c9">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown file</td>
            <td class="c10">uint</td>
            <td class="c10"></td>
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
            <td class="c9">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">4</td>
            <td class="c10">0</td>
            <td class="c10">Counter 0 to (2^32)-1</td>
            <td class="c10">uint</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10">USA</td>
            <td class="c10"><abbr title="5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.">5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are t ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10">US-CA</td>
            <td class="c10"><abbr title="Legal proceedings/arbitration will take place using the specified Governing Law in this location.">Legal proceedings/arbitration will take place using the specified Governing Law in this lo ...</abbr></td>
            <td class="c10">fixedchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Effective Date - Click to show content
                </a>
            </td>
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
            <td class="c10"><abbr title="Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).">Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  A ...</abbr></td>
            <td class="c10">varchar</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   PrevRevTxID - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="c5" colspan="7">
                <a href="javascript:;" data-popover="type-Entity">
                   Entities - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Static Contract Formation Action Transaction Summary

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
            <td class="c6">Issuer or Party X Public Address</td>
            <td class="c6"></td>
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
                <td class="c10">Entity Address</td>
                <td class="c10">Address</td>
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
                <td class="c10">Key Roles</td>
                <td class="c10">KeyRoles</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of Key Roles.</td>
                <td class="c10">KeyRole[]</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Notable Roles</td>
                <td class="c10">NotableRoles</td>
                <td class="c10">0</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">A list of Notable Roles.</td>
                <td class="c10">NotableRole[]</td>
                <td class="c10"></td>
            </tr>
        </table>
    </div>
</div>

