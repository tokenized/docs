

#Static Contract Formation Action

Static Contract Formation Action 

The following breaks down the construction of a Static Contract Formation Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="16">Metadata (OP_RETURN Payload)</td>
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

        <tr><td class="c10">Contract Name</td>
            <td class="c10">ContractName</td>
            <td class="c10">30</td>
            <td class="c10" style="word-break:break-all">Tesla - Shareholder Agreement</td>
            <td class="c10">Length 0-255 bytes. Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract Type</td>
            <td class="c10">ContractType</td>
            <td class="c10">30</td>
            <td class="c10" style="word-break:break-all">Non-Disclosure Agreement</td>
            <td class="c10"></td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract File Type</td>
            <td class="c10">ContractFileType</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">1</td>
            <td class="c10">1 - SHA-256 Hash, 2 - Markdown file</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Length of Contract File</td>
            <td class="c10">LenContractFile</td>
            <td class="c10">4</td>
            <td class="c10" style="word-break:break-all">32</td>
            <td class="c10">Max size is the max transaction size - other data in the txn.  </td>
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

        <tr><td class="c10">Contract Revision</td>
            <td class="c10">ContractRevision</td>
            <td class="c10">2</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Counter 0 - 65,535</td>
            <td class="c10">uint16</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Governing Law</td>
            <td class="c10">GoverningLaw</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">USA</td>
            <td class="c10">5 Letter Code to Identify which governing law the contract will adhere to.  Disputes are to be settled by this law in the jurisdiction specified below. Private dispute resolution organizations can be used as well.  A custom code just needs to be defined.</td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Jurisdiction</td>
            <td class="c10">Jurisdiction</td>
            <td class="c10">5</td>
            <td class="c10" style="word-break:break-all">US-CA</td>
            <td class="c10">Legal proceedings/arbitration will take place using the specified Governing Law in this location.</td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Effective Date</td>
            <td class="c10">EffectiveDate</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">Wed May 09 2018 00:00:00 GMT+1000 (AEST)</td>
            <td class="c10">Start date of the contract.</td>
            <td class="c10">time</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract Expiration</td>
            <td class="c10">ContractExpiration</td>
            <td class="c10">8</td>
            <td class="c10" style="word-break:break-all">Wed May 09 2018 00:00:00 GMT+1000 (AEST)</td>
            <td class="c10">All actions related to the contract will cease to work after this timestamp. The smart contract will stop running.  This will allow many token use cases to be able to calculate smart contract running costs. Eg. an issuer is creating tickets for an event on the 5th of June 2018.  The smart contract will facilitate exchange and send transactions up until the 6th of June.  Wallets can use this to forget tokens that are no longer valid - or at least store them in an 'Expired' folder.</td>
            <td class="c10">time</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Contract URI</td>
            <td class="c10">ContractURI</td>
            <td class="c10">53</td>
            <td class="c10" style="word-break:break-all">https://tokenized.com/Contract/3qeoSCg7JmfSnJesJFojj</td>
            <td class="c10">Length 0-255 bytes. Points to an information page that also has a copy of the Contract.  Anyone can go to the website to have a look at the price/token, information about the Issuer (company), information about the Asset, legal information, etc.  There will also be a way for Token Owners to vote on this page and contact details with the Issuer/tokenized companies. Could be a IPv6/IPv4, an IPFS address (hash) or txn-id for on chain information or even a public address (DNS).</td>
            <td class="c10">nvarchar8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">PrevRevTxID</td>
            <td class="c10">PrevRevTxID</td>
            <td class="c10">32</td>
            <td class="c10" style="word-break:break-all">3c762af9de09dc7403132f4a21bdf8aa02f41db9de7f9dab60409ab8cc907a3f</td>
            <td class="c10">The Tx-ID of the previous contract revision.</td>
            <td class="c10">string</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Entity Count</td>
            <td class="c10">EntityCount</td>
            <td class="c10">1</td>
            <td class="c10" style="word-break:break-all">0</td>
            <td class="c10">Number of entities involved in the contract as contracting parties.</td>
            <td class="c10">uint8</td>
            <td class="c11"></td>
        </tr>

        <tr><td class="c10">Entities</td>
            <td class="c10">Entities</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10"></td>
            <td class="c10">Entity[]</td>
            <td class="c11"></td>
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

