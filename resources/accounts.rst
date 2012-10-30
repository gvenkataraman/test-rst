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
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
        "card_uri": "/v1/marketplaces/TEST-MP4fVlk41nwrPPo73o5Eg99i/cards/CC8bf8f3e022b411e2a38880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T10:09:22.545239Z",  
        "uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/transactions",  
        "email_address": "b@m.com",  
        "id": "AC4hB5udg2BhwHjuzoW2KvIM",  
        "credits_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4hmEZ5Xl2faQRMrD3o8b88/accounts/AC4hB5udg2BhwHjuzoW2KvIM/cards" 
    } 
 

Create a Business Merchant
--------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
                "tax_id": "141626300" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "837224700" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T10:09:25.263342Z",  
        "uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/transactions",  
        "email_address": null,  
        "id": "AC4kECdx7GH6p8xEQUgLtl7S",  
        "credits_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4krqC0zuVT0LDzdtxM1iyE/accounts/AC4kECdx7GH6p8xEQUgLtl7S/cards" 
    } 
 

Create a Person Merchant
------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
            "tax_id": "632552000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T10:09:27.853684Z",  
        "uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/transactions",  
        "email_address": null,  
        "id": "AC4nzfnI1SpLTGVCeiq7bfUw",  
        "credits_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4njSMuFgvt4EqjHGOJyer2/accounts/AC4nzfnI1SpLTGVCeiq7bfUw/cards" 
    } 
 

Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T10:09:29.103699Z",  
        "uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC4oYq1yatexevoc0tlbl7TK",  
        "credits_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4oLWhqlyGYtaeO5sDhOHD6/accounts/AC4oYq1yatexevoc0tlbl7TK/cards" 
    } 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.205929Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC4qdeYpyM0UZ0oYtvZikTWY",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qdeYpyM0UZ0oYtvZikTWY/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.282127Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC4qiBcpUFMmYw0jLmkLMMn2",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiBcpUFMmYw0jLmkLMMn2/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.283261Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC4qiGfvfpMaz6Z5yeKBhHNO",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qiGfvfpMaz6Z5yeKBhHNO/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.323576Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC4qltZuaqHc4SoqhBp4shx2",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qltZuaqHc4SoqhBp4shx2/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.379626Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC4qpoByqDPPZKfGGONrMpSY",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qpoByqDPPZKfGGONrMpSY/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.380800Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC4qptUIV9DjpH5GP6w11Jv6",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qptUIV9DjpH5GP6w11Jv6/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T10:09:30.413292Z",  
                "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC4qrKaU27WAXqdH7FebuDkg",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts/AC4qrKaU27WAXqdH7FebuDkg/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4qbgip74RrRGX8vVYFU6FK/accounts?limit=10&offset=0" 
    } 
 

Update an Account
-----------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

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
        "card_uri": "/v1/marketplaces/TEST-MP4rKpMPEwXvM5erw0XbSOZm/cards/CC92385f2022b411e295fc80ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T10:09:33.022532Z",  
        "uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/transactions",  
        "email_address": "new@email.com",  
        "id": "AC4tnHt12d7RhvvNrf6UpKCw",  
        "credits_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4tb1ooZnTTC8OGaLzpg7vS/accounts/AC4tnHt12d7RhvvNrf6UpKCw/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**. See `Merchant <./merchants.rst>`_. 
 
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
            "tax_id": "755015800" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-30T10:09:35.612429Z",  
        "uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC4wihNSVipFQvRCHNyoJ4zy",  
        "credits_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4w7jy8HrPfZqWqqFmPFdUo/accounts/AC4wihNSVipFQvRCHNyoJ4zy/cards" 
    } 
 

