

#Contract Offer Action

The Contract Offer action allows the Issuer to tell the smart contract what they want the details (labels, data, T&C's, etc.) of the Contract to be on-chain in a public and immutable way. The Contract Offer action 'initializes' a generic smart contract that has been spun up by either the Smart Contract Operator or the Issuer. This on-chain action allows for the positive response from the smart contract with either a Contract Formation Action or a Rejection Action.

The following breaks down the construction of a Contract Offer Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="36">Metadata (OP_RETURN Payload)</td>
            <td class="c6" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="c10">Text Encoding</td>
            <td class="c10">TextEncoding</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="c10">uint8</td>
            <td class="c11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>

        <tr><td class="c10"></td>
            <td class="c10">ContractName</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tesla - Shareholder Agreement</td>
            <td class="c10">Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public key hash address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown</td>
            <td class="c10">uint8</td>
            <td class="c11">Contract File - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Length of Contract File</td>
            <td class="c10">LenContractFile</td>
            <td class="c10">4</td>
            <td class="c10" style="word-break:break-all">32</td>
            <td class="c10">Max size is the max transaction size - other data in the txn.</td>
            <td class="c10">uint32</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract File</td>
            <td class="c10">ContractFile</td>
            <td class="c10">32</td>
            <td class="c10" style="word-break:break-all">c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1</td>
            <td class="c10">SHA-256 hash of the Contract file specific to the smart contract and relevant Assets.  Legal and technical information. (eg. pdf)</td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">USA</td>
            <td class="c10">5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.</td>
            <td class="c10">string</td>
            <td class="c11">Governing Law - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">US-CA</td>
            <td class="c10">Legal proceedings/arbitration will take place using the specified Governing Law in this location.</td>
            <td class="c10">string</td>
            <td class="c11">Jurisdiction - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Contract Expiration</td>
            <td class="c10">ContractExpiration</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">Wed May 09 2018 00:00:00 GMT+1000 (AEST)</td>
            <td class="c10">All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate total smart contract running costs for the entire life of the contract. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.</td>
            <td class="c10">time</td>
            <td class="c11">Contract Expiration - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Contract URI</td>
            <td class="c10">ContractURI</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj</td>
            <td class="c10">Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on-chain information or even a public address (DNS).</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Issuer Name</td>
            <td class="c10">IssuerName</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tesla Inc.</td>
            <td class="c10">Length 0-255 bytes. 0 is not valid.Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. </td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Issuer Type</td>
            <td class="c10">IssuerType</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">P</td>
            <td class="c10">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).</td>
            <td class="c10">string</td>
            <td class="c11">Issuer Type - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Issuer Logo URL</td>
            <td class="c10">IssuerLogoURL</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">https://example.com/images/logo.png</td>
            <td class="c10">The URL of the Issuers logo.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract Operator ID</td>
            <td class="c10">ContractOperatorID</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Tokenized</td>
            <td class="c10">Length 0-255 bytes. 0 is valid. Smart Contract Operator identifier. Can be any unique identifying string, including human readable names for branding/vanity purposes. Can also be null or the Issuer.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract Authorization Flags</td>
            <td class="c10">ContractAuthFlags</td>
            <td class="c10">16</td>
            <td class="c10" style="word-break:break-all">010010010010010010010010010010010110110110110110110110110110110100100100100110110110110110110110110110110110110110110110110000000</td>
            <td class="c10">Authorization Flags aka Terms and Conditions that the smart contract can enforce.  Other terms and conditions that are out of the smart contract's control are listed in the actual Contract File.</td>
            <td class="c10">bin</td>
            <td class="c11">Contract Flags - Amendments can be restricted to a vote.  Specified in the Voting System.</td>
        </tr>

        <tr><td class="c10">Number of Voting Systems</td>
            <td class="c10">VotingSystemCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">0-10 voting systems. If 0, Voting System and associated subfields (InitiativeThreshold, InitiativeThresholdCurrency) will be null. 10 will be upper limit and restricted by the smart contract.</td>
            <td class="c10">uint8</td>
            <td class="c11">Voting - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c6" colspan="7"><a href="javascript:;" data-popover="type-VotingSystem">Voting Systems - Click to show content</a></td>
        </tr>

        <tr><td class="c10">Restricted Qty of Assets</td>
            <td class="c10">RestrictedQtyAssets</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">Number of Assets (non-fungible) permitted on this contract. 0 if unlimited which will display an infinity symbol in UI</td>
            <td class="c10">uint64</td>
            <td class="c11">Qty of Assets - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c10">Referendum Proposal</td>
            <td class="c10">ReferendumProposal</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">true</td>
            <td class="c10">A Referendum is permitted for Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c11">General Governance</td>
        </tr>

        <tr><td class="c10">Initiative Proposal</td>
            <td class="c10">InitiativeProposal</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">true</td>
            <td class="c10">An initiative is permitted for Proposals (outside of smart contract scope).</td>
            <td class="c10">bool</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Registry Count</td>
            <td class="c10">RegistryCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of registries (eg. KYC registry/database/whitelist/identity database/etc - managed by a Registrar (oracle)) the smart contract is permitted to interact with. 0-255. 0 is valid (no registry subfields).</td>
            <td class="c10">uint8</td>
            <td class="c11">Qty of Assets - Amendments can be restricted to a vote.</td>
        </tr>

        <tr><td class="c6" colspan="7"><a href="javascript:;" data-popover="type-Registry">Registries - Click to show content</a></td>
        </tr>

        <tr><td class="c10">Issuer Address</td>
            <td class="c10">IssuerAddress</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">Physical/mailing address. Y/N, N means there is no issuer address.</td>
            <td class="c10">bool</td>
            <td class="c11">Issuer Details - Can always be amended by issuer/smart contract operator.</td>
        </tr>

        <tr><td class="c10">Unit Number</td>
            <td class="c10">UnitNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">2</td>
            <td class="c10">Issuer Address Details (eg. HQ)</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Building Number</td>
            <td class="c10">BuildingNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">13577</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Street</td>
            <td class="c10">Street</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Fairmont Ave</td>
            <td class="c10"></td>
            <td class="c10">nvarchar16</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Suburb/City</td>
            <td class="c10">SuburbCity</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">Robinoh</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Territory/State/Province Code</td>
            <td class="c10">TerritoryStateProvinceCode</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">BC</td>
            <td class="c10"></td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Country Code</td>
            <td class="c10">CountryCode</td>
            <td class="c10">3</td>
            <td class="c10" style="word-break:break-all">USA</td>
            <td class="c10"></td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Postal/ZIP Code</td>
            <td class="c10">PostalZIPCode</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">50210</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Email Address</td>
            <td class="c10">EmailAddress</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">james@tokenized.com</td>
            <td class="c10">Length 0-255 bytes. 0 is valid (no ContactAddress). Address for text-based communication: eg. email address, Bitcoin address</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Phone Number</td>
            <td class="c10">PhoneNumber</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all">0420199999</td>
            <td class="c10">Length 0-50 bytes. 0 is valid (no Phone subfield).Phone Number for Entity.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">KeyRoles Count</td>
            <td class="c10">KeyRolesCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of key roles associated with the issuing entity.  (eg. Directors, etc.) 0-255. 0 is valid.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c6" colspan="7"><a href="javascript:;" data-popover="type-KeyRole">Key Roles - Click to show content</a></td>
        </tr>

        <tr><td class="c10">Notable Roles Count</td>
            <td class="c10">NotableRolesCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of notable roles associated with the issuing entity.  (eg. Corporate Officers, Managers, etc.) 0-255. 0 is valid.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c6" colspan="7"><a href="javascript:;" data-popover="type-NotableRole">Notable Roles - Click to show content</a></td>
        </tr>

    </table>
