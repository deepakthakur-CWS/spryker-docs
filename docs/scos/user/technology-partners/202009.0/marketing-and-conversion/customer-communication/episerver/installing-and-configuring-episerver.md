---
title: Episerver - Installation and Configuration
description: Install and  configure  Episerver into Spryker Commerce OS
last_updated: Nov 6, 2020
template: concept-topic-template
originalLink: https://documentation.spryker.com/v6/docs/episerver-installation-and-configuration
originalArticleId: 6a9116bd-ba85-4c53-acb9-3851681ff02b
redirect_from:
  - /v6/docs/episerver-installation-and-configuration
  - /v6/docs/en/episerver-installation-and-configuration
related:
  - title: Episerver - Integration into a project
    link: docs/scos/user/technology-partners/page.version/marketing-and-conversion/customer-communication/episerver/integrating-episerver.html
  - title: Episerver - Order referenced commands
    link: docs/scos/user/technology-partners/page.version/marketing-and-conversion/customer-communication/episerver/technical-details-and-howtos/episerver-order-referenced-commands.html
  - title: Episerver - API Requests
    link: docs/scos/user/technology-partners/page.version/marketing-and-conversion/customer-communication/episerver/technical-details-and-howtos/episerver-api-requests.html
---

## Installation

To install Episerver, run the command in the console:
```php
composer require spryker-eco/episerver
```

## Configuration

To set up the Episerver initial configuration, use the credentials received from your Episerver admin page.

The `REQUEST_BASE_URL` parameter should be: `https://api.campaign.episerver.net/`

To get `ORDER_LIST_AUTHORIZATION_CODE` or `CUSTOMER_LIST_AUTHORIZATION_CODE`, go to:

<i>Menu → API overview → SOAP API → Recipient lists → (Click one of your lists here) → Manage authorization codes → Authorization code</i>

To get any `...MAILING_ID`, go to:

<b>Menu → Transactional mails → ID</b>

```php
$config[EpiserverConstants::REQUEST_BASE_URL] = 'https://api.campaign.episerver.net/';
$config[EpiserverConstants::REQUEST_TIMEOUT] = 30;

$config[EpiserverConstants::ORDER_LIST_AUTHORIZATION_CODE] = 'QJd9U0M9xssRGhnJrNr5ztt9FQa2x1wA';
$config[EpiserverConstants::CUSTOMER_LIST_AUTHORIZATION_CODE] = 'QJd9U0M9xssRGhnJrNr5ztt9FQa2x1wA';

$config[EpiserverConstants::ORDER_NEW_MAILING_ID] = '237667360304';
$config[EpiserverConstants::ORDER_CANCELLED_MAILING_ID] = '237667360304';
$config[EpiserverConstants::ORDER_SHIPPING_CONFIRMATION_MAILING_ID] = '237667360304';
$config[EpiserverConstants::ORDER_PAYMENT_IS_NOT_RECEIVED_MAILING_ID] = '237667360304';

$config[EpiserverConstants::EPISERVER_CONFIGURATION_MAILING_ID_LIST] = [
 CustomerRegistrationMailTypePlugin::MAIL_TYPE => '243323625271',
 CustomerRestoredPasswordConfirmationMailTypePlugin::MAIL_TYPE => '243646188958',
 CustomerRestorePasswordMailTypePlugin::MAIL_TYPE => '243646188953',
];
```
