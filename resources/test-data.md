---
title: Test Data
estimated_read: 30
description: |
  Testing, are we? Good! Here's some data you can
  use to test and verify your integration!
---

## Swedbank Pay Checkout Test Data

During a Swedbank Pay Checkout implementation you can use the test data related
to the different payment instruments listed below. To see Swedbank Pay Checkout
in action, please visit our [demoshop]({{ page.front_end_url }}/pspdemoshop)

To test a checked in user in the Demo Shop, please use the following test data:

### Checkout test data for Norway

{:.table .table-striped}
| Type            | Data                         | Description                                                           |
| :-------------- | :--------------------------- | :-------------------------------------------------------------------- |
| `Email`         | `olivia.nyhuus@payex.com`    | The e-mail address of the payer.                                      |
| `Mobile number` | `+47 98765432`               | The mobile phone number of the payer. Format Norway: `+47 99999999`.  |
| `SSN`           | `{{ page.consumer_ssn_no }}` | The social security number of the payer. Format Norway: `DDMMYYXXXXX` |
| `ZipCode`       | `1642`                       | The city zip code. Format Norway: `XXXX`                              |

### Checkout test data for Sweden

{:.table .table-striped}
| Type            | Data                         | Description                                                             |
| :-------------- | :--------------------------- | :---------------------------------------------------------------------- |
| `Email`         | `leia.ahlstrom@payex.com`    | The e-mail address of the payer.                                        |
| `Mobile number` | `+46 739000001`              | The mobile phone number of the payer. Format Sweden: `+46 707777777`.   |
| `SSN`           | `{{ page.consumer_ssn_se }}` | The social security number of the payer. Format Sweden: `YYYYMMDDXXXX`. |
| `ZipCode`       | `17674`                      | The city zip code. Format Sweden: `XXXXX`                               |

### Checkout test data for Denmark

{:.table .table-striped}
| Type            | Data          | Description                                                          |
| :-------------- | :------------ | :------------------------------------------------------------------- |
| `Mobile number` | `+4522222222` | The mobile phone number of the payer. Format Denmark: `+45 22222222` |

## Credit Card Test Data

### Visa

{:.table .table-striped}
| Card number        | Expiry                  | CVC  |
| :----------------- | :---------------------- | :--- |
| `4925000000000004` | After the current month | Any  |
| `4581097032723517` | After the current month | Any  |
| `4581099940323133` | After the current month | Any  |

### MasterCard

{:.table .table-striped}
| Card number        | Expiry                  | CVC  |
| :----------------- | :---------------------- | :--- |
| `5226600159865967` | After the current month | Any  |
| `5226603115488031` | After the current month | Any  |
| `5226604266737382` | After the current month | Any  |
| `5226600156995650` | After the current month | Any  |

### American Express

{:.table .table-striped}
| Card number       | Expiry                  | CVC    | Type of test data |
| :---------------- | :---------------------- | :----- | :---------------- |
| `377601000000000` | After the current month | `5252` | Amex & loopback   |

### JCB

{:.table .table-striped}
| Card number        | Expiry                  | CVC   |
| :----------------- | :---------------------- | :---- |
| `3569990010082211` | After the current month | `123` |

### Diners

{:.table .table-striped}
| Card number     | Expiry                  | CVC   |
| :-------------- | :---------------------- | :---- |
| `6148201829798` | After the current month | `832` |

### Maestro

{:.table .table-striped}
| Card number        | Expiry | CVC   |
| :----------------- | :----- | :---- |
| `6764429999947470` | 03/17  | `066` |

### Dankort

{:.table .table-striped}
| Card number        | Expiry | CVC   |
| :----------------- | :----- | :---- |
| `5019994016316467` | 10/23  | `375` |
| `5019994001307083` | 05/21  | `615` |

### Visa/DanKort

{:.table .table-striped}
| Card number        | Expiry | CVC   |
| :----------------- | :----- | :---- |
| `4571994016401817` | 10/17  | `212` |
| `4571994016471869` | 01/19  | `829` |

### Forbrugsforeningen

{:.table .table-striped}
| Card number        | Expiry | CVC   |
| :----------------- | :----- | :---- |
| `6007220000000004` | 12/22  | `123` |

## Failure Testing

There are two different ways of testing Card Payments error scenarios. You can
test 3-D Secure errors using our 3-D Secure emulator, or you can use specific
amounts set to trigger errors in our test environment.

### 3-D Secure Method

First, [create a Card Payment][create-card-purchase] (operation `Purchase`) and
visit the URL of the returned `redirect-authorization` operation in a web
browser. Use either the Visa or MasterCard shown below.

{:.table .table-striped}
| Card type  | Card number        | Expiry | CVC   | Type of test data   |
| :--------- | :----------------- | :----- | :---- | :------------------ |
| Visa       | `4761739001010416` | 12/22  | `268` | 3-D Secure enrolled |
| MasterCard | `5226612199533406` | 09/28  | `602` | 3-D Secure enrolled |

After pressing the purchase button you will then be taken to a menu where you
can select Authentication status.

