

#Referendum Action

Referendum Action -  Issuer instructs the Contract to Initiate a Token Owner Vote. Usually used for contract amendments, organizational governance, etc.

The following breaks down the construction of a Referendum Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="14">Metadata (OP_RETURN Payload)</td>
            <td class="g6" colspan="7"><a href="javascript:;" data-popover="type-Header">Header - Click to show content</a></td>
        </tr>



        <tr><td class="g10">Text Encoding</td>
            <td class="g10">TextEncoding</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">0</td>
            <td class="g10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="g10">uint8</td>
            <td class="g11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>

        <tr><td class="g10">Asset Specific Vote</td>
            <td class="g10">AssetSpecificVote</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">1</td>
            <td class="g10">1 - Yes, 0 - No.  No Asset Type/AssetID subfields for N - No.</td>
            <td class="g10">bool</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Asset Type</td>
            <td class="g10">AssetType</td>
            <td class="g10">3</td>
            <td class="g10" style="word-break:break-all">RRE</td>
            <td class="g10">eg. Share, Bond, Ticket</td>
            <td class="g10">string</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Asset ID</td>
            <td class="g10">AssetID</td>
            <td class="g10">32</td>
            <td class="g10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="g10">Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.</td>
            <td class="g10">string</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Vote System</td>
            <td class="g10">VoteSystem</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">1</td>
            <td class="g10">X for Vote System X. (1-255, 0 is not valid.)</td>
            <td class="g10">uint8</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Proposal</td>
            <td class="g10">Proposal</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">0</td>
            <td class="g10">1 for a Proposal, 0 for an initiative that is requesting changes to specific subfields for modification. If this field is true, the subfields should be empty.  The smart contract cannot interpret the results of a vote when Proposal = 1.  All meaning is interpreted by the token owners and smart contract simply facilates the record keeping.  When Proposal = 0, the smart contract always assumes the first choice is a 'yes', or 'pass', if the threshold is met, and will process the proposed changes accordingly.</td>
            <td class="g10">bool</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10"></td>
            <td class="g10">ProposedChangesCount</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">0</td>
            <td class="g10"></td>
            <td class="g10">uint8</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Proposed Changes</td>
            <td class="g10">ProposedChanges</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all"></td>
            <td class="g10">Each element contains details of which fields to modify, or delete. Because the number of fields in a Contract and Asset is dynamic due to some fields being able to be repeated, the index value of the field needs to be calculated against the Contract or Asset the changes are to apply to. In the event of a Vote being created from this Initiative, the changes will be applied to the version of the Contract or Asset at that time.</td>
            <td class="g10">Amendment[]</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Vote Options</td>
            <td class="g10">VoteOptions</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all">ABCDEFGHIJKLMNO</td>
            <td class="g10">Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical votes will likely be multiple choice or Y/N. Vote instances are identified by the Tx-ID. AB000000000 would be chosen for Y/N (binary) type votes. Only applicable if Proposal Type is set to P for Proposal.  All other Proposal Types will be binary.  Pass/Fail.</td>
            <td class="g10">nvarchar8</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Vote Max</td>
            <td class="g10">VoteMax</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">15</td>
            <td class="g10">Range: 1-15. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N (binary)</td>
            <td class="g10">uint8</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Proposal Description</td>
            <td class="g10">ProposalDescription</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all">Change the name of the Contract.</td>
            <td class="g10">Length 0 to 65,535 bytes. 0 is valid. Description of the vote.</td>
            <td class="g10">nvarchar16</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Proposal Document Hash</td>
            <td class="g10">ProposalDocumentHash</td>
            <td class="g10">32</td>
            <td class="g10" style="word-break:break-all">77201b0094f50df309f0343e4f44dae64d0de503c91038faf2c6b039f9f18aec</td>
            <td class="g10">Hash of the proposal document to be distributed to voters</td>
            <td class="g10">sha256</td>
            <td class="g11"></td>
        </tr>

        <tr><td class="g10">Vote Cut-Off Timestamp</td>
            <td class="g10">VoteCutOffTimestamp</td>
            <td class="g10">8</td>
            <td class="g10" style="word-break:break-all">10/07/2018 00:00:00</td>
            <td class="g10">Ballot casts after this timestamp will not be included. The vote has finished.</td>
            <td class="g10">time</td>
            <td class="g11"></td>
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
                <td class="g10">Protocol Identifier</td>
                <td class="g10">ProtocolID</td>
                <td class="g10">13</td>
                <td class="g10" style="word-break:break-all">tokenized.com</td>
                <td class="g10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="g10">string</td>
                <td class="g11"></td>
            </tr>
            <tr>
                <td class="g10">Push Data</td>
                <td class="g10">OpPushdata</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">77</td>
                <td class="g10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="g10">opcode</td>
                <td class="g11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="g10">Length of Action Payload</td>
                <td class="g10">LenActionPayload</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">409</td>
                <td class="g10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="g10">pushdata_length</td>
                <td class="g11">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="g10">Version</td>
                <td class="g10">Version</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="g10">uint8</td>
                <td class="g11">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="g10">Action Prefix</td>
                <td class="g10">ActionPrefix</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">C1</td>
                <td class="g10">Contract Offer: The Contract Offer Action allows the Issuer to initialize a smart contract by providing all the necessary information, including T&C's.  The Contract Offer Action can also be used to signal to a market actor that they want to buy/form a contract.</td>
                <td class="g10">string</td>
                <td class="g11">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

