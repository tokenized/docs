


# Initiative Action

Initiative Action -  Allows Token Owners to propose an Initiative (aka Initiative/Shareholder vote).  A significant cost - specified in the Contract Formation - can be attached to this action to reduce spam, as the resulting vote will be put to all token owners.

The following breaks down the construction of a Initiative Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="g9">Asset Type</td>
            <td class="g10">AssetType</td>
            <td class="g10">3</td>
            <td class="g10">SHC</td>
            <td class="g10">eg. Share, Bond, Ticket</td>
            <td class="g10">string</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Asset ID</td>
            <td class="g10">AssetID</td>
            <td class="g10">32</td>
            <td class="g10">apm2qsznhks23z8d83u41s8019hyri3i</td>
            <td class="g10"><abbr title="Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID is always linked to a Contract that is identified by the public address of the Contract wallet. The Asset Type can be the leading bytes - a convention - to make it easy to identify that it is a token by humans.">Randomly generated base58 string.  Each Asset ID should be unique.  However, an Asset ID i ...</abbr></td>
            <td class="g10">string</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Vote System</td>
            <td class="g10">VoteSystem</td>
            <td class="g10">1</td>
            <td class="g10">1</td>
            <td class="g10">X for Vote System X. (1-255, 0 is not valid.)</td>
            <td class="g10">uint8</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal</td>
            <td class="g10">Proposal</td>
            <td class="g10">1</td>
            <td class="g10">0</td>
            <td class="g10"><abbr title="1 for a Proposal, 0 for an initiative that is requesting changes to specific subfields for modification. If this field is true, the subfields should be empty.  The smart contract cannot interpret the results of a vote when Proposal = 1.  All meaning is interpreted by the token owners and smart contract simply facilates the record keeping.  When Proposal = 0, the smart contract always assumes the first choice is a 'yes', or 'pass', if the threshold is met, and will process the proposed changes accordingly.">1 for a Proposal, 0 for an initiative that is requesting changes to specific subfields for ...</abbr></td>
            <td class="g10">bool</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9"></td>
            <td class="g10">ProposedChangesCount</td>
            <td class="g10">1</td>
            <td class="g10">0</td>
            <td class="g10"></td>
            <td class="g10">uint8</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-Amendment">
                   Proposed Changes - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="g9">Vote Options</td>
            <td class="g10">VoteOptions</td>
            <td class="g10">0</td>
            <td class="g10">ABCDEFGHIJKLMNO</td>
            <td class="g10"><abbr title="Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical votes will likely be multiple choice or Y/N. Vote instances are identified by the Tx-ID. AB000000000 would be chosen for Y/N (binary) type votes.">Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical ...</abbr></td>
            <td class="g10">nvarchar8</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Vote Max</td>
            <td class="g10">VoteMax</td>
            <td class="g10">1</td>
            <td class="g10">15</td>
            <td class="g10"><abbr title="Range: 1-X. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N (binary)">Range: 1-X. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N  ...</abbr></td>
            <td class="g10">uint8</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal Description</td>
            <td class="g10">ProposalDescription</td>
            <td class="g10">0</td>
            <td class="g10">Change the name of the Contract.</td>
            <td class="g10">Length restricted by the Bitcoin protocol. 0 is valid. Description or details of the vote</td>
            <td class="g10">nvarchar32</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal Document Hash</td>
            <td class="g10">ProposalDocumentHash</td>
            <td class="g10">32</td>
            <td class="g10"><abbr title="77201b0094f50df309f0343e4f44dae64d0de503c91038faf2c6b039f9f18aec">Hover for example</abbr></td>
            <td class="g10">Hash of the proposal document to be distributed to voters.</td>
            <td class="g10">sha256</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Vote Cut-Off Timestamp</td>
            <td class="g10">VoteCutOffTimestamp</td>
            <td class="g10">8</td>
            <td class="g10">10/07/2018 00:00:00</td>
            <td class="g10">Ballot casts after this timestamp will not be included. The vote has finished.</td>
            <td class="g10">time</td>
            <td class="g10"></td>
        </tr>
    </table>
</div>

##Initiative Action Transaction Summary

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
            <td class="g5">[{User Token Owner's Public Address }]</td>
            <td class="g6">.</td>
            <td class="g6">.</td>
            <td class="g10">.</td>
            <td class="g10">.</td>
            <td class="g10">.</td>
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
                <td class="g10">Protocol Identifier</td>
                <td class="g10">ProtocolID</td>
                <td class="g10">13</td>
                <td class="g10" style="word-break:break-all">tokenized.com</td>
                <td class="g10">Tokenized ID Prefix.  tokenized.com</td>
                <td class="g10">string</td>
                <td class="g10"></td>
            </tr>
            <tr>
                <td class="g10">Push Data</td>
                <td class="g10">OpPushdata</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">77</td>
                <td class="g10">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="g10">opcode</td>
                <td class="g10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
            <tr>
                <td class="g10">Length of Action Payload</td>
                <td class="g10">LenActionPayload</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">409</td>
                <td class="g10">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="g10">pushdata_length</td>
                <td class="g10">Depends on Action Payload</td>
            </tr>
            <tr>
                <td class="g10">Version</td>
                <td class="g10">Version</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="g10">uint8</td>
                <td class="g10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="g10">Action Prefix</td>
                <td class="g10">ActionPrefix</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">G1</td>
                <td class="g10">// G1 identifies data as a Initiative message.</td>
                <td class="g10">string</td>
                <td class="g10">Cannot be changed by issuer, operator or smart contract.</td>
            </tr>
        </table>
    </div>
</div>

<div class="ui modal" id="type-Amendment">
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
                <td class="g10">Field Index</td>
                <td class="g10">FieldIndex</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">2</td>
                <td class="g10">Index of the field to be amended.</td>
                <td class="g10">uint8</td>
                <td class="g10">A field with a complex array type uses the same FieldIndex value for all elements. For example, in C1 the VotingSystems field is FieldIndex 16. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="g10">Element</td>
                <td class="g10">Element</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.</td>
                <td class="g10">uint16</td>
                <td class="g10">To specify the 3rd VotingSystem of a Contract, the value 2 would be given. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="g10">Subfield Index</td>
                <td class="g10">SubfieldIndex</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">1</td>
                <td class="g10">Index of the subfield to be amended. This only applies to specific fields of an element in an array. This is used to specify which field of the array element the amendment applies to.</td>
                <td class="g10">uint8</td>
                <td class="g10">For example to specify the 2nd field of a VotingSystem, value 1 would be given.</td>
            </tr>
            <tr>
                <td class="g10">Operation</td>
                <td class="g10">Operation</td>
                <td class="g10">0</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">0 = Modify. 1 = Add an element to the data to the array of elements. 2 = Delete the element listed in the Element field. The Add and Delete operations only apply to a particilar element of a complex array type. For example, it could be used to remove a particular VotingSystem from a Contract.</td>
                <td class="g10">byte</td>
                <td class="g10"></td>
            </tr>
            <tr>
                <td class="g10">Data</td>
                <td class="g10">Data</td>
                <td class="g10">0</td>
                <td class="g10" style="word-break:break-all"></td>
                <td class="g10">New data for the amended subfield. Data type depends on the the type of the field being amended.</td>
                <td class="g10">byte[]</td>
                <td class="g10">The bytes should be in an format appropriate for the field being modified.</td>
            </tr>
        </table>
    </div>
</div>

