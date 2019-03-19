


# Asset Modification Action

Asset Modification Action -  Token Dilutions, Call Backs/Revocations, burning etc.

The following breaks down the construction of a Asset Modification Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-Header">
                   Header - Click to show content
                </a>
             </td>
        </tr>
        <tr>
            <td class="a9">Asset Type</td>
            <td class="a10">AssetType</td>
            <td class="a10">3</td>
            <td class="a10">SHC</td>
            <td class="a10">eg. Share - Common</td>
            <td class="a10">fixedchar</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-AssetCode">
                   Asset Code - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="a9">Asset Revision</td>
            <td class="a10">AssetRevision</td>
            <td class="a10">4</td>
            <td class="a10">0</td>
            <td class="a10"><abbr title="Counter. (Subfield cannot be manually changed by Asset Modification Action.  Only SC can increment by 1 with each AC action. SC will reject AM actions where the wrong asset revision has been selected. ">Counter. (Subfield cannot be manually changed by Asset Modification Action.  Only SC can i ...</abbr></td>
            <td class="a10">uint</td>
            <td class="a10">Cannot be Amended</td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-Amendment">
                   Modifications - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="a5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Ref Tx ID - Click to show content
                </a>
            </td>
        </tr>
    </table>
</div>

##Asset Modification Action Transaction Summary

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
            <td class="a5">0</td>
            <td class="a6">Issuer's Public Address</td>
            <td class="a6"></td>
            <td class="a10">0</td>
            <td class="a10">Contract Public Address</td>
            <td class="a10">Enough for the responding action.</td>
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
                <td class="a10">Field Index</td>
                <td class="a10">FieldIndex</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">2</td>
                <td class="a10">Index of the field to be amended.</td>
                <td class="a10">uint</td>
                <td class="a10">A field with a complex array type uses the same FieldIndex value for all elements. For example, in C1 the VotingSystems field is FieldIndex 16. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="a10">Element</td>
                <td class="a10">Element</td>
                <td class="a10">2</td>
                <td class="a10" style="word-break:break-all">0</td>
                <td class="a10">Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.</td>
                <td class="a10">uint</td>
                <td class="a10">To specify the 3rd VotingSystem of a Contract, the value 2 would be given. Indexes are zero based.</td>
            </tr>
            <tr>
                <td class="a10">Subfield Index</td>
                <td class="a10">SubfieldIndex</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">1</td>
                <td class="a10">Index of the subfield to be amended. This only applies to specific fields of an element in an array. This is used to specify which field of the array element the amendment applies to.</td>
                <td class="a10">uint</td>
                <td class="a10">For example to specify the 2nd field of a VotingSystem, value 1 would be given.</td>
            </tr>
            <tr>
                <td class="a10">Operation</td>
                <td class="a10">Operation</td>
                <td class="a10">1</td>
                <td class="a10" style="word-break:break-all">0</td>
                <td class="a10">0 = Modify. 1 = Add an element to the data to the array of elements. 2 = Delete the element listed in the Element field. The Add and Delete operations only apply to a particilar element of a complex array type. For example, it could be used to remove a particular VotingSystem from a Contract.</td>
                <td class="a10">uint</td>
                <td class="a10"></td>
            </tr>
            <tr>
                <td class="a10">Data</td>
                <td class="a10">Data</td>
                <td class="a10">32</td>
                <td class="a10" style="word-break:break-all"></td>
                <td class="a10">New data for the amended subfield. Data type depends on the the type of the field being amended.</td>
                <td class="a10">varchar</td>
                <td class="a10">The bytes should be in an format appropriate for the field being modified.</td>
            </tr>
        </table>
    </div>
</div>

