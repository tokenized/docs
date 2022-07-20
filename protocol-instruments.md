# Protocol Instruments

- [Introduction](#introduction)
- [Available Instruments](#available-instruments)
- [Field Types](#field-types)
- [Field Aliases](#field-aliases)

<a name="introduction"></a>

## Introduction

Instrument Types are used with reference to the `InstrumentPayload` field found in the Instrument Definition, Instrument Creation and Instrument Modification actions.

<a name="available-instruments"></a>

## Available Instruments

<div class="content-list collection-method-list" markdown="1">

- [Membership](#membership)
- [Currency](#currency)
- [Share - Common](#share---common)
- [Bond - Fixed Rate](#bond---fixed-rate)
- [Coupon](#coupon)
- [Loyalty Points](#loyalty-points)
- [Ticket (Admission)](#ticket-admission)
- [Casino Chip](#casino-chip)
- [Information Service License](#information-service-license)
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
            Age restriction is used to specify required ages for instrument ownership.
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
            varchar(tiny)
        </td>
        <td>
             Example: 34536457575486868
        </td>
    </tr>
    <tr>
        <td>MembershipClass</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Owner, Administrator, Manager, General, can be NULL.
        </td>
    </tr>
    <tr>
        <td>RoleType</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Director, Partner, CEO, COO, etc., can be NULL from Roles in Resources/Roles
        </td>
    </tr>
    <tr>
        <td>MembershipType</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Silver, Platinum, can be NULL.
        </td>
    </tr>
    <tr>
        <td>Description</td>
        <td>
            varchar(small)
        </td>
        <td>
             This field is always required.  Example: Rights and duties listed.
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>
</table>

<a name="currency"></a>

#### Currency

Currency, fiat money, cash. Issued by a monetary authority (eg. Reserve Bank of Australia, ECB, Bank of England). Currency is free of counterparty risk except for the risks associated with the management of the currency by the monetary authority and its recognition as acceptable legal tender by the market and associated government(s). Custody of currency must be backed by a 1:1 ratio, or a full reserve. A currency instrument type should be considered the digital equivalent of physical cash.

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
             This field is always required.  Example: AUD
        </td>
    </tr>
    <tr>
        <td>MonetaryAuthority</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Reserve Bank of Australia
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Description</td>
        <td>deprecated</td>
        <td>
            Deprecated because the currency instrument should be distinguished by its meta data and contract.
             Example: Australian dollar
        </td>
    </tr>
    <tr>
        <td>Precision</td>
        <td>
            uint(8)
        </td>
        <td>
            Required field to specify the decimal precision of a currency. It will normally be the &#34;precision&#34; value associated with the CurrencyCode. It is the number of decimal places between the number of tokens and the common unit of measure. For example, in AUD, the common unit is the dollar, but a token would only be worth a penny. So the precision should be 2 for the two decimal places in a dollar amount &#34;$1.00&#34;. In this scenario 100 tokens are worth $1.
             This field is always required.  Example: 100
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
        <td>Ticker</td>
        <td>
            fixedchar(5)
        </td>
        <td>
            Ticker symbol assigned by exchanges to represent the instrument.
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
            varchar(small)
        </td>
        <td>
             This field is always required.  Example: Class C
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>

</table>

<a name="bond-fixed-rate"></a>

#### Bond - Fixed Rate

A fixed rate bond is a bond that pays the same level of interest over its entire term. An investor who wants to earn a guaranteed interest rate for a specified term could purchase a fixed rate bond in the form of a Treasury, corporate bond, municipal bond, or certificate of deposit (CD).

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Name</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            Name of bond
             Example: City of Chicago, Midway Airport, Series 2001A
        </td>
    </tr>
    <tr>
        <td>BondType</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            Type of bond.
                <br>C - Corporate
                <br>M - Municipal
                <br>G - Government / Sovereign
             <br>This field is always required.
             <br>Example: C
        </td>
    </tr>
    <tr>
        <td>ISIN</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            International Securities Identification Number or Committee on Uniform Securities Identification Procedures.
            Example: US0004026250
        </td>
    </tr>
    <tr>
        <td>Collateral</td>
        <td>
            varchar(small)
        </td>
        <td>
            An instrument that secures securing the bond.  If null, then the bond is unsecured.
        </td>
    </tr>
    <tr>
        <td>ParValue</td>
        <td>
            <a href="#type-currency-value">CurrencyValue</a>
        </td>
        <td>
            Par value of the bond. The value that will be paid at maturity.
             This field is always required.
        </td>
    </tr>
    <tr>
        <td>InterestRate</td>
        <td>
            <a href="#type-rate">Rate</a>
        </td>
        <td>
            The fixed interest rate of the bond.
        </td>
    </tr>
    <tr>
        <td>InterestPaymentInitialDate</td>
        <td>
            <a href="#alias-uint">TimestampSeconds</a>
        </td>
        <td>
            Unix epoch date time (in seconds) for the first interest payment.
            This field is required when the field InterestRate is specified.
            This field is only valid when the field InterestRate is specified.
        </td>
    </tr>
    <tr>
        <td>InterestPaymentDateDeltas</td>
        <td>
            <a href="#alias-uint">uint[0]</a>
        </td>
        <td>
            Number of seconds from the previous interest payment until the next payment. A delta in seconds from the previous payment.
            This field is required when the field InterestRate is specified.
            This field is only valid when the field InterestRate is specified.
        </td>
    </tr>
    <tr>
        <td>LatePaymentPenaltyRate</td>
        <td>
            <a href="#type-rate">Rate</a>
        </td>
        <td>
            The rate of the penalty per the penalty period.
        </td>
    </tr>
    <tr>
        <td>LatePaymentWindow</td>
        <td>
            <a href="#alias-uint">TimestampSeconds</a>
        </td>
        <td>
            The amount of time after a payment is due before the late payment penalty is applied.
            This field is only valid when the field LatePaymentPenaltyRate is specified.
        </td>
    </tr>
    <tr>
        <td>LatePaymentPenaltyPeriod</td>
        <td>
            <a href="#alias-uint">TimestampSeconds</a>
        </td>
        <td>
            The period at which the late payment penalty accrues.
            This field is only valid when the field LatePaymentPenaltyRate is specified.
        </td>
    </tr>
    <tr>
        <td>MaturityDate</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
            The date of the maturity of the bond. When the par value is paid.
            This field is always required.
        </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for instrument ownership.
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
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
            varchar(tiny)
        </td>
        <td>
            The entity responsible for redemption of this coupon.
             Example: Woolworths - Robina Town Centre
        </td>
    </tr>
    <tr>
        <td>ValidFromTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Value</td>
        <td>deprecated</td>
        <td>
            Deprecated for FaceValue.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Currency</td>
        <td>deprecated</td>
        <td>
            Deprecated for FaceValue.
        </td>
    </tr>
    <tr>
        <td>CouponName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             This field is always required.  Example: Gift Card
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Precision</td>
        <td>deprecated</td>
        <td>
            Deprecated for FaceValue.
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>
    <tr>
        <td>FaceValue</td>
        <td>
            <a href="#type-currency-value">CurrencyValue</a>
        </td>
        <td>
            Face value of each coupon specified in a currency.
        </td>
    </tr>
    <tr>
        <td>RedemptionVenue</td>
        <td>
            varchar(tiny)
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>Details</td>
        <td>
            varchar(small)
        </td>
        <td>
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
            Age restriction is used to specify required ages for instrument ownership.
        </td>
    </tr>
    <tr>
        <td>ProgramName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             This field is always required.  Example: Qantas Frequent Flyer Points
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ValidFrom</td>
        <td>deprecated</td>
        <td>
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>Details</td>
        <td>
            varchar(small)
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
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
            Age restriction is used to specify required ages for instrument ownership.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)AdmissionType</td>
        <td>deprecated</td>
        <td>
        </td>
    </tr>
    <tr>
        <td>Venue</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Orion Cinemas - 293 Stehpens St, Vancouver, BC V4A 9V1
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Class</td>
        <td>deprecated</td>
        <td>
             Example: Gold Class, Platinum, VIP, Section A, etc.
        </td>
    </tr>
    <tr>
        <td>Area</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Upper Bowl
        </td>
    </tr>
    <tr>
        <td>Seat</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Seat 5, or A122
        </td>
    </tr>
    <tr>
        <td>EventStartTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ValidFrom</td>
        <td>deprecated</td>
        <td>
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ExpirationTimestamp</td>
        <td>deprecated</td>
        <td>
        </td>
    </tr>
    <tr>
        <td>EventName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             This field is always required.  Example: Coingeek Conference - London (November 2018).
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>
    <tr>
        <td>Details</td>
        <td>
            varchar(small)
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>Section</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Sec 1
        </td>
    </tr>
    <tr>
        <td>Row</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             Example: Sec 1
        </td>
    </tr>
    <tr>
        <td>EventEndTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
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
        <td>(Deprecated)CurrencyCode</td>
        <td>deprecated</td>
        <td>
            Deprecated for FaceValue
        </td>
    </tr>
    <tr>
        <td>UseType</td>
        <td>
            fixedchar(1)
        </td>
        <td>
            Real Money (R), Free Play (F)
             This field is always required.  Example: R
        </td>
    </tr>
    <tr>
        <td>AgeRestriction</td>
        <td>
            <a href="#type-age-restriction">AgeRestriction</a>
        </td>
        <td>
            Age restriction is used to specify required ages for instrument ownership.
        </td>
    </tr>
    <tr>
        <td>(Deprecated)ValidFrom</td>
        <td>deprecated</td>
        <td>
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>(Deprecated)Precision</td>
        <td>deprecated</td>
        <td>
            Deprecated for FaceValue
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>
    <tr>
        <td>CasinoName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
            The name of the casino, or host, of the chip.
             This field is always required.
        </td>
    </tr>
    <tr>
        <td>FaceValue</td>
        <td>
            <a href="#type-currency-value">CurrencyValue</a>
        </td>
        <td>
            Face value of each coupon specified in a currency.
             This field is always required.
        </td>
    </tr>

</table>

<a name="information-service-license"></a>

#### Information Service License

Information Service License

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
            Age restriction is used to specify required ages for instrument ownership.
        </td>
    </tr>
    <tr>
        <td>ExpirationTimestamp</td>
        <td>
            <a href="#alias-uint">Timestamp</a>
        </td>
        <td>
        </td>
    </tr>
    <tr>
        <td>ServiceName</td>
        <td>
            varchar(tiny)
        </td>
        <td>
             This field is always required.
        </td>
    </tr>
    <tr>
        <td>TransfersPermitted</td>
        <td>
            bool
        </td>
        <td>
            Set to true if transfers are permitted between two parties, otherwise set to false to prevent peer-to-peer transfers.
        </td>
    </tr>
    <tr>
        <td>URL</td>
        <td>
            varchar(small)
        </td>
        <td>
            URL linking to any related documents or media
        </td>
    </tr>

</table>

<a name="field-types"></a>

## Field Types

<div class="content-list collection-method-list" markdown="1">
- [Age Restriction](#type-age-restriction)
- [Currency Value](#type-currency-value)
- [Rate](#type-rate)
</div>

<a name="type-age-restriction"></a>

### Age Restriction

Age restriction is used to specify required ages for instrument ownership.

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
            The lowest age valid to own instrument. Zero for no restriction.
        </td>
    </tr>
    <tr>
        <td>Upper</td>
        <td>
            uint(1)
        </td>
        <td>
            The highest age valid to own instrument. Zero for no restriction.
        </td>
    </tr>

</table>

<a name="type-currency-value"></a>

### Currency Value

A value specified in terms of a currency.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Value</td>
        <td>
            uint(8)
        </td>
        <td>
            Denominated in precision specified in Precision field.
             This field is always required.  Example: 100
        </td>
    </tr>
    <tr>
        <td>CurrencyCode</td>
        <td>
            <a href="#alias-fixedchar">CurrencyType</a>
        </td>
        <td>
            International Organization for Standardization code for Currency. Currency for coupon. From  resources/currency.
            This field is always required.  Example: AUD
        </td>
    </tr>
    <tr>
        <td>Precision</td>
        <td>
            uint(1)
        </td>
        <td>
            Required field to specify the decimal precision of the value. It will normally be the  &#34;precision&#34; value associated with the Currency. It is the number of decimal places between  the number of tokens and the common unit of measure. For example, in AUD, the common unit is  the dollar, but a token would only be worth a penny. So the precision should be 2 for the  two decimal places in a dollar amount &#34;$1.00&#34;. In this scenario 100 tokens are worth $1.
            This field is always required.  Example: 2
        </td>
    </tr>

</table>

<a name="type-rate"></a>

### Rate

A rate value specified in terms of a precision.

<table>
    <tr>
        <th style="width:15%">Field</th>
        <th style="width:15%">Type</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Precision</td>
        <td>
            uint(1)
        </td>
        <td>
            Required field to specify the decimal precision of the value. It will normally be the  &#34;precision&#34; value associated with the Currency. It is the number of decimal places between  the number of tokens and the common unit of measure. For example, in AUD, the common unit is  the dollar, but a token would only be worth a penny. So the precision should be 2 for the  two decimal places in a dollar amount &#34;$1.00&#34;. In this scenario 100 tokens are worth $1.
            Example: 2
        </td>
    </tr>
    <tr>
        <td>Value</td>
        <td>
            uint(8)
        </td>
        <td>
             Example: Denominated in precision specified in Precision field.
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
                Example: 1594668650000000000
            </td>
        </tr>
        <tr id="alias-timestamp-seconds">
            <td>TimestampSeconds</td>
            <td>
                uint(8)
            </td>
            <td>
                Represents a time encoded as a 64 bit unsigned integer representing the number of seconds since the Unix epoch.
                Example: 1594668654
            </td>
        </tr>
        <tr id="alias-seconds">
            <td>Seconds</td>
            <td>
                uint(8)
            </td>
            <td>
                Represents a time delta encoded as a 64 bit unsigned integer representing the number of seconds since a previous timestamp.
                Example: 1500
            </td>
        </tr>

</table>
