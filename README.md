Wayfair price alert
==================

Poll an Wayfair sale page (or multiple pages) for a maximum price and send yourself an email if the price check passes.

## Installation
Clone the repository. This code was written for python 2.7, you should also have [pip](https://pip.pypa.io/en/stable/) installed. To install external dependencies:

`pip install -r requirements.txt`

## Configuration
Configuration is held in json format, `config.json` is used by default and has some configuration for reference, but a different file can be passed using the command line flags. you must set your email credentials. Required configuration:

- `email` (dictionary) - this is the configuration for the email server and credentials to use for sending out the email.
    - `smtp_url` - smtp server to use (default: smtp.gmail.com:587)
    - `user` - the email address to be used for authentication
    - `password` - the password to be used for authentication
        (if you have 2FA set up on your account, take a look at [app passwords](https://security.google.com/settings/security/apppasswords))

- `base_url` (string) - the base amazon url of the sales page, differs among the different variants of amazon.

- `xpath_selector` (string) - the xpath selector of the element holding the price in the sale page, the default is true for all amazon variants that have been tested so far (default: `//*[@id='priceblock_ourprice']`)

- `items` (array) - an array of items, each item should be an array as follows:


    `[amazon_item_id_string, price_in_integer]`


## Running the script

```
$ ./price-alert.py --help
usage: price-alert.py [-h] [-c CONFIG] 

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG, --config CONFIG
                        Configuration file path
```

If you want this to run on a regular basis use a cron job or change the loop.

when running without any arguments, the script will use `config.json` for configuration and the default polling interval of 30 seconds.

### Other sale pages/email client
The script was tested on Wayfair, so if you try running it on a different site make sure that `xpath_selector` is set correctly in the configuration json and that the price check itself is correct.
The smtp client is configured for Gmail, so be sure to change it if you're using a different one.
