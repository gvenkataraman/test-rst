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
        "card_uri": "/v1/marketplaces/TEST-MP10Kkd3SnuHLM2aXhDAG0eg/cards/CC215811c4222311e2988680ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T16:48:26.693306Z",  
        "uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/transactions",  
        "email_address": "b@m.com",  
        "id": "AC12t14kAycgzY0U3Nb8H82w",  
        "credits_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP12d3qav2UH9iaQm1ejk48Q/accounts/AC12t14kAycgzY0U3Nb8H82w/cards" 
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
                "tax_id": "082007300" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "484233600" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T16:48:29.473674Z",  
        "uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/transactions",  
        "email_address": null,  
        "id": "AC15AUoyMvsaAg1GDPpA3iba",  
        "credits_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP15nlTqs8aJODtj3Qhc1uny/accounts/AC15AUoyMvsaAg1GDPpA3iba/cards" 
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
            "tax_id": "375661400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T16:48:32.113744Z",  
        "uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/transactions",  
        "email_address": null,  
        "id": "AC18yZSoFTaj3PjF2gwvhm6g",  
        "credits_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP18ltJT6e2rsBpcRZ1I3rr6/accounts/AC18yZSoFTaj3PjF2gwvhm6g/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T16:48:33.440729Z",  
        "uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC1a3xg8RwMWvUzbHmrIqBSc",  
        "credits_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP19QTZe7qCgAKKayTmYXbWA/accounts/AC1a3xg8RwMWvUzbHmrIqBSc/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.711939Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC1buc1ETZxD7UkmW9GtHSNm",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1buc1ETZxD7UkmW9GtHSNm/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.712754Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC1bug8jemJ94EKRJMDuIJ1O",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bug8jemJ94EKRJMDuIJ1O/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.735245Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC1bvP9qaInsQvRoSpFsyBww",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bvP9qaInsQvRoSpFsyBww/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.570653Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC1bkjvv990Na4pp5zis0dq4",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bkjvv990Na4pp5zis0dq4/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.629512Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC1borfEcz3v7t2HeVn2GqvG",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1borfEcz3v7t2HeVn2GqvG/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.630638Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC1bowuNp8p3A4UThRgquE4Y",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1bowuNp8p3A4UThRgquE4Y/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T16:48:34.668650Z",  
                "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC1braz8XT6lqGkCdbVQX0QA",  
                "credits_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts/AC1braz8XT6lqGkCdbVQX0QA/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1biWPpFvaJm16QeZ4EodU0/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP1cQpSdjXMk8TLcHAzncOSU/cards/CC27c13c52222311e28d1880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T16:48:37.406519Z",  
        "uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/transactions",  
        "email_address": "new@email.com",  
        "id": "AC1ew53ivPjhcB423cmnby3G",  
        "credits_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1eiGFpkwh9JIZFW80LkXoU/accounts/AC1ew53ivPjhcB423cmnby3G/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

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
            "tax_id": "013537600" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T16:48:40.082628Z",  
        "uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC1hwHzTCagQvMTXOnLIn39y",  
        "credits_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1hn9WYhFRFMBRmHJbDZsEY/accounts/AC1hwHzTCagQvMTXOnLIn39y/cards" 
    } 
 

