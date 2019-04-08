# ShareCommon

Common stock represents ownership interests in corporations.

<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:20%" class="s0">Field</th>
            <th style="width:10%" class="s0">Type</th>
            <th style="width:30%" class="s0">Description</th>
            <th style="width:5%" class="s0">Size</th>
            <th class="s1">Example</th>
        </tr>
        <tr>
            <td class="s0">Version</td>
            <td class="s0">uint</td>
            <td class="s0">Payload Version</td>
            <td class="s0">1</td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">TransferLockout</td>
            <td class="s0">Timestamp</td>
            <td class="s0">A period of time where the asset is unable to be transferred.  After the transfer lockout period, the assets can be transferred.</td>
            <td class="s0">0</td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">Ticker Symbol</td>
            <td class="s0">fixedchar</td>
            <td class="s0">Ticker symbol assigned by exchanges to represent the asset.</td>
            <td class="s0">5</td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">ISIN (optional)</td>
            <td class="s0">fixedchar</td>
            <td class="s0">International Securities Identification Number</td>
            <td class="s0">12</td>
            <td class="s0"></td>
        </tr>
        <tr>
            <td class="s0">Description</td>
            <td class="s0">varchar</td>
            <td class="s0"></td>
            <td class="s0">16</td>
            <td class="s0"></td>
        </tr>
    </table>
</div>
