Accounts
========

- `Create a Buyer`_
- `Create a Person Merchant`_
- `Create a Business Merchant`_
- `Retrieve an Account`_
- `List all Accounts`_
- `Update an Account`_
- `Promote a Buyer Account to a Merchant`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the account. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    account was created. 
 
``name`` 
    **string**. The name of the account. 
 
``email_address`` 
    **string**. The email address of the account. 
 
``roles`` 
    **list**. A list of roles the account has. Can be zero, one, or both of 
    ``buyer``, ``merchant`` 
 
``debits_uri`` 
    **string**. URI for all debits associated with the account. 
 
``credits_uri`` 
    **string**. URI for all credits associated with the account. 
 
``refunds_uri`` 
    **string**. URI for all refunds associated with the account. 
 
``holds_uri`` 
    **string**. URI for all holds associated with the account. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``transactions_uri`` 
    **string**. URI for all transactions associated with the account. 
 
``bank_accounts_uri`` 
    **string**. URI for all bank accounts associated with the account. 
 
``cards_uri`` 
    **string**. URI for all cards associated with the account. 
 

Create a Buyer
--------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``card_uri`` 
    *optional* **string** or **null**. The URI of the tokenized card. 
 
``card`` 
    *optional* **object** or **null**. See `Create a Card <./cards.rst#create-a-card>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MP13YP423QERatE2klo7ltnS/cards/CC230ad60821fd11e287ea80ee7316ae44",  
        "email_address": "b@m.com",  
        "name": "Benny Riemann" 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 201 CREATED 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:16:28.580714Z",  
        "uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/transactions",  
        "email_address": "b@m.com",  
        "id": "AC15zI0Ew2ldpims2MipHrZq",  
        "credits_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP15oLl0XbWpHFnmFPQWTYQk/accounts/AC15zI0Ew2ldpims2MipHrZq/cards" 
    } 
 

Create a Business Merchant
--------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. The URI of the bank account created via *balanced.js*. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 
``merchant_uri`` 
    *optional* **string** or **null**. The URI of the merchant account created during a request for more 
    information. 
 
``merchant`` 
    *optional* **object** or **null**.  
        ``type`` 
            *required* **string** or **null**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string** or **null**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
        ``person`` 
            *optional* **object** or **null**.  
                ``name`` 
                    *required* **string** or **null**.  
 
                ``dob`` 
                    *required* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
                ``city`` 
                    *optional* **string** or **null**. City. 
 
                ``postal_code`` 
                    *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
                    *requires* ``country_code``. 
 
                ``street_address`` 
                    *required* **string** or **null**. Street address. 
                    *requires* ``postal_code``. 
 
                ``country_code`` 
                    *optional* **string** or **null**. `ISO-3166-3 
                    <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
                    three character country code. 
 
                ``tax_id`` 
                    *optional* **string** or **null**. Length must be **=** ``9``. 
 
 
        ``name`` 
            *optional* **string** or **null**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean** or **null**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string** or **null**. City. 
 
        ``postal_code`` 
            *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
            *requires* ``country_code``. 
 
        ``street_address`` 
            *required* **string** or **null**. Street address. 
            *requires* ``postal_code``. 
 
        ``country_code`` 
            *optional* **string** or **null**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "person": { 
                "city": "San Francisco",  
                "state": "CA",  
                "postal_code": "94110",  
                "name": "jo",  
                "dob": "1984-01",  
                "street_address": "Somewhere over the rainbow",  
                "tax_id": "605073500" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "132874300" 
        } 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 201 CREATED 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:16:31.335254Z",  
        "uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/transactions",  
        "email_address": null,  
        "id": "AC18FMkvCyFnXoGwFZgimeR6",  
        "credits_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP18tgztd1BpZGuYBLYoZs68/accounts/AC18FMkvCyFnXoGwFZgimeR6/cards" 
    } 
 

