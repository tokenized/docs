


# Referendum Action

Referendum Action -  Issuer instructs the Contract to Initiate a Token Owner Vote. Usually used for contract amendments, organizational governance, etc.

The following breaks down the construction of a Referendum Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="g9">Asset Specific Vote</td>
            <td class="g10">AssetSpecificVote</td>
            <td class="g10">0</td>
            <td class="g10">1</td>
            <td class="g10">1 - Yes, 0 - No.  No Asset Type/AssetCode subfields for N - No.</td>
            <td class="g10">bool</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Asset Type</td>
            <td class="g10">AssetType</td>
            <td class="g10">3</td>
            <td class="g10">RRE</td>
            <td class="g10">eg. Share, Bond, Ticket</td>
            <td class="g10">fixedchar</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-AssetCode">
                   Asset Code - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="g9">Vote System</td>
            <td class="g10">VoteSystem</td>
            <td class="g10">1</td>
            <td class="g10">1</td>
            <td class="g10">X for Vote System X. (1-255, 0 is not valid.)</td>
            <td class="g10">uint</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal</td>
            <td class="g10">Proposal</td>
            <td class="g10">0</td>
            <td class="g10">0</td>
            <td class="g10"><abbr title="1 for a Proposal, 0 for an initiative that is requesting changes to specific subfields for modification. If this field is true, the subfields should be empty.  The smart contract cannot interpret the results of a vote when Proposal = 1.  All meaning is interpreted by the token owners and smart contract simply facilates the record keeping.  When Proposal = 0, the smart contract always assumes the first choice is a 'yes', or 'pass', if the threshold is met, and will process the proposed changes accordingly.">1 for a Proposal, 0 for an initiative that is requesting changes to specific subfields for ...</abbr></td>
            <td class="g10">bool</td>
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
            <td class="g10">8</td>
            <td class="g10">ABCDEFGHIJKLMNO</td>
            <td class="g10"><abbr title="Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical votes will likely be multiple choice or Y/N. Vote instances are identified by the Tx-ID. AB000000000 would be chosen for Y/N (binary) type votes. Only applicable if Proposal Type is set to P for Proposal.  All other Proposal Types will be binary.  Pass/Fail.">Length 1-255 bytes. 0 is not valid. Each byte allows for a different vote option.  Typical ...</abbr></td>
            <td class="g10">varchar</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Vote Max</td>
            <td class="g10">VoteMax</td>
            <td class="g10">1</td>
            <td class="g10">15</td>
            <td class="g10"><abbr title="Range: 1-15. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N (binary)">Range: 1-15. How many selections can a voter make in a Ballot Cast.  1 is selected for Y/N ...</abbr></td>
            <td class="g10">uint</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal Description</td>
            <td class="g10">ProposalDescription</td>
            <td class="g10">32</td>
            <td class="g10">Change the name of the Contract.</td>
            <td class="g10">Length restricted by the Bitcoin protocol. 0 is valid. Description of the vote.</td>
            <td class="g10">varchar</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Proposal Document Hash</td>
            <td class="g10">ProposalDocumentHash</td>
            <td class="g10">32</td>
            <td class="g10"><abbr title="77201b0094f50df309f0343e4f44dae64d0de503c91038faf2c6b039f9f18aec">Hover for example</abbr></td>
            <td class="g10">SHA256 Hash of the proposal document to be distributed to voters</td>
            <td class="g10">bin</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Vote Cut-Off Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Referendum Action Transaction Summary

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
            <td class="g5">0</td>
            <td class="g6">Issuer's Public Address</td>
            <td class="g6"></td>
            <td class="g10">0</td>
            <td class="g10">Contract Public Address</td>
            <td class="g10">Enough for the responding action.</td>
        </tr>

       <tr>
            <td class="g5"></td>
            <td class="g6"></td>
            <td class="g6"></td>
            <td class="g10">1</td>
            <td class="g10">Contract Public Address</td>
            <td class="g10">Fund the Result at Vote cut off</td>
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
                <td class="g10">uint</td>
                <td class="g10">A field with a complex array type uses the same FieldIndex value for all elements. For example, in C1 the VotingSystems field is FieldIndex 16. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="g10">Element</td>
                <td class="g10">Element</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.</td>
                <td class="g10">uint</td>
                <td class="g10">To specify the 3rd VotingSystem of a Contract, the value 2 would be given. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="g10">Subfield Index</td>
                <td class="g10">SubfieldIndex</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">1</td>
                <td class="g10">Index of the subfield to be amended. This only applies to specific fields of an element in an array. This is used to specify which field of the array element the amendment applies to.</td>
                <td class="g10">uint</td>
                <td class="g10">For example to specify the 2nd field of a VotingSystem, value 1 would be given.</td>
            </tr>
            <tr>
                <td class="g10">Operation</td>
                <td class="g10">Operation</td>
                <td class="g10">1</td>
                <td class="g10" style="word-break:break-all">0</td>
                <td class="g10">0 = Modify. 1 = Add an element to the data to the array of elements. 2 = Delete the element listed in the Element field. The Add and Delete operations only apply to a particilar element of a complex array type. For example, it could be used to remove a particular VotingSystem from a Contract.</td>
                <td class="g10">uint</td>
                <td class="g10"></td>
            </tr>
            <tr>
                <td class="g10">Data</td>
                <td class="g10">Data</td>
                <td class="g10">32</td>
                <td class="g10" style="word-break:break-all"></td>
                <td class="g10">New data for the amended subfield. Data type depends on the the type of the field being amended.</td>
                <td class="g10">varchar</td>
                <td class="g10">The bytes should be in an format appropriate for the field being modified.</td>
            </tr>
        </table>
    </div>
</div>

