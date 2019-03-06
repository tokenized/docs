
<html>
    <head>
        <link rel="stylesheet" href="css/style.css">
        <H1>Confiscation Action</H1>
        <p>
        Confiscation Action -  to be used to comply with contractual obligations and/or legal requirements.<br><br>
        The following breaks down the construction of a Confiscation Action. The action is constructed by building a single string from each of the elements in order.
        </p>
    </head>
    <div class="ritz grid-container" dir="ltr">
        <body>
            <table class="waffle" cellspacing="0" cellpadding="0" table-layout=fixed width=100%>
                 <tr style='height:19px;'>
                    <th style="width:6%" class="s0">Field</th>
                       <th style="width:9%" class="s1">Label</th>
                    <th style="width:9%" class="s1">Name</th>
                    <th style="width:2%" class="s1">Bytes</th>
                    <th style="width:29%" class="s1">Example Values</th>
                    <th style="width:26%" class="s1">Comments</th>
                    <th style="width:5%" class="s1">Data Type</th>
                    <th style="width:14%" class="s2">Amendment Restrictions</th>
                </tr>
                <tr>
                    <td class="s5" rowspan="5">Metadata (OP_RETURN Payload)</td>
                    <td class="e6">Header[]</td>
                    <td class="e6">Header Array</td>
                    <td class="e6">-</td>
                    <td class="e6">-</td>
                    <td class="e6">Common header data for all messages</td>
                    <td class="e6">Header</td>
                    <td class="e7"></td>
                </tr>
                    <tr>
                    <td class="e10">Number of Addresses</td>
                    <td class="e10">AddressCount</td>
                    <td class="e10">2</td>
                    <td class="e10" style="word-break:break-all">0</td>
                    <td class="e10">0 - 65,535</td>
                    <td class="e10">uint16</td>
                    <td class="e11"></td>
                </tr>                <tr>
                    <td class="e10">Addresses</td>
                    <td class="e10">Addresses</td>
                    <td class="e10">0</td>
                    <td class="e10" style="word-break:break-all"></td>
                    <td class="e10">Addresses holding tokens to be confiscated.</td>
                    <td class="e10">Address[]</td>
                    <td class="e11"></td>
                </tr>                <tr>
                    <td class="e10">Deposit Qty</td>
                    <td class="e10">DepositQty</td>
                    <td class="e10">8</td>
                    <td class="e10" style="word-break:break-all">10000</td>
                    <td class="e10">Custodian's token balance after confiscation.</td>
                    <td class="e10">uint64</td>
                    <td class="e11"></td>
                </tr>                <tr>
                    <td class="e10">Timestamp</td>
                    <td class="e10">Timestamp</td>
                    <td class="e10">8</td>
                    <td class="e10" style="word-break:break-all">1551767413250187179</td>
                    <td class="e10">Timestamp in nanoseconds of when the smart contract created the action.</td>
                    <td class="e10">timestamp</td>
                    <td class="e11">Cannot be changed by issuer, operator. Smart contract controls.</td>
                </tr>
            </table>
        </body>
    </div>
</html>