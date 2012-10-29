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
        "card_uri": "/v1/marketplaces/TEST-MP4W2RyqKxfI18M7EUorjkEI/cards/CCa246650021f711e287ea80ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:37:05.103414Z",  
        "uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/transactions",  
        "email_address": "b@m.com",  
        "id": "AC4XHSfsSxxHKdJ4zlEpm0rq",  
        "credits_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4XtaBMHmQqBy5BLtRWazu4/accounts/AC4XHSfsSxxHKdJ4zlEpm0rq/cards" 
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
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
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
                "tax_id": "664475800" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "024712100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T11:37:07.799341Z",  
        "uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/transactions",  
        "email_address": null,  
        "id": "AC50JSXqYooft1Kz3lll5Ul6",  
        "credits_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP50weRYw9fXkxYt6vewT2sI/accounts/AC50JSXqYooft1Kz3lll5Ul6/cards" 
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
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
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
            "tax_id": "502270800" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T11:37:10.372940Z",  
        "uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/transactions",  
        "email_address": null,  
        "id": "AC53DlnCgNGOMHjNGhrjWHhW",  
        "credits_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP53qYHKZEeoldjtaDIx3U0I/accounts/AC53DlnCgNGOMHjNGhrjWHhW/cards" 
    } 
 

Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request 
~~~~~~~ 
 
Body 
^^^^ 
 
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
        "holds_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:37:11.627982Z",  
        "uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC552RcnHTOumORRP8q1YTFa",  
        "credits_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP54QGXaTLZO1Oq2wDggx7Pm/accounts/AC552RcnHTOumORRP8q1YTFa/cards" 
    } 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request 
~~~~~~~ 
 
Body 
^^^^ 
 
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
        "first_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.848066Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/transactions",  
                "email_address": "email.10@y.com",  
                "id": "AC56pWt076QrSSLhLMrrtAEs",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56pWt076QrSSLhLMrrtAEs/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.849337Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC56q1Dkay3iNuhjjuxNXGXW",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56q1Dkay3iNuhjjuxNXGXW/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.882223Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/transactions",  
                "email_address": "email.13@y.com",  
                "id": "AC56sjFWqKsSTzmYfAsUiBw0",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56sjFWqKsSTzmYfAsUiBw0/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.700631Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC56fEgBKVZOV8QpJN8mHj92",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56fEgBKVZOV8QpJN8mHj92/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.772800Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC56kGZ9RfUxqxtXsxX9tQZC",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kGZ9RfUxqxtXsxX9tQZC/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:37:12.773977Z",  
                "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC56kMcqJ3jBaVrjcrVAdH4E",  
                "credits_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts/AC56kMcqJ3jBaVrjcrVAdH4E/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP56emxaKwDhYlnJl7BHu5o0/accounts?limit=10&offset=0" 
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
    *optional* **object** or **null**. See `Create a Card <./bank_accounts.rst#create-a-card>`_. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. Tokenized bank account URI. 
 
``bank_account`` 
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 

Body 
^^^^ 
 

Response
~~~~~~~~

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**.  
 
``merchant`` 
    *optional* **object** or **null**. See `Create a Business Merchant <./bank_accounts.rst#create-a-business-merchant>`_ or `Create a Person Merchant <./bank_accounts.rst#create-a-person-merchant>`_. 
 
 

Body 
^^^^ 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:37:16.753380Z",  
        "uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC5aOhr32tnMjfIRCXD6ojmA",  
        "credits_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5aDAc5JBAGRdbVkvGgjI2M/accounts/AC5aOhr32tnMjfIRCXD6ojmA/cards" 
    } 
 

