
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
            <td class="c10">30</td>
            <td class="c10">Tesla - Shareholder Agreement</td>
            <td class="c10"><abbr title="Length 0-255 bytes. Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.">Length 0-255 bytes. Can be any unique identifying string, including hu ... Hover for more</abbr></td>
            <td class="c10">nvarchar8</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Type</td>
            <td class="c10">ContractType</td>
            <td class="c10">30</td>
            <td class="c10">Non-Disclosure Agreement</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown file</td>
            <td class="c10">uint8</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Length of Contract File</td>
            <td class="c10">LenContractFile</td>
            <td class="c10">4</td>
            <td class="c10">32</td>
            <td class="c10">Max size is the max transaction size - other data in the txn.  </td>
            <td class="c10">uint32</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract File</td>
            <td class="c10">ContractFile</td>
            <td class="c10">32</td>
            <td class="c10"><abbr title="c236f77c7abd7249489e7d2bb6c7e46ba3f4095956e78a584af753ece56cf6d1">Hover for example</abbr></td>
            <td class="c10"><abbr title="SHA-256 hash of the Contract file specific to the smart contract and relevant Assets.  Legal and technical information. (eg. pdf)">SHA-256 hash of the Contract file specific to the smart contract and r ... Hover for more</abbr></td>
            <td class="c10">string</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">2</td>
            <td class="c10">0</td>
            <td class="c10">Counter 0 - 65,535</td>
            <td class="c10">uint16</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10">USA</td>
            <td class="c10"><abbr title="5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.">5 Letter Code to Identify which governing law the contract will adhere ... Hover for more</abbr></td>
            <td class="c10">string</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10">US-CA</td>
            <td class="c10"><abbr title="Legal proceedings/arbitration will take place using the specified Governing Law in this location.">Legal proceedings/arbitration will take place using the specified Gove ... Hover for more</abbr></td>
            <td class="c10">string</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Effective Date</td>
            <td class="c10">EffectiveDate</td>
            <td class="c10">8</td>
            <td class="c10"><abbr title="Wed May 09 2018 00:00:00 GMT+1000 (AEST)">Hover for example</abbr></td>
            <td class="c10">Start date of the contract.</td>
            <td class="c10">time</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract Expiration</td>
            <td class="c10">ContractExpiration</td>
            <td class="c10">8</td>
            <td class="c10"><abbr title="Wed May 09 2018 00:00:00 GMT+1000 (AEST)">Hover for example</abbr></td>
            <td class="c10"><abbr title="All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.">All actions related to the contract will cease to work after this time ... Hover for more</abbr></td>
            <td class="c10">time</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Contract URI</td>
            <td class="c10">ContractURI</td>
            <td class="c10">53</td>
            <td class="c10"><abbr title="https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj">Hover for example</abbr></td>
            <td class="c10"><abbr title="Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).">Length 0-255 bytes. Points to an information page that also has a copy ... Hover for more</abbr></td>
            <td class="c10">nvarchar8</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">PrevRevTxID</td>
            <td class="c10">PrevRevTxID</td>
            <td class="c10">32</td>
            <td class="c10"><abbr title="3c762af9de09dc7403132f4a21bdf8aa02f41db9de7f9dab60409ab8cc907a3f">Hover for example</abbr></td>
            <td class="c10">The Tx-ID of the previous contract revision.</td>
            <td class="c10">string</td>
            <td class="c10"></td>
        </tr>
        <tr>
            <td class="c9">Entity Count</td>
            <td class="c10">EntityCount</td>
            <td class="c10">1</td>
            <td class="c10">0</td>
            <td class="c10">Number of entities involved in the contract as contracting parties.</td>
            <td class="c10">uint8</td>
            <td class="c10"></td>
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
            <td class="c5">[{PartyX Issuer or Party X Public Address }]</td>
            <td class="c6">.</td>
            <td class="c6">.</td>
            <td class="c10">.</td>
            <td class="c10">.</td>
            <td class="c10">.</td>
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
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Push Data</td>
                <td class="c10">OpPushdata</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">77</td>
                <td class="c10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="c10">opcode</td>
                <td class="c10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="c10">Length of Action Payload</td>
                <td class="c10">LenActionPayload</td>
                <td class="c10">2</td>
                <td class="c10" style="word-break:break-all">409</td>
                <td class="c10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="c10">pushdata_length</td>
                <td class="c10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="c10">Version</td>
                <td class="c10">Version</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="c10">uint8</td>
                <td class="c10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="c10">Action Prefix</td>
                <td class="c10">ActionPrefix</td>
                <td class="c10">2</td>
                <td class="c10" style="word-break:break-all">C1</td>
                <td class="c10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="c10">string</td>
                <td class="c10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Entity">
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
                <td class="c10">Name</td>
                <td class="c10">Name</td>
                <td class="c10">11</td>
                <td class="c10" style="word-break:break-all">Tesla Inc.</td>
                <td class="c10">Length 1-255 bytes (0 is not valid). Issuing entity (company, organization, individual).  Can be any unique identifying string, including human readable names for branding/vanity purposes. </td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Type</td>
                <td class="c10">Type</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">P</td>
                <td class="c10">P - Public Company Limited by Shares, C - Private Company Limited by Shares, I - Individual, L - Limited Partnership, U -Unlimited Partnership, T - Sole Proprietorship, S - Statutory Company, O - Non-Profit Organization, N - Nation State, G - Government Agency, U - Unit Trust, D - Discretionary Trust.  Found in 'Entities' (Specification/Resources).</td>
                <td class="c10">string</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Entity Address</td>
                <td class="c10">Address</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">1</td>
                <td class="c10">Registered/Physical/mailing address(HQ). Y-1/N-0, N means there is no issuer address.</td>
                <td class="c10">bool</td>
                <td class="c10">Entity/Contracting Party X Details </td>
            </tr>
            <tr>
                <td class="c10">Unit Number</td>
                <td class="c10">UnitNumber</td>
                <td class="c10">2</td>
                <td class="c10" style="word-break:break-all">2</td>
                <td class="c10">Issuer/Entity/Contracting Party X Address Details (eg. HQ)</td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Building Number</td>
                <td class="c10">BuildingNumber</td>
                <td class="c10">6</td>
                <td class="c10" style="word-break:break-all">13577</td>
                <td class="c10"></td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Street</td>
                <td class="c10">Street</td>
                <td class="c10">14</td>
                <td class="c10" style="word-break:break-all">Fairmont Ave</td>
                <td class="c10"></td>
                <td class="c10">nvarchar16</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Suburb/City</td>
                <td class="c10">SuburbCity</td>
                <td class="c10">8</td>
                <td class="c10" style="word-break:break-all">Robinoh</td>
                <td class="c10"></td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Territory/State/Province Code</td>
                <td class="c10">TerritoryStateProvinceCode</td>
                <td class="c10">5</td>
                <td class="c10" style="word-break:break-all">BC</td>
                <td class="c10"></td>
                <td class="c10">string</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Country Code</td>
                <td class="c10">CountryCode</td>
                <td class="c10">3</td>
                <td class="c10" style="word-break:break-all">USA</td>
                <td class="c10"></td>
                <td class="c10">string</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Postal/ZIP Code</td>
                <td class="c10">PostalZIPCode</td>
                <td class="c10">12</td>
                <td class="c10" style="word-break:break-all">50210</td>
                <td class="c10"></td>
                <td class="c10">string</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Email Address</td>
                <td class="c10">EmailAddress</td>
                <td class="c10">20</td>
                <td class="c10" style="word-break:break-all">satoshi@tokenized.com</td>
                <td class="c10">Length 0-255 bytes. Address for text-based communication: eg. email address, Bitcoin address</td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">Phone Number</td>
                <td class="c10">PhoneNumber</td>
                <td class="c10">11</td>
                <td class="c10" style="word-break:break-all">0448484848</td>
                <td class="c10">Length 0-50 bytes. 0 is valid. Phone Number for Entity.</td>
                <td class="c10">nvarchar8</td>
                <td class="c10"></td>
            </tr>
            <tr>
                <td class="c10">KeyRoles Count</td>
                <td class="c10">KeyRolesCount</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">Number of key roles associated with the issuing entity.  (eg. Directors, etc.) 0-255. 0 is valid.</td>
                <td class="c10">uint8</td>
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
                <td class="c10">Notable Roles Count</td>
                <td class="c10">NotableRolesCount</td>
                <td class="c10">1</td>
                <td class="c10" style="word-break:break-all">0</td>
                <td class="c10">Number of notable roles associated with the issuing entity.  (eg. Corporate Officers, Managers, etc.) 0-255. 0 is valid.</td>
                <td class="c10">uint8</td>
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

