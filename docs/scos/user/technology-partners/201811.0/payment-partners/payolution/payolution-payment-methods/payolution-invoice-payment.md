---
title: Payolution - Invoice Payment
description: Integrate invoice payment through Payolution into the Spryker-based shop.
last_updated: May 19, 2020
template: concept-topic-template
originalLink: https://documentation.spryker.com/v1/docs/payolution-invoice
originalArticleId: a7d58767-222b-4bf9-878a-a8b748d2a423
redirect_from:
  - /v1/docs/payolution-invoice
  - /v1/docs/en/payolution-invoice
related:
  - title: Payolution - Performing Requests
    link: docs/scos/user/technology-partners/page.version/payment-partners/payolution/technical-details-and-howtos/payolution-performing-requests.html
  - title: Payolution - Workflow
    link: docs/scos/user/technology-partners/page.version/payment-partners/payolution/technical-details-and-howtos/payolution-workflow.html
  - title: Payolution - Installment Payment
    link: docs/scos/user/technology-partners/page.version/payment-partners/payolution/payolution-payment-methods/payolution-installment-payment.html
  - title: Payolution
    link: docs/scos/user/technology-partners/page.version/payment-partners/payolution/payolution.html
  - title: Payolution - Configuration
    link: docs/scos/user/technology-partners/page.version/payment-partners/payolution/payolution-installation-and-configuration.html
---

## Workflow Scenarios

Payments from Payolution to Merchant are not included in the sequence diagrams since they occur on a regular basis (e.g. every week).
```html
<table>
        <col>
        <col>
        <tbody>
            <tr>
                <td>
                    <h3>Standard Case</h3>
                    <p>
                        <img>

                    </p>
                </td>
                <td>
                    <h3>Full Refund Before Payment</h3>
                    <p>
                        <img>

                    </p>
                </td>
            </tr>
            <tr>
                <td>
                    <h3>Partial Refund Before Payment</h3>
                    <p>
                        <img>

                    </p>
                </td>
                <td>
                    <h3>Full Refund After Payment</h3>
                    <p>
                        <img>

                    </p>
                </td>
            </tr>
            <tr>
                <td>
                    <h3>Partial Refund After Payment</h3>
                    <p>
                        <img>

                    </p>
                </td>
                <td>&#xA0;</td>
            </tr>
        </tbody>
    </table>
```
## Integrating Payolution Invoice Payment
To integrate invoice payments, two simple steps are needed: setting Payolution invoice payment configuration and calling the facade functions.

### Setting Payolution Invoice Configuration
The configuration to integrate invoice payments using Payolution is:

* `TRANSACTION_GATEWAY_URL`: the gateway URL to connect with Payolution services (required).
* `TRANSACTION_SECURITY_SENDER `: the sender id (required).
* `TRANSACTION_USER_LOGIN`: the sender username (required).
* `TRANSACTION_USER_PASSWORD`: the sender password (required).
* `TRANSACTION_MODE`: the mode of the transaction, either test or live (required).
* `TRANSACTION_CHANNEL_PRE_CHECK`: a Payolution channel for handling pre-check requests, in case of using Pre-check (optional).
* `TRANSACTION_CHANNEL_INVOICE`: a Payolution channel for handling invoice requests except Pre-check as it has its own channel (required).
* `MIN_ORDER_GRAND_TOTAL_INVOICE`: the allowed minimum order grand total amount for invoice payments in the shop e.g. the minimum allowed payment is $2 (required).
* `MAX_ORDER_GRAND_TOTAL_INVOICE`: the allowed maximum order grand total amount for invoice payments in the shop e.g. the maximum allowed payment is $5000 (required).
* `PAYOLUTION_BCC_EMAIL_ADDRESS`: Payolution email address to send copies of payment details to Payolution.

### Performing Requests
In order to perform the needed requests, you can easily use the implemented state machine commands and conditions. See [Payolution — Performing Requests](/docs/scos/user/technology-partners/201811.0/payment-partners/payolution/payolution-performing-requests.html) for a summary. You can also use the facade methods directly which, however, are invoked by the state machine.
