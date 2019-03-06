
#Initiative Action

Initiative Action -  Allows Token Owners to propose a Initiative (aka Initiative/Shareholder vote).  A significant cost - specified in the Contract Formation - is attached to this action to reduce spam, as the resulting vote will be put to all token owners.

The following breaks down the construction of a Initiative Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="s5" rowspan="12">Metadata (OP_RETURN Payload)</td>
            <td class="g6">Header[]</td>
            <td class="g6">Header Array</td>
            <td class="g6">-</td>
            <td class="g6">-</td>
            <td class="g6">Common header data for all messages</td>
            <td class="g6">Header</td>
            <td class="g7"></td>
        </tr>
        <tr>
            <td class="g10">Text Encoding</td>
            <td class="g10">TextEncoding</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">0</td>
            <td class="g10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="g10">uint8</td>
            <td class="g11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>
        <tr>
            <td class="g10">Asset Type</td>
            <td class="g10">AssetType</td>
            <td class="g10">3</td>
            <td class="g10" style="word-break:break-all">SHC</td>
            <td class="g10">eg. Share, Bond, Ticket</td>
            <td class="g10">string</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Asset ID</td>
            <td class="g10">AssetID</td>
            <td class="g10">32</td>
            <td class="g10" style="word-break:break-all">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="g10">Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.</td>
            <td class="g10">string</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Vote System</td>
            <td class="g10">VoteSystem</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">1</td>
            <td class="g10">X for Vote System X. (1-255, 0 is not valid.)</td>
            <td class="g10">uint8</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Proposal Type</td>
            <td class="g10">ProposalType</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all">VotingSystemCount</td>
            <td class="g10">Length 1-255 bytes. P - Proposal, otherwise the name of the subfield that is looking to be amended/modified.</td>
            <td class="g10">nvarchar8</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Vote Options</td>
            <td class="g10">VoteOptions</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all">ABCDEFGHIJKLMNO</td>
            <td class="g10">Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical votes will likely be multiple choice or Y/N. Vote instances are identified by the Tx-ID. AB000000000 would be chosen for Y/N (binary) type votes.</td>
            <td class="g10">nvarchar8</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Vote Max</td>
            <td class="g10">VoteMax</td>
            <td class="g10">1</td>
            <td class="g10" style="word-break:break-all">15</td>
            <td class="g10">Range: 1-X. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N (binary)</td>
            <td class="g10">uint8</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Length of Proposal Description</td>
            <td class="g10">LenProposalDescription</td>
            <td class="g10">2</td>
            <td class="g10" style="word-break:break-all">0</td>
            <td class="g10">Length of Proposal Description Subfield (bytes). 0 to 65,535 bytes. 0 is valid. If 0, Proposal Document Hash is also 0.</td>
            <td class="g10">uint16</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Proposal Description</td>
            <td class="g10">ProposalDescription</td>
            <td class="g10">0</td>
            <td class="g10" style="word-break:break-all">Change the name of the Contract.</td>
            <td class="g10">Length 0 to 65,535 bytes. 0 is valid. If 0, Proposal Document Hash is also 0. Description of the vote</td>
            <td class="g10">nvarchar16</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Proposal Document Hash</td>
            <td class="g10">ProposalDocumentHash</td>
            <td class="g10">32</td>
            <td class="g10" style="word-break:break-all">77201b0094f50df309f0343e4f44dae64d0de503c91038faf2c6b039f9f18aec</td>
            <td class="g10">Hash of the proposal document to be distributed to voters</td>
            <td class="g10">sha256</td>
            <td class="g11"></td>
        </tr>
        <tr>
            <td class="g10">Vote Cut-Off Timestamp</td>
            <td class="g10">VoteCutOffTimestamp</td>
            <td class="g10">8</td>
            <td class="g10" style="word-break:break-all">10/07/2018 00:00:00</td>
            <td class="g10">Ballot casts after this timestamp will not be included. The vote has finished.</td>
            <td class="g10">time</td>
            <td class="g11"></td>
        </tr>
    </table>
</div>