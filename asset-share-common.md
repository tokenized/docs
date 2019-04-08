# ShareCommon

Common stock represents ownership interests in corporations.



<div class="ritz grid-container" dir="ltr">
    <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
         <tr style='height:19px;'>
            <th style="width:18%" class="s1">Field</th>
            <th style="width:9%" class="s1">Type</th>
            <th style="width:15%" class="s1">Description</th>
            <th style="width:20%" class="s1">Size</th>
            <th class="s1">Example</th>
        </tr>
        <tr>
            <td class="a10">Version</td>
            <td class="a10">uint</td>
            <td class="a10">Payload Version</td>
            <td class="a10">1</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a10">TransferLockout</td>
            <td class="a10">Timestamp</td>
            <td class="a10">A period of time where the asset is unable to be transferred.  After the transfer lockout period, the assets can be transferred.</td>
            <td class="a10">0</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a10">Ticker Symbol</td>
            <td class="a10">fixedchar</td>
            <td class="a10">Ticker symbol assigned by exchanges to represent the asset.</td>
            <td class="a10">5</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a10">ISIN (optional)</td>
            <td class="a10">fixedchar</td>
            <td class="a10">International Securities Identification Number</td>
            <td class="a10">12</td>
            <td class="a10"></td>
        </tr>
        <tr>
            <td class="a10">Description</td>
            <td class="a10">varchar</td>
            <td class="a10"></td>
            <td class="a10">16</td>
            <td class="a10"></td>
        </tr>
    </table>
</div>
