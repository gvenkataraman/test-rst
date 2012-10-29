Holds
=====

- `Create a Hold`_
- `Retrieve a Hold`_
- `List all Holds`_
- `Update a Hold`_
- `Capture a Hold`_
- `Void a Hold`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    hold was created. 
 
``amount`` 
    **integer**. Amount of the hold. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this hold. 
 
``expires_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    hold was will expire and can **NO LONGER BE CAPTURED**. 
 
``description`` 
    **string**. A description of the hold, used for display purposes. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``debit`` 
    **object**. The captured debit associated with this hold. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``account`` 
    **object**. The account against which this hold was created. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``is_void`` 
    **boolean**. A boolean flag indicating if the hold has been voided or not.  
 
``source`` 
    **object**. The funding source for this hold. 
 

Create a Hold
-------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/holds 
    POST /v1/marketplaces/(marketplace:marketplace)/holds 
 

Request
~~~~~~~

``amount`` 
    *required* **integer** or **null**. Value must be >= to the minimum debit amount allowed for *your* 
    marketplace. Value must be <= to the maximum debit amount allowed for *your* 
    marketplace. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``source_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 3421,  
        "meta": { 
            "id": "#12312123123" 
        },  
        "description": "Something tasty" 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:48.976057Z",  
            "uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC2x0PKdNZXFXNe5UICCeHmk",  
            "credits_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL085-490-7636",  
        "created_at": "2012-10-29T16:49:49.050560Z",  
        "uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/holds/HL2x60QwIwdC3mPkF2TjAboo",  
        "expires_at": "2012-11-05T23:49:49.047179Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:49:48.997857Z",  
            "uri": "/v1/marketplaces/TEST-MP2wR5DqzJ9CLt3xVrCaS0As/accounts/AC2x0PKdNZXFXNe5UICCeHmk/cards/CC53386950222311e2ad8b80ee7316ae44",  
            "id": "CC53386950222311e2ad8b80ee7316ae44",  
            "card_type": "visa",  
            "is_valid": true,  
            "meta": {},  
            "country_code": "USA",  
            "postal_code": "94110",  
            "brand": "Visa",  
            "street_address": "Somewhere over the rainbow",  
            "name": "Jet Li" 
        },  
        "amount": 3421,  
        "meta": { 
            "id": "#12312123123" 
        },  
        "is_void": false,  
        "debit": null,  
        "id": "HL2x60QwIwdC3mPkF2TjAboo" 
    } 
 

Retrieve a Hold
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/holds/(hold:hold) 
    GET /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold) 
 

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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:50.605278Z",  
            "uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC2yQr5Y3u3yeATA4MIH4ojW",  
            "credits_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL888-803-6546",  
        "created_at": "2012-10-29T16:49:50.647831Z",  
        "uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/holds/HL2yToGzJ0im9YFsZ4SE56S0",  
        "expires_at": "2012-10-30T23:49:50.632122Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:49:50.629867Z",  
            "uri": "/v1/marketplaces/TEST-MP2yGbswWfhaQ9EbbQw2HD9O/accounts/AC2yQr5Y3u3yeATA4MIH4ojW/cards/CC54315696222311e2814d80ee7316ae44",  
            "id": "CC54315696222311e2814d80ee7316ae44",  
            "card_type": "visa",  
            "is_valid": true,  
            "meta": {},  
            "country_code": "USA",  
            "postal_code": "94110",  
            "brand": "Visa",  
            "street_address": "Somewhere over the rainbow",  
            "name": "Jet Li" 
        },  
        "amount": 1233,  
        "meta": {},  
        "is_void": false,  
        "debit": null,  
        "id": "HL2yToGzJ0im9YFsZ4SE56S0" 
    } 
 

List all Holds
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/holds 
    GET /v1/marketplaces/(marketplace:marketplace)/holds 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:52.084576Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL875-131-0627",  
                "created_at": "2012-10-29T16:49:52.122693Z",  
                "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/holds/HL2AyfEL3ZBtRfsRcgHktKYc",  
                "expires_at": "2012-10-30T23:49:52.106157Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:49:52.104033Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards/CC5512595c222311e28c5b80ee7316ae44",  
                    "id": "CC5512595c222311e28c5b80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "amount": 1233,  
                "meta": {},  
                "is_void": false,  
                "debit": null,  
                "id": "HL2AyfEL3ZBtRfsRcgHktKYc" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:52.084576Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL905-572-4602",  
                "created_at": "2012-10-29T16:49:52.124209Z",  
                "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/holds/HL2Aym55kIKm8C5XdppS2Kzy",  
                "expires_at": "2012-10-30T23:49:52.118348Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:49:52.104033Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards/CC5512595c222311e28c5b80ee7316ae44",  
                    "id": "CC5512595c222311e28c5b80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "amount": 3344,  
                "meta": {},  
                "is_void": false,  
                "debit": null,  
                "id": "HL2Aym55kIKm8C5XdppS2Kzy" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:52.084576Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL747-781-9697",  
                "created_at": "2012-10-29T16:49:52.125782Z",  
                "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/holds/HL2AysT06jsT6efEO56XDEji",  
                "expires_at": "2012-10-30T23:49:52.118596Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:49:52.104033Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards/CC5512595c222311e28c5b80ee7316ae44",  
                    "id": "CC5512595c222311e28c5b80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "amount": 6754,  
                "meta": {},  
                "is_void": false,  
                "debit": null,  
                "id": "HL2AysT06jsT6efEO56XDEji" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:52.084576Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC2AvBMcKFH1lLOr3Hwb2lgM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL223-955-1200",  
                "created_at": "2012-10-29T16:49:52.127149Z",  
                "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/holds/HL2AyzbypygQZO5g7OapCMTi",  
                "expires_at": "2012-10-30T23:49:52.118858Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:49:52.104033Z",  
                    "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/cards/CC5512595c222311e28c5b80ee7316ae44",  
                    "id": "CC5512595c222311e28c5b80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "amount": 1322,  
                "meta": {},  
                "is_void": false,  
                "debit": null,  
                "id": "HL2AyzbypygQZO5g7OapCMTi" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP2AmJgchudlS5dTcWlMseJC/accounts/AC2AvBMcKFH1lLOr3Hwb2lgM/holds?limit=10&offset=0" 
    } 
 