![3D-Secure Emulator without dropdown menu][3ds-emulator-no-dropdown]{:width="805px" :height="685px"}

![3D-Secure Emulator with dropdown menu][3ds-emulator-with-dropdown]{:width="805px" :height="685px"}

In this menu there are a few different options to choose from, choose the status
you want to test. When selected, simply press the Continue button and the
status you selected will be sent with the payment.

### Amount Error Testing Method

We have some preset amounts that will trigger error codes. When creating a
payment (operation `purchase`), enter one of the amounts from the list below in
the prices object (`"amount": <number>`) before submitting a payment. The error
message displayed behind the amounts will be sent with your payment in the test
environment.

The amounts that can be used to trigger error codes
(`transactionThirdPartyError`):

{:.table .table-striped}
| Amount   | Error Code                                | Description                              |
| :------- | :---------------------------------------- | :--------------------------------------- |
| `900313` | `REJECTED_BY_ACQUIRER_INVALID_AMOUNT`     | Invalid amount, response-code: 13        |
| `900330` | `REJECTED_BY_ACQUIRER_FORMAT_ERROR`       | Format error, response-code: 30          |
| `900334` | `REJECTED_BY_ACQUIRER_POSSIBLE_FRAUD`     | Possible fraud, response-code: 34        |
| `900343` | `REJECTED_BY_ACQUIRER_CARD_STOLEN`        | Card stolen, response-code: 43           |
| `900354` | `REJECTED_BY_ACQUIRER_CARD_EXPIRED`       | Card expired, response-code: 54          |
| `900351` | `REJECTED_BY_ACQUIRER`                    | Unknown error, response-code: 51         |
| `900359` | `REJECTED_BY_ACQUIRER_POSSIBLE_FRAUD`     | Possible fraud, response-code: 59        |
| `900361` | `REJECTED_BY_ACQUIRER_INSUFFICIENT_FUNDS` | Insufficient funds, response-code: 61    |
| `900362` | `REJECTED_BY_ACQUIRER`                    | Unknown error, response-code: 62         |
| `900391` | `ACQUIRER_HOST_OFFLINE`                   | Acquirer host offline, response-code: 91 |

## Invoice Test Data

### Invoice test data for Norway

{:.table .table-striped}
| Type    | Data             |
| :------ | :--------------- |
| SSN     | 26026708248      |
| Name    | Olivia Nyhuus    |
| Address | Saltnestoppen 43 |
| City    | 1642 Saltnes     |

### Invoice test data for Sweden

{:.table .table-striped}
| Type    | Data            | Alternative data        |
| :------ | :-------------- | :---------------------- |
| SSN     | 600307-1161     | 971020-2392             |
| Name    | Azra Oliveira   | Leia Ahlström           |
| Address | Helgestavägen 9 | Hökvägen 5              |
| City    | 19792 Bro       | 17674 Järfälla          |
| MSISDN  |                 | +46739000001            |
| email   |                 | leia.ahlstrom@payex.com |

### Invoice test data for Finland

{:.table .table-striped}
| Type    | Data             |
| :------ | :--------------- |
| SSN     | 100584-451P      |
| Name    | Järvilehto Kimmo |
| Address | Kiannonkatu 88   |
| City    | 90500 Oulu       |

## Invoice Service Test Data

Use any name, address etc.

## Vipps Test Data

Testing a successful Vipps purchase (in our external integration test
environment) can be done using any valid Norwegian mobile number, E.g:
`+47 99999999` except within the range: `9999991` - `99999998`, as these will
trigger errors according to the table below. Please note that the external
integration test environment is usinga fake service, which means that no app
will be involved.

{:.table .table-striped}
| Mobile number | Error message                                                   |
| :------------ | :-------------------------------------------------------------- |
| 99999991      | Vipps internal error                                            |
| 99999992      | Request Validation error message on paticular request parameter |
| 99999993      | Transaction Id already exists in vipps                          |
| 99999994      | PSPID not enrolled in vipps                                     |
| 99999995      | Invalid payment model type                                      |
| 99999996      | User Vipps App version not supported                            |
| 99999997      | User not Registered with Vipps                                  |
| 99999998      | Merchant not available or active                                |

## Swish Test Data

Testing a successful Swish purchase (in our external integration test
environment) can be done by using any valid Swedish mobile number. E.g:
`+46 739000001`. As with Vipps, the external integration test environment uses a
fake service with no app involved. To trigger an error message, set the
`description` value in `POST` Create Payment or `Create` Payment Order to one of
the following values:

{:.table .table-striped}
| Description | Simulates                                      |
| :---------- | :--------------------------------------------- |
| RF07        | Transaction declined                           |
| TM01        | Swish timed out before the payment was started |
| BANKIDCL    | Payer cancelled BankId signing                 |

[create-card-purchase]: /payments/card/redirect#step-1-create-a-purchase
[3ds-emulator-no-dropdown]: /assets/img/3DS-emulator-no-dropdown.png
[3ds-emulator-with-dropdown]: /assets/img/3DS-emulator-with-dropdown.png
