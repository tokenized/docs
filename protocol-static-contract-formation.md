

#Static Contract Formation Action

Static Contract Formation Action - 

The following breaks down the construction of a Static Contract Formation Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr"> 
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style="height:19px">
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
            <td class="s5" rowspan="15">Metadata (OP_RETURN Payload)</td>
            <td class="c7" colspan="7"><a href="javascript" data-popover="header">Header - Click to show content</a></td>
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
            <td class="c10">Length 0-255 bytes. Can be any unique identifying string, including human readable names for branding/vanity purposes.   [Contract identifier (instance) is the bitcoin public key hash address. If the Public Address is lost, then the issuer will have to reissue the entire contract, Asset definition and tokens with the new public address.]. Smart contracts can be branded and specialized to suit any terms and conditions.</td>
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
        <tr>                <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>

<div class="ui modal" id="header">
    <i class="close icon"></i>
    <div class="content docs-content">
        <table class="ui table">
        	<tr style='height:19px;'>
	            <th style="width:9%" class="s0">Label</th>
	            <th style="width:9%" class="s1">Name</th>
	            <th style="width:2%" class="s1">Bytes</th>
	            <th style="width:29%" class="s1">Example Values</th>
	            <th style="width:26%" class="s1">Comments</th>
	            <th style="width:5%" class="s1">Data Type</th>
	        </tr>
            <tr>
                <td class="c5">ProtocolID</td>
                <td class="c6">Protocol Identifier</td>
                <td class="c6">13</td>
                <td class="c6">tokenized.com</td>
                <td class="c6">Tokenized Protocol Identifier</td>
                <td class="c6">string</td>
            </tr>
            <tr>
                <td class="c5">OpPushdata</td>
                <td class="c6">Pushdata Instruction</td>
                <td class="c6">1</td>
                <td class="c6">Varies</td>
                <td class="c6">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload. May be followed by a secondary 1, 2 or 4 byte data element depending on the size of the tokenized data packet</td>
                <td class="c6">opcode</td>
            </tr>
            <tr>
                <td class="c5">LenActionPayload</td>
                <td class="c6">Length of Action Payload</td>
                <td class="c6">0, 1, 2 or 4 bytes</td>
                <td class="c6">0x199</td>
                <td class="c6">Length of the action message (0 - 4,294,967,296‬ bytes), and dependent on the 'OP_PUSHDATA instruction used in the preceding byte. Field is omitted if pushdata is less than 76, 1 byte if OP_PUSHDATA1 is used, 2 bytes if OP_PUSHDATA2 and 4 bytes if OP_PUSHDATA4 is used."</td>
                <td class="c6">pushdata_length</td>
            </tr>
            <tr>
                <td class="c5">Version</td>
                <td class="c6">Version</td>
                <td class="c6">1</td>
                <td class="c6">0</td>
                <td class="c6">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="c6">uint8</td>
            </tr>
            <tr>
                <td class="c5">ActionPrefix</td>
                <td class="c6">Action Prefix</td>
                <td class="c6">2</td>
                <td class="c6">C4</td>
                <td class="c6">The action prefix is what determines the action type.</td>
                <td class="c6">string</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="StaticContractFormation">
    <i class="close icon"></i>
    <table class="ui table">
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
            <td class="c10">Header</td>
            <td class="c10">Header</td>
            <td class="c10">0</td>
            <td class="c10" style="word-break:break-all"></td>
            <td class="c10">Common header data for all messages</td>
            <td class="c10">Header</td>
            <td class="c11">Common header data for all messages.</td>
        </tr>
        <tr>
            <td class="s15" colspan="8"></td>
        </tr>
    </table>
</div>