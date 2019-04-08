# Offer

A message that contains all of the details required for an agreement to be formed. Sent to an address(es). The Offer should have all, or nearly all, of the details required for the receiving party to accept the offer.  The Offer shall be in the form of a partially formed Bitcoin transaction with all of the relevent details (offer, consideration, offeror's payment/receipt details, etc.).  The Offer message is different to a Signature Request message in that it is missing the offeree's payment/receipt details (eg. UTXOs). If the Offer message is well received by the offeree, then the offeree can add their relevent details (eg. inputs/outputs) and sign the transaction.  If an additional signature is required from the offeror at this point, then the partially-signed transaction can be sent to the offeror by way of a Signature Request message.

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
            <td class="s0">Ref Tx Id</td>
            <td class="s0">TxId</td>
            <td class="s0">Tx Id of the request transaction referenced by the offer.</td>
            <td class="s0">0</td>
            <td class="s0"></td>
            <td class="s0">For a multi-contract settlement, the Payload will be a Settlement op return script and the RefTxId will be the id of the tx containing the Transfer.</td>
        </tr>
        <tr>
            <td class="s0">Payload</td>
            <td class="s0">varbin</td>
            <td class="s0">Full serialized op return script containing an offer to another party, usually to exchange tokens/bitcoin. The message needs data added by another party.</td>
            <td class="s0">32</td>
            <td class="s0"></td>
            <td class="s0"></td>
        </tr>
    </table>
</div>
