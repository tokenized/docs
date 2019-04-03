


# Result Action

Result Action -  Once a vote has been completed the results are published.

The following breaks down the construction of a Result Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Vote Tx ID - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="g9">VoteOptionsCount</td>
            <td class="g10">VoteOptionsCount</td>
            <td class="g10">1</td>
            <td class="g10">1</td>
            <td class="g10">Number of Vote Options to follow.</td>
            <td class="g10">uint</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Option X Tally</td>
            <td class="g10">OptionXTally</td>
            <td class="g10">8</td>
            <td class="g10">3000</td>
            <td class="g10">Number of valid votes counted for Option X</td>
            <td class="g10">uint</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Result</td>
            <td class="g10">Result</td>
            <td class="g10">8</td>
            <td class="g10">2</td>
            <td class="g10"><abbr title="Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw for 1st place, all winning options are listed. ">Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw ...</abbr></td>
            <td class="g10">varchar</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-Timestamp">
                   Timestamp - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Result Action Transaction Summary

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th class="s0" colspan="6">smart contract Operator Fee: 0</th>
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
            <td class="g6">Contract Public Address</td>
            <td class="g6"></td>
            <td class="g10">0</td>
            <td class="g10">Contract Public Address</td>
            <td class="g10">Dust limit rule minimum value output of 546</td>
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

