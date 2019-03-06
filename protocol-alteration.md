
#Alteration Action

Alteration Action -  A registry entry can be altered.

The following breaks down the construction of a Alteration Action. The action is constructed by building a single string from each of the elements in order.

<div class="ritz grid-container" dir="ltr">
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
            <td class="s5" rowspan="9">Metadata (OP_RETURN Payload)</td>
            <td class="r6">Header[]</td>
            <td class="r6">Header Array</td>
            <td class="r6">-</td>
            <td class="r6">-</td>
            <td class="r6">Common header data for all messages</td>
            <td class="r6">Header</td>
            <td class="r7"></td>
        </tr>
                <tr>
            <td class="r10">Text Encoding</td>
            <td class="r10">TextEncoding</td>
            <td class="r10">1</td>
            <td class="r10" style="word-break:break-all">0</td>
            <td class="r10"> 0 = ASCII, 1 = UTF-8, 2 = UTF-16, 3 = Unicode.  Encoding applies to all 'text' data types. All 'string' types will always be encoded with ASCII.  Where string is selected, all fields will be ASCII.</td>
            <td class="r10">uint8</td>
            <td class="r11">Can be changed by Issuer or Operator at their discretion.</td>
        </tr>                <tr>
            <td class="r10">Sublist</td>
            <td class="r10">Sublist</td>
            <td class="r10">4</td>
            <td class="r10" style="word-break:break-all"></td>
            <td class="r10">Null value = Global KYC compliance. eg. Organizations can define their own pseudo-anonymous and publicly available membership lists.</td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">KYC</td>
            <td class="r10">KYC</td>
            <td class="r10">1</td>
            <td class="r10" style="word-break:break-all">Y</td>
            <td class="r10">Y/N</td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">Jurisdiction</td>
            <td class="r10">Jurisdiction</td>
            <td class="r10">5</td>
            <td class="r10" style="word-break:break-all">AUS</td>
            <td class="r10"></td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">DOB</td>
            <td class="r10">DOB</td>
            <td class="r10">8</td>
            <td class="r10" style="word-break:break-all">Tue Jun 02 1987 17:00:00 GMT+1000 (AEST)</td>
            <td class="r10">Date of Birth : DD/MM/YYYY</td>
            <td class="r10">time</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">Country of Residence</td>
            <td class="r10">CountryofResidence</td>
            <td class="r10">3</td>
            <td class="r10" style="word-break:break-all">AUS</td>
            <td class="r10"></td>
            <td class="r10">string</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">Supporting Documentation Hash</td>
            <td class="r10">SupportingDocumentationHash</td>
            <td class="r10">32</td>
            <td class="r10" style="word-break:break-all">98ea6e4f216f2fb4b69fff9b3a44842c38686ca685f3f55dc48c5d3fb1107be4</td>
            <td class="r10"></td>
            <td class="r10">sha256</td>
            <td class="r11"></td>
        </tr>                <tr>
            <td class="r10">Message</td>
            <td class="r10">Message</td>
            <td class="r10">0</td>
            <td class="r10" style="word-break:break-all">Changed Country of Residence</td>
            <td class="r10">Length 0-65,535 bytes. Note</td>
            <td class="r10">nvarchar16</td>
            <td class="r11"></td>
        </tr>
    </table>
</div>