Create a Person Merchant
------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. The URI of the bank account created via *balanced.js*. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 
``merchant_uri`` 
    *optional* **string** or **null**. The URI of the merchant account created during a request for more 
    information. 
 
``merchant`` 
    *optional* **object** or **null**.  
        ``type`` 
            *required* **string** or **null**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string** or **null**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
        ``name`` 
            *optional* **string** or **null**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean** or **null**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string** or **null**. City. 
 
        ``postal_code`` 
            *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
            *requires* ``country_code``. 
 
        ``street_address`` 
            *required* **string** or **null**. Street address. 
            *requires* ``postal_code``. 
 
        ``country_code`` 
            *optional* **string** or **null**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "dob": "1984-01",  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "person",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "543543000" 
        } 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 201 CREATED 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:16:33.922398Z",  
        "uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/transactions",  
        "email_address": null,  
        "id": "AC1bAcou4jqu7EL1DbTtXjzC",  
        "credits_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1bov0NF6yxd0HOdD65ihbm/accounts/AC1bAcou4jqu7EL1DbTtXjzC/cards" 
    } 
 

Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Body 
~~~~ 
 
Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
~~~~ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:16:35.128430Z",  
        "uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC1cWiMEcRSx4NXaSFn3EIGo",  
        "credits_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1cNDvGDbX3qLxN3AA87wHi/accounts/AC1cWiMEcRSx4NXaSFn3EIGo/cards" 
    } 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Response 
~~~~~~~~ 
 
Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "first_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.228052Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC1eaXfKqP5EXVdArPheupo0",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eaXfKqP5EXVdArPheupo0/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.296191Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC1efJfcujoi4Y6Pn35HO8uw",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efJfcujoi4Y6Pn35HO8uw/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.297334Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC1efOjTxqLEQTSjZFrd56le",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1efOjTxqLEQTSjZFrd56le/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.384852Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/transactions",  
                "email_address": "email.10@y.com",  
                "id": "AC1elUuLJXQWGVuAb4bwkJJG",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elUuLJXQWGVuAb4bwkJJG/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.386021Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC1elZCWQeynmpXDWsnEs7uA",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1elZCWQeynmpXDWsnEs7uA/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:16:36.419037Z",  
                "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/transactions",  
                "email_address": "email.13@y.com",  
                "id": "AC1eoiPFH0vz9HhIXBaNmrNq",  
                "credits_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts/AC1eoiPFH0vz9HhIXBaNmrNq/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1e9t7gFLsX5YZ7FL7dCcBu/accounts?limit=10&offset=0" 
    } 
 

Update an Account
-----------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~   
 
``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. RFC-2822 formatted email address. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``card_uri`` 
    *optional* **string** or **null**. Tokenized card URI. 
 
``card`` 
    *optional* **object** or **null**. See `Card <./cards.rst>`_. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. Tokenized bank account URI. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MP1fGesjTd8ilNNPzWoOyTm4/cards/CC2942ca4421fd11e2a19c80ee7316ae44",  
        "meta": { 
            "more-data": "here" 
        },  
        "email_address": "new@email.com",  
        "name": "my new name" 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:16:39.064064Z",  
        "uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/transactions",  
        "email_address": "new@email.com",  
        "id": "AC1hmKb3lT69dXMfNHmbgPUU",  
        "credits_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1haPV6GQySzfG7w7c1HLU0/accounts/AC1hmKb3lT69dXMfNHmbgPUU/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**. See `Merchant <./merchants.rst>`. 
 
``merchant`` 
    *optional* **object** or **null**. See `Business Merchant <./accounts.rst#create-a-business-merchant>`_ or `Person Merchant <./accounts.rst#create-a-person-merchant>`_. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "dob": "1984-01",  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "person",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "504883400" 
        } 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:16:41.688210Z",  
        "uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC1kjJHDc41nL03WJYrkLQva",  
        "credits_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1k9BGLTiqUAeJ1JxJuUdfK/accounts/AC1kjJHDc41nL03WJYrkLQva/cards" 
    } 
 