</div>


<div class="ui modal" id="type-Header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Protocol Identifier</td>
                <td class="c10">ProtocolID</td>
                <td class="c10">13</td>
                <td class="c10" style="word-break:break-all">tokenized.com</td>
                <td class="c10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="c10">string</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Push Data</td>
                <td class="c10">OpPushdata</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">77</td>
                <td class="c10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="c10">opcode</td>
                <td class="c11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="c10">Length of Action Payload</td>
                <td class="c10">LenActionPayload</td>
                <td class="c10">2</td>
                <td class="c10" style="word-break:break-all">409</td>
                <td class="c10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="c10">pushdata_length</td>
                <td class="c11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="c10">Version</td>
                <td class="c10">Version</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="c10">uint8</td>
                <td class="c11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="c10">Action Prefix</td>
                <td class="c10">ActionPrefix</td>
                <td class="c10">2</td>
                <td class="c10" style="word-break:break-all">C1</td>
                <td class="c10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="c10">string</td>
                <td class="c11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-VotingSystem">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Voting System Name</td>
                <td class="c10">Name</td>
                <td class="c10">20</td>
                <td class="c10" style="word-break:break-all">Special Resolutions</td>
                <td class="c10">eg. Special Resolutions, Ordinary Resolutions, Fundamental Matters, General Matters, Directors' Vote, Poll, etc.</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Voting System</td>
                <td class="c10">System</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">1010111101011001001010101010111111011000010100010010100000010000</td>
                <td class="c10">Specifies which subfield is subject to this vote system's control.</td>
                <td class="c10">bin</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Vote Method</td>
                <td class="c10">Method</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">A</td>
                <td class="c10">R - Relative Threshold, A - Absolute Threshold, P - Plurality,  (Relative Threshold means the number of counted votes must exceed the threshold %!o(MISSING)f total ballots cast.  Abstentations/spoiled votes do not detract from the liklihood of a vote passing as they are not included in the denominator.  Absolute Threshold requires the number of ballots counted to exceed the threshold value when compared to the total outstanding tokens.  Abstentations/spoiled votes detract from the liklihood of the vote passing.  For example, in an absolute threshold vote, if the threshold was 50%!a(MISSING)nd 51%!o(MISSING)f the total outstanding tokens did not vote, then the vote cannot pass.  50%!o(MISSING)f all tokens would have had to vote for one vote option for the vote to be successful.</td>
                <td class="c10">string</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Vote Logic</td>
                <td class="c10">Logic</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">0 - Standard Scoring (+1 * # of tokens owned), 1 - Weighted Scoring (1st choice * Vote Max * # of tokens held, 2nd choice * Vote Max-1 * # of tokens held,..etc.) </td>
                <td class="c10">string</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Threshold Percentage for the Voting System</td>
                <td class="c10">ThresholdPercentage</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0.75</td>
                <td class="c10">1-100 is valid for relative threshold and absolute threshold. (eg. 75 means 75%!a(MISSING)nd greater). 0 & >=101 is invalid and will be rejected by the smart contract.  Only applicable to Relative and Absolute Threshold vote methods.  The Plurality vote method requires no threshold value (NULL), as the successful vote option is simply selected on the basis of highest ballots cast for it.</td>
                <td class="c10">uint8</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">VoteMultiplierPermitted</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">Y/N</td>
                <td class="c10">Y - Yes, N - No. Where an asset has a vote multiplier, Y must be selected here for the vote multiplier to count, otherwise votes are simply treated as 1x per token.</td>
                <td class="c10">string</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Initiative Threshold for the Voting System</td>
                <td class="c10">InitiativeThreshold</td>
                <td class="c10">4</td>
                <td class="c10" style="word-break:break-all">100</td>
                <td class="c10">Token Owners must pay the threshold amount to broadcast a valid Initiative.  If the Initiative action is valid, the smart contract will start a vote. 0 is valid.</td>
                <td class="c10">float32</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Initiative Threshold Currency for the Voting System</td>
                <td class="c10">InitiativeThresholdCurrency</td>
                <td class="c10">3</td>
                <td class="c10" style="word-break:break-all">AUD</td>
                <td class="c10">Currency.  Always paid in BSV or a currency token (CUR) at current market valuations in the currency listed. NULL is valid.</td>
                <td class="c10">string</td>
                <td class="c11"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Registry">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Registry Name</td>
                <td class="c10">Name</td>
                <td class="c10">10</td>
                <td class="c10" style="word-break:break-all">Tokenized</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Registry X Name (eg. Coinbase, Tokenized, etc.)</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Registry URL</td>
                <td class="c10">URL</td>
                <td class="c10">53</td>
                <td class="c10" style="word-break:break-all">http://registry.tokenized.com/api/3650d9/version2010</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. If applicable: URL for REST/RPC Endpoint</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
            <tr>
                <td class="c10">Registry Public Key</td>
                <td class="c10">PublicKey</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all"></td>
                <td class="c10">Length 0-255 bytes. 0 is not valid. Registry Public Key (eg. Bitcoin Public key), used to confirm digital signed proofs for transfers.  Can also be the same public address that controls a Tokenized Registry.</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-KeyRole">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Key Role Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">7</td>
                <td class="c10">Chairman, Director. Found in 'Roles' in Specification/Resources</td>
                <td class="c10">string</td>
                <td class="c11">7 - Chairman</td>
            </tr>
            <tr>
                <td class="c10">Key Role Name</td>
                <td class="c10">Name</td>
                <td class="c10">14</td>
                <td class="c10" style="word-break:break-all">Satoshi Nakamoto</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-NotableRole">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
            <tr style='height:19px;'>
                <th style="width:9%" class="s1">Label</th>
                <th style="width:9%" class="s1">Name</th>
                <th style="width:2%" class="s1">Bytes</th>
                <th style="width:29%" class="s1">Example Values</th>
                <th style="width:26%" class="s1">Comments</th>
                <th style="width:5%" class="s1">Data Type</th>
                <th style="width:14%" class="s2">Amendment Restrictions</th>
            </tr>
            <tr>
                <td class="c10">Notable Role Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">5</td>
                <td class="c10">Found in 'Roles' in Specification/Resources</td>
                <td class="c10">string</td>
                <td class="c11">5 - CEO</td>
            </tr>
            <tr>
                <td class="c10">Notable Role Name</td>
                <td class="c10">Name</td>
                <td class="c10">14</td>
                <td class="c10" style="word-break:break-all">Satoshi Nakamoto</td>
                <td class="c10">Length 0-255 bytes. 0 is valid. Name (eg. John Alexander Smith)</td>
                <td class="c10">nvarchar8</td>
                <td class="c11"></td>
            </tr>
        </table>
    </div>
</div>

