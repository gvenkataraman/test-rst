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
            "holds_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:32.258501Z",  
            "uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4OqAFVpNwnEppcfjrPemKE",  
            "credits_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL451-142-8450",  
        "created_at": "2012-10-29T15:04:32.335401Z",  
        "uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/holds/HL4OvV7e04CByFULqkB5vTnu",  
        "expires_at": "2012-11-05T22:04:32.331298Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:04:32.275544Z",  
            "uri": "/v1/marketplaces/TEST-MP4OgZSMLiJYCkunkhnyk1dW/accounts/AC4OqAFVpNwnEppcfjrPemKE/cards/CC9e292c10221411e2a16980ee7316ae44",  
            "id": "CC9e292c10221411e2a16980ee7316ae44",  
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
        "id": "HL4OvV7e04CByFULqkB5vTnu" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:33.547350Z",  
            "uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4PSsaJWhQ0sprw2Qhtrp4g",  
            "credits_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL202-719-2939",  
        "created_at": "2012-10-29T15:04:33.588855Z",  
        "uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/holds/HL4PVkZ9i1ztddudVxiaABzS",  
        "expires_at": "2012-10-30T22:04:33.573210Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:04:33.571030Z",  
            "uri": "/v1/marketplaces/TEST-MP4PJxDyg5h0fsGGzAxNIAYs/accounts/AC4PSsaJWhQ0sprw2Qhtrp4g/cards/CC9eeeaa58221411e29c7780ee7316ae44",  
            "id": "CC9eeeaa58221411e29c7780ee7316ae44",  
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
        "id": "HL4PVkZ9i1ztddudVxiaABzS" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:04:34.765827Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4RfqOalKGyerdDWgOLuSUs",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL965-692-8434",  
                "created_at": "2012-10-29T15:04:34.798587Z",  
                "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/holds/HL4RhHJmdlbNWdo5wdKCdMoY",  
                "expires_at": "2012-10-30T22:04:34.785129Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:04:34.783461Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards/CC9fa7d96a221411e2abea80ee7316ae44",  
                    "id": "CC9fa7d96a221411e2abea80ee7316ae44",  
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
                "id": "HL4RhHJmdlbNWdo5wdKCdMoY" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:04:34.765827Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4RfqOalKGyerdDWgOLuSUs",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL216-991-6599",  
                "created_at": "2012-10-29T15:04:34.799759Z",  
                "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/holds/HL4RhNlPiny5ybELFoDgLz2k",  
                "expires_at": "2012-10-30T22:04:34.794753Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:04:34.783461Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards/CC9fa7d96a221411e2abea80ee7316ae44",  
                    "id": "CC9fa7d96a221411e2abea80ee7316ae44",  
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
                "id": "HL4RhNlPiny5ybELFoDgLz2k" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:04:34.765827Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4RfqOalKGyerdDWgOLuSUs",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL642-767-3292",  
                "created_at": "2012-10-29T15:04:34.800833Z",  
                "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/holds/HL4RhSbf2UOz5qXomtDSb9UE",  
                "expires_at": "2012-10-30T22:04:34.794990Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:04:34.783461Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards/CC9fa7d96a221411e2abea80ee7316ae44",  
                    "id": "CC9fa7d96a221411e2abea80ee7316ae44",  
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
                "id": "HL4RhSbf2UOz5qXomtDSb9UE" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:04:34.765827Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4RfqOalKGyerdDWgOLuSUs",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL065-475-1225",  
                "created_at": "2012-10-29T15:04:34.802006Z",  
                "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/holds/HL4RhWRh7Amz3yFNwp3IeRlG",  
                "expires_at": "2012-10-30T22:04:34.795214Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:04:34.783461Z",  
                    "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/cards/CC9fa7d96a221411e2abea80ee7316ae44",  
                    "id": "CC9fa7d96a221411e2abea80ee7316ae44",  
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
                "id": "HL4RhWRh7Amz3yFNwp3IeRlG" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4R7t0Ko5Q90hUeMN56z41e/accounts/AC4RfqOalKGyerdDWgOLuSUs/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:37.530046Z",  
            "uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4Umb75pBJFbDFq31K0s34w",  
            "credits_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL498-746-2370",  
        "created_at": "2012-10-29T15:04:37.571813Z",  
        "uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/holds/HL4Up51A3YyOGiYJVpNyJzi4",  
        "expires_at": "2012-10-30T22:04:37.556062Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:04:37.553847Z",  
            "uri": "/v1/marketplaces/TEST-MP4UbXqxB31M2eundWiauylS/accounts/AC4Umb75pBJFbDFq31K0s34w/cards/CCa14e64aa221411e2bd1480ee7316ae44",  
            "id": "CCa14e64aa221411e2bd1480ee7316ae44",  
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
        "id": "HL4Up51A3YyOGiYJVpNyJzi4" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/holds/HL4VTFT6MxGqabzXAN1mTHjS" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:38.857699Z",  
            "uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4VQLfA5Cdny8golEUWV5o8",  
            "credits_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/debits/WD4VYmyjRVVRJJ6Iuza9MKwY/refunds",  
        "created_at": "2012-10-29T15:04:38.973711Z",  
        "transaction_number": "W116-329-9645",  
        "uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/debits/WD4VYmyjRVVRJJ6Iuza9MKwY",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:04:38.881681Z",  
            "uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/cards/CCa2190160221411e2b4aa80ee7316ae44",  
            "id": "CCa2190160221411e2b4aa80ee7316ae44",  
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
            "created_at": "2012-10-29T15:04:38.899679Z",  
            "uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/holds/HL4VTFT6MxGqabzXAN1mTHjS",  
            "expires_at": "2012-10-30T22:04:38.883905Z",  
            "transaction_number": "HL488-446-2461",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8",  
            "source_uri": "/v1/marketplaces/TEST-MP4VGvWw2ufwtgY9mLPv29ww/accounts/AC4VQLfA5Cdny8golEUWV5o8/cards/CCa2190160221411e2b4aa80ee7316ae44",  
            "id": "HL4VTFT6MxGqabzXAN1mTHjS" 
        },  
        "id": "WD4VYmyjRVVRJJ6Iuza9MKwY",  
        "available_at": "2012-10-29T22:04:38.965726Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:41.536158Z",  
            "uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4YRxfKGo2VEx6VXgBEIzju",  
            "credits_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL935-174-6305",  
        "created_at": "2012-10-29T15:04:41.577757Z",  
        "uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/holds/HL4YUqvLOVNY2VE3uQq5kM0k",  
        "expires_at": "2012-10-30T22:04:41.562187Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:04:41.559920Z",  
            "uri": "/v1/marketplaces/TEST-MP4YHjyFD2dbrlFEbBbgaosc/accounts/AC4YRxfKGo2VEx6VXgBEIzju/cards/CCa3b1ad1a221411e2b47680ee7316ae44",  
            "id": "CCa3b1ad1a221411e2b47680ee7316ae44",  
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
        "id": "HL4YUqvLOVNY2VE3uQq5kM0k" 
    } 
 

