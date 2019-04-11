# Protocol Assets

- [Introduction](#introduction)
- [Available Actions](#all-assets)

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

A voucher entitling the holder to a discount off a particular product or service.

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
        <td> </td>
    </tr>
    <tr>
        <td>RedeemingEntity</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>IssueDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ExpiryDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Value</td>
        <td>
            uint(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Currency</td>
        <td>
            Currency
        </td>
        <td>Currency for coupon. From resources/currency. </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
    </tr>
</table>



<a name="action-currency"></a>
#### Currency

A Currency

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
        <td> </td>
    </tr>
    <tr>
        <td>ISOCode</td>
        <td>
            Currency
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>MonetaryAuthority</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
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
        <td> </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>OfferName</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
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
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ID</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>MembershipClass</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>RoleType</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>MembershipType</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
    </tr>
</table>



<a name="action-share-common"></a>
#### Share - Common

Common stock represents ownership interests in corporations.

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
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>TransferLockout</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td>A period of time where the asset is unable to be transferred.  After the transfer lockout period, the assets can be transferred. </td>
    </tr>
    <tr>
        <td>Ticker</td>
        <td>
            fixedchar(5)
        </td>
        <td>Ticker symbol assigned by exchanges to represent the asset. </td>
    </tr>
    <tr>
        <td>ISIN</td>
        <td>
            fixedchar(12)
        </td>
        <td>International Securities Identification Number </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
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
        <td>Payload Version </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="field-types#type-age-restriction">AgeRestriction</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>AdmissionType</td>
        <td>
            fixedchar(3)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Venue</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Class</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Area</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Seat</td>
        <td>
            varchar(8)
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>StartTimeDate</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ValidFrom</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="field-types#type-timestamp">Timestamp</a>
        </td>
        <td> </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(16)
        </td>
        <td> </td>
    </tr>
</table>


