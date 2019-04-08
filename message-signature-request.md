# SignatureRequest

Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.



<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:20%" class="s1">Field</th>
            <th style="width:10%" class="s1">Type</th>
            <th style="width:30%" class="s1">Description</th>
            <th style="width:5%" class="s1">Size</th>
            <th style="width:20%" class="s1">Example</th>
            <th class="s1">Notes</th>
        </tr>
        <tr>
            <td class="110">Version</td>
            <td class="110">uint</td>
            <td class="110">Payload Version</td>
            <td class="110">1</td>
            <td class="110"></td>
            <td class="110"></td>
        </tr>
        <tr>
            <td class="110">Timestamp</td>
            <td class="110">Timestamp</td>
            <td class="110">Timestamp in nanoseconds for when the message sender creates the transaction.</td>
            <td class="110">0</td>
            <td class="110">1551767413250187179</td>
            <td class="110"></td>
        </tr>
        <tr>
            <td class="110">Payload</td>
            <td class="110">varbin</td>
            <td class="110">Full serialized bitcoin tx with multiple inputs from different wallets/users.</td>
            <td class="110">32</td>
            <td class="110"></td>
            <td class="110"></td>
        </tr>
    </table>
</div>
