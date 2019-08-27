# Protocol Assets

- [Introduction](#introduction)
- [Available Assets](#all-assets)
- [Field Types](#field-types)
- [Field Aliases](#field-aliases)

<a name="introduction"></a>
## Introduction

Asset Types are used with reference to the `AssetPayload` field found in the Asset Definition, Asset Creation and Asset Modification actions.

<a name="all-assets"></a>
## Available Assets

<div class="content-list collection-method-list" markdown="1">
- [Membership](#membership)
- [Currency](#currency)
- [Share - Common](#share-common)
- [Coupon](#coupon)
- [Loyalty Points](#loyalty-points)
- [Ticket (Admission)](#ticket-admission)
- [Casino Chip](#casino-chip)
</div>

<a name="membership"></a>
#### Membership

A Membership

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>

    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ID</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: 34536457575486868
        </td>
    </tr>

    <tr>
        <td>MembershipClass</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Owner, Administrator, Manager, General, can be NULL.
        </td>
    </tr>

    <tr>
        <td>RoleType</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Director, Partner, CEO, COO, etc., can be NULL from Roles in Resources/Roles
        </td>
    </tr>

    <tr>
        <td>MembershipType</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Silver, Platinum, can be NULL.
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Rights and duties listed.
        </td>
    </tr>

</table>



<a name="currency"></a>
#### Currency

Currency, fiat money, cash.  Issued by a monetary authority (eg. Reserve Bank of Australia, ECB, Bank of England).  Currency is free of counterparty risk except for the risks associated with the management of the currency by the monetary authority and its recognition as acceptable legal tender by the market and associated government(s).  Custody of currency must be backed by a 1:1 ratio, or a full reserve. A currency asset type should be considered the digital equivalent of physical cash.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>CurrencyCode</td>
        <td>
            <a href="#alias-fixedchar">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. (Specification/Resources)
             Example: AUD
        </td>
    </tr>

    <tr>
        <td>MonetaryAuthority</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Reserve Bank of Australia
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Australian dollar
        </td>
    </tr>

</table>



<a name="share-common"></a>
#### Share - Common

Common stock represents ownership interests in companies.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>TransferLockout</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            A period of time where the asset is unable to be transferred.  After the transfer lockout period, the assets can be transferred.
             Example: 11/4/2019 18:00:00
        </td>
    </tr>

    <tr>
        <td>Ticker</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            Ticker symbol assigned by exchanges to represent the asset.
             Example: AAPL
        </td>
    </tr>

    <tr>
        <td>ISIN</td>
        <td>
            fixedchar(12)
        </td>
        <td>
            International Securities Identification Number
             Example: US0004026250
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Class C
        </td>
    </tr>

</table>



<a name="coupon"></a>
#### Coupon

A voucher entitling the holder to a discount on a particular product or service.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>RedeemingEntity</td>
        <td>
            varchar
        </td>
        <td>
            The entity responsible for redemption of this coupon.
             Example: Woolworths - Robina Town Centre
        </td>
    </tr>

    <tr>
        <td>IssueDate</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Sat Dec 12 2015 18:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ExpiryDate</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Sat Dec 12 2020 18:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>Value</td>
        <td>
            uint(8)
        </td>
        <td>
            
             Example: Denominated in the smallest unit of currency specified in the Currency subfield.
        </td>
    </tr>

    <tr>
        <td>Currency</td>
        <td>
            <a href="#alias-fixedchar">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. Currency for coupon. From resources/currency.
             Example: AUD
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Gift Card
        </td>
    </tr>

</table>



<a name="loyalty-points"></a>
#### Loyalty Points

A Loyalty Point

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>

    <tr>
        <td>OfferName</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Qantas Frequent Flyer Points
        </td>
    </tr>

    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Coingeek Conference - London (November 2018).
        </td>
    </tr>

</table>



<a name="ticket-admission"></a>
#### Ticket (Admission)

Admission ticket

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>

    <tr>
        <td>AdmissionType</td>
        <td>
            fixedchar(3)
        </td>
        <td>
            
             Example: MOV - Movie, CON - Conference, MUS - Music/Concert, GAM - Sports/Game/Athletics, EXH - Exhibition
        </td>
    </tr>

    <tr>
        <td>Venue</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Orion Cinemas - 293 Stehpens St, Vancouver, BC V4A 9V1
        </td>
    </tr>

    <tr>
        <td>Class</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Gold Class, Platinum, VIP, Section A, etc.
        </td>
    </tr>

    <tr>
        <td>Area</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Upper Bowl
        </td>
    </tr>

    <tr>
        <td>Seat</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Sec 1, Row 3, Seat 5, or A122
        </td>
    </tr>

    <tr>
        <td>StartTimeDate</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Mon Nov 05 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>Description</td>
        <td>
            varchar
        </td>
        <td>
            
             Example: Coingeek Conference - London (November 2018).
        </td>
    </tr>

</table>



<a name="casino-chip"></a>
#### Casino Chip

Casino Chip

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>CurrencyCode</td>
        <td>
            <a href="#alias-fixedchar">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. (Specification/Resources)
             Example: AUD
        </td>
    </tr>

    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>

    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT&#43;1000 (AEST)
        </td>
    </tr>

</table>



<a name="field-types"></a>
## Field Types

<div class="content-list collection-method-list" markdown="1">
- [Age Restriction](#type-age-restriction)
</div>



<a name="type-age-restriction"></a>
### Age Restriction

Age restriction is used to specify required ages for asset ownership.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Lower</td>
        <td>
            uint(1)
        </td>
        <td>
            The lowest age valid to own asset. Zero for no restriction.
            
        </td>
    </tr>

    <tr>
        <td>Upper</td>
        <td>
            uint(1)
        </td>
        <td>
            The highest age valid to own asset. Zero for no restriction.
            
        </td>
    </tr>

</table>



<a name="field-aliases"></a>
## Field Aliases

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
        <tr id="alias-currency-type">
            <td>CurrencyType</td>
            <td>
                fixedchar(3)
            </td>
            <td>
                International Organization for Standardization code for Currency. 3 character code.
                 Example: AUD
            </td>
        </tr>
        <tr id="alias-timestamp">
            <td>Timestamp</td>
            <td>
                uint(8)
            </td>
            <td>
                Represents a time, encoded as a 64 bit unsigned integer representing the number of nanoseconds since the Unix epoch.
                 Example: Wed May 09 2018 00:00:00 GMT&#43;1000 (AEST)
            </td>
        </tr>
</table>
