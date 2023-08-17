# Sadad PHP - Library

Sadad Pay library is a PHP library to integrate Sadad payment APIs with PHP plugins, modules, e-commerce and websites.

## License

The GPL-3.0-only License.


## Install

You can install/require it via Composer

``` bash
composer require sadad/library
```

## How to use it ..

### Create refresh Token

``` php
$sadadConfig = array(
	'clientId'     => '',
	'clientSecret' => '',
	'isTest'       => true, // true for test mode | false for live mode
);

$sadadObj = new SadadLibrary( $sadadConfig );
$sadadObj->generateRefreshToken();

echo "Save the refresh Token ".$sadadObj->refreshToken. " into a secure place.";

```
### Create an invoice

``` php

$invoice = array(
	'ref_Number'        => "order #110092",
	'amount'            => SadadLibrary::getKWDAmount( 'USD', 40 ),
	'customer_Name'     => "fname lname",
	'customer_Mobile'   => SadadLibrary::validatePhone( '+966987654321' ),
	'customer_Email'    => "email@email.com",
	'currency_Code'     => 'USD'
);

$request = array( 'Invoices' => array( $invoice ) );

$sadadInvoice = $sadadObj->createInvoice( $request, $sadadObj->refreshToken );

$invoiceURL = $sadadInvoice['InvoiceURL'];

echo "Pay Sadad Invoice <a href='$invoiceURL' target='_blank'>$invoiceURL</a>.";

```

### Get invoice information

``` php

$invoiceInfo = $sadadObj->getInvoiceInfo( $sadadInvoice['InvoiceId'], $sadadObj->refreshToken );

echo "Sadad Invoice information <pre/>";
print_r($invoiceInfo);

```

## Credits

- [Sadad Plugin Team](https://github.com/sadad-pay)

