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
        "card_uri": "/v1/marketplaces/TEST-MP4fV9vtujQn3nbdRCCUfTtq/cards/CC8beee46821fb11e29a2f80ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:05:05.581699Z",  
        "uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/transactions",  
        "email_address": "b@m.com",  
        "id": "AC4hwilbQtQNLZ9gtmxasqdm",  
        "credits_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4hjEvqASruTeizVaYawPdO/accounts/AC4hwilbQtQNLZ9gtmxasqdm/cards" 
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
                "tax_id": "866014100" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "743574400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:05:08.453860Z",  
        "uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/transactions",  
        "email_address": null,  
        "id": "AC4kKAj9f4h6g5Lu0Zl7kI4I",  
        "credits_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4kzQwQpDNkq5lNpedwCCPy/accounts/AC4kKAj9f4h6g5Lu0Zl7kI4I/cards" 
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
            "tax_id": "612652400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:05:11.087438Z",  
        "uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/transactions",  
        "email_address": null,  
        "id": "AC4nIdUzVRu4g4APeyLSOnHe",  
        "credits_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4nx6lIn1ZRiwG8PLCHSRVy/accounts/AC4nIdUzVRu4g4APeyLSOnHe/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:05:12.292332Z",  
        "uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC4p4gcTBernR4nETEFXjPRG",  
        "credits_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4oVK9qmdAdaPdeh95Mrawk/accounts/AC4p4gcTBernR4nETEFXjPRG/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.399396Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC4qjr67UaeUKnW3iRe7OD9q",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qjr67UaeUKnW3iRe7OD9q/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.458339Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC4qnyJiRhDuUFadaFBsO0qE",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnyJiRhDuUFadaFBsO0qE/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.459619Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC4qnEBAtHewP6a0bXNzNQb2",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qnEBAtHewP6a0bXNzNQb2/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.524495Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/transactions",  
                "email_address": "email.10@y.com",  
                "id": "AC4qsbuc6wC6Wmi10ag4hQC8",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsbuc6wC6Wmi10ag4hQC8/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.525699Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC4qsg8T5dltg2lONDJvRQHy",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qsg8T5dltg2lONDJvRQHy/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:05:13.548088Z",  
                "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/transactions",  
                "email_address": "email.13@y.com",  
                "id": "AC4qtOZ0DjTKhr5pznf2zNl2",  
                "credits_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts/AC4qtOZ0DjTKhr5pznf2zNl2/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4qi2ep43lkwomvpsTawGm8/accounts?limit=10&offset=0" 
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
    *optional* **object** or **null**. See `Card <./cards.rst#create-a-card>`_. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. Tokenized bank account URI. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MP4rQg5X2MvgMshUY3DCBUlS/cards/CC924497b821fb11e2855180ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:05:16.309895Z",  
        "uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/transactions",  
        "email_address": "new@email.com",  
        "id": "AC4tApvAR0DVjeZlDBVyYViA",  
        "credits_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4tqALYYP30vsFQ9TmD6BVy/accounts/AC4tApvAR0DVjeZlDBVyYViA/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**.  
 
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
            "tax_id": "084602300" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:05:19.082069Z",  
        "uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC4wHIPKbWR74Ytfa08idCRu",  
        "credits_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4wxnRgfqkLymsZPKi7xaAY/accounts/AC4wHIPKbWR74Ytfa08idCRu/cards" 
    } 
 

