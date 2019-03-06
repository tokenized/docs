
#Contract Formation Action

This txn is created by the Contract (smart contract/off-chain agent/token contract) upon receipt of a valid Contract Offer Action from the issuer.  The Smart Contract will execute on a server controlled by the Issuer. or a Smart Contract Operator on their behalf .

The following breaks down the construction of a Contract Formation Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:6%" class="s0">Field</th>
               <th style="width:9%" class="s1">Label</th>
            <th style="width:9%" class="s1">Name</th>
            <th style="width:2%" class="s1">Bytes</th>
            <th style="width:29%" class="s1">Example Values</th>
            <th style="width:26%" class="s1">Comments</th>
            <th style="width:5%" class="s1">Data Type</th>
            <th style="width:14%" class="s2">Amendment Restrictions</th>
        </tr>
        <tr>
            <td class="s5" rowspan="38">Metadata (OP_RETURN Payload)</td>
            <td class="c6">Header[]</td>
            <td class="c6">Header Array</td>
            <td class="c6">-</td>
            <td class="c6">-</td>
            <td class="c6">Common header data for all messages</td>
            <td class="c6">Header</td>
            <td class="c7"></td>
        </tr>
        <tr>
            <td class="c10">Text Encoding</td>
            <td class="c10">TextEncoding</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="c10">uint8</td>
            <td class="c11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr>
            <td class="c10">Contract Name</td>
            <td class="c10">ContractName</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tesla - Shareholder Agreement</td>
            <td class="c10">Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public key hash address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown file</td>
            <td class="c10">uint8</td>
            <td class="c11">Contract File - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Length of Contract File</td>
            <td class="c10">LenContractFile</td>
            <td class="c10">4</td>
            <td class="c10" style="word-break:break-all">32</td>
            <td class="c10">Max size is the max transaction size - other data in the txn.  </td>
            <td class="c10">uint32</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract File</td>
            <td class="c10">ContractFile</td>
            <td class="c10">32</td>
            <td class="c10" style="word-break:break-all">c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1</td>
            <td class="c10">SHA-256 hash of the Contract file specific to the smart contract and relevant Assets.  Legal and technical information. (eg. pdf)</td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">USA</td>
            <td class="c10">5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.</td>
            <td class="c10">string</td>
            <td class="c11">Governing Law - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">US-CA</td>
            <td class="c10">Legal proceedings/arbitration will take place using the specified Governing Law in this location.</td>
            <td class="c10">string</td>
            <td class="c11">Jurisdiction - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Contract Expiration</td>
            <td class="c10">ContractExpiration</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">Wed May 09 2018 00:00:00 GMT+1000 (AEST)</td>
            <td class="c10">All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.</td>
            <td class="c10">time</td>
            <td class="c11">Contract Expiration - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Contract URI</td>
            <td class="c10">ContractURI</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj</td>
            <td class="c10">Length 0-255 bytes.  0 is valid. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Issuer Name</td>
            <td class="c10">IssuerName</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tesla Inc.</td>
            <td class="c10">Length 0-255 bytes. 0 is not valid. Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. </td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Issuer Type</td>
            <td class="c10">IssuerType</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">P</td>
            <td class="c10">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).</td>
            <td class="c10">string</td>
            <td class="c11">Issuer Type - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Issuer Logo URL</td>
            <td class="c10">IssuerLogoURL</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">https://example.com/images/logo.png</td>
            <td class="c10">The URL of the Issuers logo.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract Operator ID</td>
            <td class="c10">ContractOperatorID</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tokenized</td>
            <td class="c10">Length 0-255 bytes. 0 is valid. Smart Contract Operator identifier. Can be any unique identifying string, including human readable names for branding/vanity purposes. Can also be null or the Issuer.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract Authorization Flags</td>
            <td class="c10">ContractAuthFlags</td>
            <td class="c10">16</td>
            <td class="c10" style="word-break:break-all">010010010010010010010010010010010110110110110110110110110110110100100100100110110110110110110110110110110110110110110110110000000</td>
            <td class="c10">Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other terms and conditions that are out of the smart contract's control are listed in the actual Contract File.</td>
            <td class="c10">bin</td>
            <td class="c11">Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.</td>
        </tr>
        <tr>
            <td class="c10">Number of Voting Systems</td>
            <td class="c10">VotingSystemCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">0-10 voting systems. If 0, Voting System and associated subfields (InitiativeThreshold, InitiativeThresholdCurrency) will be null. 10 will be upper limit and restricted by the smart contract.</td>
            <td class="c10">uint8</td>
            <td class="c11">Voting - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Voting Systems</td>
            <td class="c10">VotingSystems</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10">A list voting systems.</td>
            <td class="c10">VotingSystem[]</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Restricted Qty of Assets</td>
            <td class="c10">RestrictedQtyAssets</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI</td>
            <td class="c10">uint64</td>
            <td class="c11">Qty of Assets - Amendments can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Referendum Proposal</td>
            <td class="c10">ReferendumProposal</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">A Referendum is permitted for Contract-Wide Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c11">General Governance</td>
        </tr>
        <tr>
            <td class="c10">Initiative Proposal</td>
            <td class="c10">InitiativeProposal</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">An initiative is permitted for Contract-Wide Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Registry Count</td>
            <td class="c10">RegistryCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of registries (eg. KYC registry/database/whitelist/identity database/etc - managed by a Registrar (oracle)) the smart contract is permitted to interact with. 0-255. 0 is valid (no registry subfields).</td>
            <td class="c10">uint8</td>
            <td class="c11">Registry - Can be restricted to a vote.</td>
        </tr>
        <tr>
            <td class="c10">Registries</td>
            <td class="c10">Registries</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10">A list Registries</td>
            <td class="c10">Registry[]</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Issuer Address</td>
            <td class="c10">IssuerAddress</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">Physical/mailing address. Y/N, N means there is no issuer address.</td>
            <td class="c10">bool</td>
            <td class="c11">Issuer Details - Can always be amended by issuer/smart contract operator.</td>
        </tr>
        <tr>
            <td class="c10">Unit Number</td>
            <td class="c10">UnitNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">2</td>
            <td class="c10">Issuer Address Details (eg. HQ)</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Building Number</td>
            <td class="c10">BuildingNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">13577</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Street</td>
            <td class="c10">Street</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Fairmont Ave</td>
            <td class="c10"></td>
            <td class="c10">nvarchar16</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Suburb/City</td>
            <td class="c10">SuburbCity</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Robinoh</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Territory/State/Province Code</td>
            <td class="c10">TerritoryStateProvinceCode</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">BC</td>
            <td class="c10"></td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Country Code</td>
            <td class="c10">CountryCode</td>
            <td class="c10">3</td>
            <td class="c10" style="word-break:break-all">USA</td>
            <td class="c10"></td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Postal/ZIP Code</td>
            <td class="c10">PostalZIPCode</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">50210</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Email Address</td>
            <td class="c10">EmailAddress</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">james@tokenized.com</td>
            <td class="c10">Address for text-based communication: eg. email address, Bitcoin address</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Phone Number</td>
            <td class="c10">PhoneNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">0448484848</td>
            <td class="c10">Phone Number for Entity. Max acceptable size: 50.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">KeyRoles Count</td>
            <td class="c10">KeyRolesCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of key roles associated with the issuing entity.  (eg. Directors, etc.) 0-255. 0 is valid.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Key Roles</td>
            <td class="c10">KeyRoles</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10">A list of Key Roles.</td>
            <td class="c10">KeyRole[]</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Notable Roles Count</td>
            <td class="c10">NotableRolesCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of notable roles associated with the issuing entity.  (eg. Corporate Officers, Managers, etc.) 0-255. 0 is valid.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Notable Roles</td>
            <td class="c10">NotableRoles</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10">A list of Notable Roles.</td>
            <td class="c10">NotableRole[]</td>
            <td class="c11"></td>
        </tr>
        <tr>
            <td class="c10">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Counter. Cannot be manually changed by issuer.  Can only be incremented by 1 by SC when CF action is published.</td>
            <td class="c10">uint64</td>
            <td class="c11">Can't be changed by issuer or smart contract operator.</td>
        </tr>
        <tr>
            <td class="c10">Timestamp</td>
            <td class="c10">Timestamp</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">1551767413250187179</td>
            <td class="c10">Timestamp in nanoseconds of when the smart contract created the action.</td>
            <td class="c10">timestamp</td>
            <td class="c11">Cannot be changed by issuer, operator. Smart contract controls.</td>
        </tr>
    </table>
</div>