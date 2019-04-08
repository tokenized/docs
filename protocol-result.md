


# Result Action

Result Action - Once a vote has been completed the results are published. After the result is posted, it is up to the issuer to send a contract/asset amendement if appropriate.

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
            <td class="g9">Asset Specific Vote</td>
            <td class="g10">AssetSpecificVote</td>
            <td class="g10">0</td>
            <td class="g10"></td>
            <td class="g10"><abbr title="When true this proposal is specific to an asset and the asset type and asset code fields are serialized.">When true this proposal is specific to an asset and the asset type and asset code fields a ...</abbr></td>
            <td class="g10">bool</td>
            <td class="g10"></td>
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
            <td class="g9">Specific</td>
            <td class="g10">Specific</td>
            <td class="g10">0</td>
            <td class="g10"></td>
            <td class="g10"><abbr title="When true the ProposedAmendments field is included and specifies the exact changes to make to the Contract/Asset on chain. When false this is just a general proposal like a strategy/direction and doesn't result in any on chain update.">When true the ProposedAmendments field is included and specifies the exact changes to make ...</abbr></td>
            <td class="g10">bool</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-Amendment">
                   Proposed Amendments - Click to show content
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
            <td class="g9">Option Tally</td>
            <td class="g10">OptionTally</td>
            <td class="g10">8</td>
            <td class="g10"></td>
            <td class="g10"><abbr title="List of number of valid votes counted for each vote option. Length is encoded like a regular list object, but must match the length of VoteOptions from the Proposal action.">List of number of valid votes counted for each vote option. Length is encoded like a regul ...</abbr></td>
            <td class="g10">uint64[]</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Result</td>
            <td class="g10">Result</td>
            <td class="g10">8</td>
            <td class="g10"></td>
            <td class="g10"><abbr title="Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw for 1st place, all winning options are listed.">Length 1-255 bytes. 0 is not valid. The Option with the most votes. In the event of a draw ...</abbr></td>
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
            <tr>
                <td class="g10">Protocol Identifier</td>
                <td class="g10">ProtocolID</td>
                <td class="g10">13</td>
                <td class="g10">tokenized.com</td>
                <td class="g10" style="word-break:break-all">Tokenized ID Prefix. tokenized.com</td>
                <td class="g10">byte</td>
                <td class="g10"></td>
            </tr>
            <tr>
                <td class="g10">Push Data</td>
                <td class="g10">OpPushdata</td>
                <td class="g10">1</td>
                <td class="g10">0x4d</td>
                <td class="g10" style="word-break:break-all">PACKET LENGTH, PUSHDATA1 (76), PUSHDATA2 (77), or PUSHDATA4 (78) depending on total size of action payload.</td>
                <td class="g10">byte</td>
                <td class="g10"></td>
            </tr>
            <tr>
                <td class="g10">Length of Action Payload</td>
                <td class="g10">LenActionPayload</td>
                <td class="g10"></td>
                <td class="g10">tokenized.com</td>
                <td class="g10" style="word-break:break-all">Length of the action message (0 - 65,535 bytes). 0 if pushdata length <76B, 1 byte if PUSHDATA1 is used, 2 bytes if PUSHDATA2 and 4 bytes if PUSHDATA4.</td>
                <td class="g10">byte</td>
                <td class="g10">Size depends on Action Payload.</td>
            </tr>
            <tr>
                <td class="g10">Version</td>
                <td class="g10">Version</td>
                <td class="g10">1</td>
                <td class="g10">0</td>
                <td class="g10" style="word-break:break-all">255 reserved for additional versions. Tokenized protocol versioning.</td>
                <td class="g10">uint8</td>
                <td class="g10">Can be changed by Issuer or Operator at their discretion.  Smart Contract will reject if it hasn't been updated to interpret the specified version.</td>
            </tr>
            <tr>
                <td class="g10">Action Prefix</td>
                <td class="g10">ActionPrefix</td>
                <td class="g10">2</td>
                <td class="g10">G5</td>
                <td class="g10" style="word-break:break-all">// G5 identifies data as a Result message.</td>
                <td class="g10">string</td>
                <td class="g10">Cannot be changed by issuer, operator or smart contract..</td>
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
                <td class="g10">Index of the subfield to be amended. This only applies to specific fields containing complex types with subfields. This is used to specify which field of the object the amendment applies to.</td>
                <td class="g10">uint</td>
                <td class="g10">For example to specify the 2nd field of a VotingSystem, value 1 would be given.</td>
            </tr>
            <tr>
                <td class="g10">Subfield Element</td>
                <td class="g10">SubfieldElement</td>
                <td class="g10">2</td>
                <td class="g10" style="word-break:break-all">1</td>
                <td class="g10">Specifies the element of the complex array type to be amended. This only applies to array types, and has no meaning for a simple type such as uint64, string, byte or byte[]. Specifying a value > 0 for a simple type will result in a Rejection.</td>
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
                <td class="g10">New data for the amended subfield. Data type depends on the the type of the field being amended. The value should be serialize as defined by the protocol.</td>
                <td class="g10">varbin</td>
                <td class="g10">The bytes should be in an format appropriate for the field being modified.</td>
            </tr>
        </table>
    </div>
</div>

