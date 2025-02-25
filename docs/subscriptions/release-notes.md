---
sidebar_position: 8
---

# Release Notes

## Coming soon

There is a plan to introduce a new refund error code (60008) on 15th of October. The error is related to a situation when a refund is declined due to no funds in merchant’s account.

## 2022

#### 14 November 2022 - Payment agreement deletion by users

Users can always delete payment agreement from the app from 5.22.0 app version.

![Agreement deletion](/img/subs-agreement_deletion_by_user.png)

#### 13 September 2022 - Update on agreement signing flow

With MobilePay app August release (version 5.20.0) agreement context screen was removed. In agreement confirm screen confirmation checkbox was added. Updated flow you can find [here](/docs/subscriptions/agreement#agreement-signing-in-dual-device-flow).

#### 24 August 2022 - Deprecated features section added

There is now a section in the menu dedicated for deprecated features.

#### 17 June 2022 - NextPaymentDate is no longer used

NextPaymentDate is no longer used in any of the requests and responses.

#### 12 May 2022 - Refunds can be done 90 days after payment

Instead of 30 days, [refunds](/docs/subscriptions/refund) can now be done 90 days after payment.

## 2021

#### 22 December 2021 - Line break in attachment's comment field

Merchants are now able to add a line break in the payment attachment's comment field using "\n".

More information in [Invoice](/docs/subscriptions/invoice).

#### 28 July 2021 - Multiple payments on same due date

Merchants are now able to create multiple payments for same AgreementId and DueDate but such payments must have different ExternalId.

More information in [Payment frequency](/docs/subscriptions/subscriptions-payments#frequency-of-payment-requests).

#### 12 July 2021 - Payment attachments V2

The purpose of payment attachments V2 is to replace existing invoice PDF functionality and to offer more flexibility for the merchant. With this new functionality you will be able to choose how attachment will be presented to the user:

- External URL. Your own link to the payment document.
- Attachment details. Extra payment details.
- MobilePay generated PDF. PDF document generated from the attachment details.

More information in [Invoice](/docs/subscriptions/invoice).

#### 23 April 2021 - Sms messages for suspended payments

We recently implemented SMS sending to users, in case they have a `suspended` payment. The purpose of the SMS is to prompt the customer to pay quicker. `suspended`  means that the the Merchant could not withdraw the money from the customers payment card. There can be various reasons why it can he suspended. If the problem persists, and there is not sufficient funds on the customers card, or/and if the card is expired or/and blocked, then the payment will fail. Suspended is a status internally for MobilePay to mark hiccupped payments, which is why it is not a part of the callback table [here](/docs/subscriptions/subscriptions-payments#callbacks). You should still see the status `failed` or `executed` as the final status

|New Status|Condition|When to expect|Callback *status*  | Callback *status_text* | Callback *status_code* |
|----------|---------|--------------|-------------------|------------------------|------------------------|
|Executed  |_The payment was successfully executed on the due-date_| After 03:15 in the morning of the due-date |Executed  | | 0 |
|Failed    |_Payment failed to execute during the due-date or at the end of grace period._| After 23:59 of the due-date, or the last day of grace period. |Failed    | | 50000 |

`failed` callback entails that MobilePay has sent push messages and SMS to the user, and the payment still didn't go through. If you get the callback status `failed`, we recommend that you contact the user to find the root cause.

Sms are sent at 10:00 in Denmark and 11:00 in Finland.

#### 22 January 2021 - Visual design of PDF changed

More information in [Invoice](/docs/subscriptions/invoice), PDF Invoice example.

#### 4 January 2021 - One-off payment expiration

[One-off](/docs/subscriptions/one-off-payments#expired-one-off) payment expiration date changed from 14 to 7 days.

## 2020

#### 16 December 2020 - Updated agreement POST and PATCH requests

- `disable_notification_management` property was added to [agreement patch](/docs/subscriptions/agreement#update-existing-agreement-request) request.
- `notications_on` property was added to [create agreement](/docs/subscriptions/agreement#create-agreement-request) request. This property will be honored **only** by MobilePay app starting from **5.0.0 version**.

#### 04 November 2020 - Invoice fields

Merchants can add [invoice](/docs/subscriptions/invoice) for susbscription payments without user's information.
Properties that are now optional: consumer_name, consumer_phone_number, consumer_address_lines.
If the fields are not filled, they are not displayed in PDF.
Can be negative: total_vat_amount, total_price_including_vat, price_per_unit, price_discount.
Up to 10 digits after the decimal seperator allowed for: quantity, price_per_unit.

#### 18 September 2020 - amount

For DK merchants [payment](/docs/subscriptions/subscriptions-payments#request-parameters) amount limit is 60000. If the customer is identified via NemID or picture ID (drivers license, passport and etc) then the monthly payment limit for Subscriptions is 60.000 kr.
For example: If all payment requests share the same DueDate, and thereby exceed the normal payment limit of 15.000 kr.,   the customer can still pay all their Subscription payments, as long as the total amount does not exceed 60.000 kr. on a monthly basis.
If the customer is only identified via CPR-number, then Subscription payments count as a part of the daily payments to stores, and the daily payment limit is therefore 3.000 kr.

#### 14 September 2020 - amount

For FI merchants [payment](/docs/subscriptions/subscriptions-payments#request-parameters) amount limit is 2000.

#### 26 August 2020 - frequency

Default `frequency` for agreement was changed from 12 to 0.

#### 20 August 2020 - payment-due-date

Maximum `payment-due-date` was increased from 32 days to 126 days for [subscription](/docs/subscriptions/subscriptions-payments#frequency-of-payment-requests) payment requests.

#### 12 August 2020 - expiration_timeout_minutes

Maximum `expiration_timeout_minutes` was increased from 2 weeks (20160 minutes) to 18 weeks (181440 minutes) for both [agreements](/docs/subscriptions/subscriptions-payments#frequency-of-payment-requests) and [one-off](/docs/subscriptions/one-off-payments#flow-3---one-off-with-auto-reserve) payment requests as well as [one-off with agreement](/docs/subscriptions/one-off-payments#flow-1--one-off-payment-with-a-new-agreement) payment requests.

#### 28 July 2020 - external_id

Due to restrictions in external systems we added recommendation to keep `external_id` up to 30 symbols for [subscription](/docs/subscriptions/subscriptions-payments#request-parameters) and [one-off](/docs/subscriptions/one-off-payments#flow-3---one-off-with-auto-reserve) payment requests.

#### 09 July 2020 - payment_transaction_id

We received feature request to include payment_transaction_id for all payments: recurring; one-off; refund. By including the payment_transaction_id, It is easier to conduct reconciliation through the Transaction Reporting API. The payment_transaction_id  is visible on the receipt screen. Note, in the technical documentation it is called payment_transaction_id in all API responses with additional property.

Note: this is not a breaking change.

#### 10 June 2020 - `cancel-redirect`

The feature to attach `cancel-redirect` url to an agreement has been released. If this url is set, users, who want to cancel their agreement, will be redirected to your defined link only if they use MobilePay app version **4.22 or higher**.

#### 25 May 2020

- Addded support for agreement cancelation redirect Url. For new agreements, use endpoint `POST /api/providers/{providerId}/agreements` with `cancel-redirect` link. A new link allows agreement to be cancelled in merchant own environmnet. Merchant should ensure easy access to information and support. By making it possible for customers to cancel the agreement in merchant own environment, you can get more control of your possible leaving customers. If `cancel-redirect` is used, then MobilePay redirects customer to merchant environment, and thus making Canceling funcionality not available for the user in the app.  MobilePay validates the link, as it should be https:// and not http://. The `cancel-redirect` is not mandatory, and merchant can only use `cancel-redirect` if they have a self-service environment.

- Currently feature is available to test in Sandbox and in Production.

##### Sample create agreement request

```json
{
  "external_id": "AGGR00068",
  "amount": "10",
  "currency": "DKK",
  "description": "Monthly subscription",
  "frequency": 12,
  "links": [
    {
      "rel": "user-redirect",
      "href": "https://example.com/1b08e244-4aea-4988-99d6-1bd22c6a5b2c"
    },
    {
      "rel": "success-callback",
      "href": "https://example.com/1b08e244-4aea-4988-99d6-1bd22c6a5b2c"
    },
    {
      "rel": "cancel-callback",
      "href": "https://example.com/1b08e244-4aea-4988-99d6-1bd22c6a5b2c"
    },
        {
      "rel": "cancel-redirect",
      "href": "https://example.com/1b08e244-4aea-4988-99d6-1bd22c6a5b2c"
    }
  ],
  "country_code": "DK",
  "plan": "Basic",
  "expiration_timeout_minutes": 5,
  "mobile_phone_number": "4511100118",
  "retention_period_hours": 0,
  "disable_notification_management": false,
}
```

In order to updated existing agreements use `PATCH /api/providers/{providerId}/{agreementId}` endpoint with payload:

```json
[
    {
        "value": "https://example.com/1b08e244-4aea-4988-99d6-1bd22c6a5b2c",
        "path": "/cancel-redirect",
        "op": "replace"
    }
]
```

#### 09 Apr 2020

- Added ability to set `expiration_timeout_minutes` parameter for one-off payments. It can be done when requesting one-off payment or when requesting agreement with one-off payment. It is optional to `expiration_timeout_minutes`. Min: 1, max: 20160 (2 weeks), default: 1440 (24 hours)

#### 27 Feb 2020

- Increased length of `external_id` for Subscriptions Payments. Maximum length is 64 characters  

#### 24 Feb 2020

- Updated `GET /api/providers/{providerId}/agreements` endpoint documentation. Removing obsolete **paginationState** argument and replacing with **pageNumber**.  We recommend you always explicitly set the **pageSize** to ensure you know how many results per page you'll get.

## 2019

#### 2 Jul 2019

- New parameter added into payment request - `grace_period_days` which lets merchants to configure how many days we will try to complete unsuccessful payment. More information can be found [here](/docs/subscriptions/subscriptions-payments).

#### 30 May 2019

- New Refund callback Status Code introduced - **60007**. This allows to better inform merchants abount Refund limitations for instant transfer payments. An updated Status Code table can be found [here](/docs/subscriptions/refund#callbacks).

#### 14 May 2019

New Agreement parameters introduced for Merchants:

- Agreement `disable_notification_management` push notification. Merchant can set if their customer should be able to manage push notifications for an agreement or not. If the merchant choses so, then the push notification is not displayed when signing new agreement and when browsing agreement information. This parameter is not required, and the default value is 'false' [See more](/docs/subscriptions/agreement#request-parameters-for-create-agreement-request)
  ![Disable notifications](/img/subs-Disable_notification_management1.png)
  
- Agreement frequency. We are now able to handle more agreement frequency parameters. Merchant can set new frequency: *daily*, *weekly*, or *flexible*. Flexible is also known as on demand  [See more](/docs/subscriptions/agreement#request-parameters-for-create-agreement-request).
  ![Flexible payments](/img/subs-Flexiblepayments.png)
  
- Agreement `retention_period_hours` Merchant can set for how long agreement can't be Cancelled by the user, after the user accepted the agreement, for up to 24 hours. This is an advantage in relation to street sales and when/if merchants offer cheaper prices, if the customer establishes a subscription agreement with the merchant. Before retention period has passed, then the cusomer will not be able to cancel an agreement
  ![Delete agreement](/img/subs-DeleteAgreement.png)

- Subscription payment 8 days rule validation on payment creation is changed to 1 day. The merchant can send a payment max 32 days prior due date, and at least 1 day before due date. Valid values are 1, 2, 4, 12, 26, 52, 365, 0. This means that the daily payment (365) is the most frequent. When you are requesting a payment, you need to keep the 1 day rule. [See more](/docs/subscriptions/subscriptions-payments#frequency-of-payment-requests).

- Merchants also has the possibility to notify end users about “future payments” from 8 days to 1 day before due date.  On due date all end users receive a receipt for the payment

- One-off payment without confirmation. Merchant can send one-off payment, which MobilePay will attempt to automatically reserve, without user's confirmation. One-off without swipe omits the MobilePay landing page and is instantly executed. Existing functionality of one-off with confirmation will still be available. It is valid for One-offs without new agreements. Updated request can be found [here](/docs/subscriptions/one-off-payments#flow-2---one-off-payment-on-an-existing-agreement).

New functionality will be available for all users from APP version 4.12.0.

We have deprecated Subscriptions (Mutual SSL) 2.0.11.We are not going to release new functionality to those, who are using Mutual SSL. The features are available for those, who have integrated using OpenID Connect

#### 16 January 2019

[Add invoice details to subscription payment.](/docs/subscriptions/invoice)
Invoices are now available for subscription payments.
Merchants can send details, which we will use to generate a PDF and show it to customers in the app. This makes easy for merchants to have invoices available to customers. For technical questions about integrating via OpenID Connect, refer to the Integration docs on the Developer Portal [Here](/docs/subscriptions/authentication). The deadline for migrating to OpenID Connect is 01-01-2020

## 2018

#### 23 August 2018

We are excited to announce **Subscriptions Integrator 1.1** that is already available in Sandbox.

ETA in production is **December 2018**.
