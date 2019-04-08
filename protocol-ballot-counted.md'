


# Ballot Counted Action

Ballot Counted Action - The smart contract will respond to a Ballot Cast action with a Ballot Counted action if the Ballot Cast is valid. If the Ballot Cast is not valid, then the smart contract will respond with a Rejection Action.

The following breaks down the construction of a Ballot Counted Action. The action is constructed by building a single string from each of the elements in order.

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
            <td class="g5" colspan="7">
                <a href="javascript:;" data-popover="type-TxId">
                   Vote Tx ID - Click to show content
                </a>
            </td>
        </tr>
        <tr>
            <td class="g9">Vote</td>
            <td class="g10">Vote</td>
            <td class="g10">8</td>
            <td class="g10">A</td>
            <td class="g10"><abbr title="Length 1-255 bytes. 0 is not valid. Max length is the VoteMax value from the Proposal action. Accept, Reject, Abstain, Spoiled, Multiple Choice, or Preference List. 15 options total. Order of preference. 1st position = 1st choice. 2nd position = 2nd choice, etc. A is always Accept and B is always reject in a Y/N votes.">Length 1-255 bytes. 0 is not valid. Max length is the VoteMax value from the Proposal acti ...</abbr></td>
            <td class="g10">varchar</td>
            <td class="g10"></td>
        </tr>
        <tr>
            <td class="g9">Quantity</td>
            <td class="g10">Quantity</td>
            <td class="g10">8</td>
            <td class="g10"></td>
            <td class="g10"><abbr title="Number of votes counted for this ballot. Factors in vote multipliers if there are any allowed, otherwise it is just quantity of tokens held.">Number of votes counted for this ballot. Factors in vote multipliers if there are any allo ...</abbr></td>
            <td class="g10">uint</td>
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

##Ballot Counted Action Transaction Summary

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
                <td class="g10">G4</td>
                <td class="g10" style="word-break:break-all">// G4 identifies data as a BallotCounted message.</td>
                <td class="g10">string</td>
                <td class="g10">Cannot be changed by issuer, operator or smart contract..</td>
            </tr>
        </table>
    </div>
</div>
