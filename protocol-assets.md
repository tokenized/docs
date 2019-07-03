# Protocol Assets

- [Introduction](#introduction)
- [Available Assets](#all-assets)

<a name="introduction"></a>
## Introduction

Asset Types are used with reference to the `AssetPayload` field found in the Asset Definition, Asset Creation and Asset Modification actions.

<a name="all-assets"></a>
## Available Assets

<div class="content-list collection-method-list" markdown="1">
- [Coupon](#action-coupon)
- [Currency](#action-currency)
- [Loyalty Points](#action-loyalty-points)
- [Membership](#action-membership)
- [Share - Common](#action-share-common)
- [Ticket (Admission)](#action-ticket-admission)
</div>

<a name="action-coupon"></a>
#### Coupon

A voucher entitling the holder to a discount on a particular product or service.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>RedeemingEntity</td>
        <td>
            varchar(8)
        </td>
        <td>
            The entity responsible for redemption of this coupon.
             Example: Woolworths - Robina Town Centre
        </td>
    </tr>
    <tr>
        <td>IssueDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Sat Dec 12 2015 18:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ExpiryDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Sat Dec 12 2020 18:00:00 GMT+1000 (AEST)
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
            <a href="resources#resource-currencies">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. Currency for coupon. From resources/currency.
             Example: AUD
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Gift Card
        </td>
    </tr>
</table>



<a name="action-currency"></a>
#### Currency

Currency, fiat money, cash.  Issued by a monetary authority (eg. Reserve Bank of Australia, ECB, Bank of England).  Currency is free of counterparty risk except for the risks associated with the management of the currency by the monetary authority and its recognition as acceptable legal tender by the market and associated government(s).  Custody of currency must be backed by a 1:1 ratio, or a full reserve. A currency asset type should be considered the digital equivalent of physical cash.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>ISOCode</td>
        <td>
            <a href="resources#resource-currencies">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. (Specification/Resources)
             Example: AUD
        </td>
    </tr>
    <tr>
        <td>MonetaryAuthority</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Reserve Bank of Australia
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Australian dollar
        </td>
    </tr>
</table>



<a name="action-loyalty-points"></a>
#### Loyalty Points

A Loyalty Point

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>
    <tr>
        <td>OfferName</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Qantas Frequent Flyer Points
        </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Coingeek Conference - London (November 2018).
        </td>
    </tr>
</table>



<a name="action-membership"></a>
#### Membership

A Membership

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for asset ownership.
            
        </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ID</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: 34536457575486868
        </td>
    </tr>
    <tr>
        <td>MembershipClass</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Owner, Administrator, Manager, General, can be NULL.
        </td>
    </tr>
    <tr>
        <td>RoleType</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Director, Partner, CEO, COO, etc., can be NULL from Roles in Resources/Roles
        </td>
    </tr>
    <tr>
        <td>MembershipType</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Silver, Platinum, can be NULL.
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Rights and duties listed.
        </td>
    </tr>
</table>



<a name="action-share-common"></a>
#### Share - Common

Common stock represents ownership interests in companies.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>TransferLockout</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
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
            varchar(16)
        </td>
        <td>
            
             Example: Class C
        </td>
    </tr>
</table>



<a name="action-ticket-admission"></a>
#### Ticket (Admission)

Admission ticket

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            uint(1)
        </td>
        <td>
            The version number that this asset payload adheres to.
             Example: 0
        </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
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
            varchar(8)
        </td>
        <td>
            
             Example: Orion Cinemas - 293 Stehpens St, Vancouver, BC V4A 9V1
        </td>
    </tr>
    <tr>
        <td>Class</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Gold Class, Platinum, VIP, Section A, etc.
        </td>
    </tr>
    <tr>
        <td>Area</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Upper Bowl
        </td>
    </tr>
    <tr>
        <td>Seat</td>
        <td>
            varchar(8)
        </td>
        <td>
            
             Example: Sec 1, Row 3, Seat 5, or A122
        </td>
    </tr>
    <tr>
        <td>StartTimeDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Mon Nov 05 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>
            
             Example: Fri Nov 09 2018 09:00:00 GMT+1000 (AEST)
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td>
            
             Example: Coingeek Conference - London (November 2018).
        </td>
    </tr>
</table>


