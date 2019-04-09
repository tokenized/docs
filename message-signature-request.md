# Signature Request

Partially-signed transactions (Tokenized actions, Bitcoin, Multisig, Threshold Signatures, etc.) can be passed around on-chain to the parties (including Smart Contracts) that still have to sign the transaction.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:20%" class="s0">Field</th>
            <th style="width:10%" class="s0">Type</th>
            <th style="width:30%" class="s0">Description</th>
            <th style="width:5%" class="s0">Size</th>
            <th style="width:20%" class="s0">Example</th>
            <th class="s1">Notes</th>
        </tr>
        <tr>
            <td class="s0">Version</td>
            <td class="s0">uint</td>
            <td class="s0">Payload Version</td>
            <td class="s0">1</td>
            <td class="s0"></td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">Timestamp</td>
            <td class="s0">Timestamp</td>
            <td class="s0">Timestamp in nanoseconds for when the message sender creates the transaction.</td>
            <td class="s0">0</td>
            <td class="s0">1551767413250187179</td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">Payload</td>
            <td class="s0">varbin</td>
            <td class="s0">Full serialized bitcoin tx with multiple inputs from different wallets/users.</td>
            <td class="s0">32</td>
            <td class="s0"></td>
            <td class="s0"></td>
        </tr>
    </table>
</div>