Update a Hold
-------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/holds/(hold:hold) 
    PUT /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold) 
 

Request
~~~~~~~

``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "meta": { 
            "the-address": "123 Fake Street" 
        },  
        "description": "Something really tasty" 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:55.467349Z",  
            "uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC2EjuEWSw76WgQe8bR4P3uI",  
            "credits_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL420-284-3475",  
        "created_at": "2012-10-29T16:49:55.503555Z",  
        "uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/holds/HL2Em0m4RRB2gtyuYx39jadu",  
        "expires_at": "2012-10-30T23:49:55.489682Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:49:55.487695Z",  
            "uri": "/v1/marketplaces/TEST-MP2EaJkrFMVD6rVZrDmjRKPG/accounts/AC2EjuEWSw76WgQe8bR4P3uI/cards/CC5716a29e222311e28e7280ee7316ae44",  
            "id": "CC5716a29e222311e28e7280ee7316ae44",  
            "card_type": "visa",  
            "is_valid": true,  
            "meta": {},  
            "country_code": "USA",  
            "postal_code": "94110",  
            "brand": "Visa",  
            "street_address": "Somewhere over the rainbow",  
            "name": "Jet Li" 
        },  
        "amount": 1233,  
        "meta": { 
            "the-address": "123 Fake Street" 
        },  
        "is_void": false,  
        "debit": null,  
        "id": "HL2Em0m4RRB2gtyuYx39jadu" 
    } 
 

Capture a Hold
--------------

Use ``hold_uri`` when `creating a debit <./debits.rst#create-a-debit>`_.

Request 
~~~~~~~ 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "hold_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/holds/HL2Gco5l0DCevCPA7vDRmHaI" 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:57.113221Z",  
            "uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC2GagIhadyJC6Zn7t1f4uGM",  
            "credits_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/debits/WD2GgllshjwL4GQBEhUXIOc4/refunds",  
        "created_at": "2012-10-29T16:49:57.210428Z",  
        "transaction_number": "W954-957-9869",  
        "uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/debits/WD2GgllshjwL4GQBEhUXIOc4",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:49:57.129842Z",  
            "uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/cards/CC5811633c222311e2a7e480ee7316ae44",  
            "id": "CC5811633c222311e2a7e480ee7316ae44",  
            "card_type": "visa",  
            "is_valid": true,  
            "meta": {},  
            "country_code": "USA",  
            "postal_code": "94110",  
            "brand": "Visa",  
            "street_address": "Somewhere over the rainbow",  
            "name": "Jet Li" 
        },  
        "amount": 1233,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": { 
            "fee": 30,  
            "description": "Something sour",  
            "created_at": "2012-10-29T16:49:57.143748Z",  
            "uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/holds/HL2Gco5l0DCevCPA7vDRmHaI",  
            "expires_at": "2012-10-30T23:49:57.131417Z",  
            "transaction_number": "HL744-016-0722",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM",  
            "source_uri": "/v1/marketplaces/TEST-MP2G0CPtIrYSifqnpZgvFajq/accounts/AC2GagIhadyJC6Zn7t1f4uGM/cards/CC5811633c222311e2a7e480ee7316ae44",  
            "id": "HL2Gco5l0DCevCPA7vDRmHaI" 
        },  
        "id": "WD2GgllshjwL4GQBEhUXIOc4",  
        "available_at": "2012-10-29T23:49:57.199411Z" 
    } 
 

Void a Hold
-----------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/holds/(hold:hold) 
    PUT /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold) 
 

Request
~~~~~~~

``is_void`` 
    *optional* **boolean** or **null**. Flag value, should be ``true`` or ``false``. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "is_void": true,  
        "meta": { 
            "reason": "Customer request" 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:50:00.258783Z",  
            "uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC2JHBJUCwC04O1gZt3Sop7K",  
            "credits_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL637-068-4522",  
        "created_at": "2012-10-29T16:50:00.300703Z",  
        "uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/holds/HL2JKuOp8298EXVddznjhZOI",  
        "expires_at": "2012-10-30T23:50:00.284700Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:50:00.282494Z",  
            "uri": "/v1/marketplaces/TEST-MP2JxoVvTZHy51izAZgobyug/accounts/AC2JHBJUCwC04O1gZt3Sop7K/cards/CC59f23ce4222311e2a74480ee7316ae44",  
            "id": "CC59f23ce4222311e2a74480ee7316ae44",  
            "card_type": "visa",  
            "is_valid": true,  
            "meta": {},  
            "country_code": "USA",  
            "postal_code": "94110",  
            "brand": "Visa",  
            "street_address": "Somewhere over the rainbow",  
            "name": "Jet Li" 
        },  
        "amount": 1233,  
        "meta": { 
            "reason": "Customer request" 
        },  
        "is_void": true,  
        "debit": null,  
        "id": "HL2JKuOp8298EXVddznjhZOI" 
    } 
 

