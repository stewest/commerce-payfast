# Commerce Payfast
## drupal 8 commerce 2.x Payment Gateway Contrib Module

Integration instructions:
 you will need a working Drupal 8 with the latest version of Drupal Commerce 2 installed.

Add the following to your composer.json.
Under repositories:

    "repositories": [
        {
          "type": "package",
          "package": {
            "name": "commerce/payfast",
            "version": "2.3.0",
            "type": "drupal-module",
            "source": {
                "url": "https://github.com/stewest/commerce_payfast.git",
                "type": "git",
                "reference": "2.3.0"
            },
            "dist": {
                "url": "https://github.com/stewest/commerce_payfast/archive/2.3.0.zip",
                "type": "zip"
            }
          }
        }

Then add the Require section, with the other contrib modules:

    "require": {
        "commerce/payfast": "2.3.0",

and then under Extra / Installer Paths:

    "extra": {
      "installer-paths": {
        "web/modules/contrib/commerce/modules/{$name}": [
            "commerce/payfast"
        ],
      }
    }

*The above url depends on your module folder path:*
* root/web/modules... 
* or root/modules...

OR if you're not using composer.

* Unzip and copy the payfast folder to the ../modules/contrib/commerce/modules/ folder so that the path is ../modules/contrib/commerce/modules/payfast.

Then:
1. Log into the admin dashboard and install Commerce PayFast on the 'Extend' page.

2. Navigate to Commerce>Configuration>Payments and click on 'new payment gateway'

3. Select PayFast and configure as required.

4. Click Save.

## Securing your config

1. You may want to ignore the Payment Gateway config, by using the config ignore module https://www.drupal.org/project/config_ignore

2. You can otherwise add your config for the payment gateway via a settings.local.php file (which is not committed to version control) or an even safer ENV variable. (see https://www.npmjs.com/package/dotenv)

* Example:
From the *config/sync/commerce_payment.commerce_payment_gateway.payfast.yml*

      $config['commerce_payment.commerce_payment_gateway.payfast']['configuration'] = [
        'merchant_id' => 'YOUR_PAYFAST_MERCH_ID',
        'merchant_key' => 'YOUR_PAYFAST_MERCH_KEY',
        'passphrase' => 'YOUR_OPTIONAL_PAYFAST_PASSPHRASE',
      ];
