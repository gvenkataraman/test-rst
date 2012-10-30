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
            "holds_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:29.674858Z",  
            "uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC6Uwe4cpseYiTRDmgA8HntV",  
            "credits_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL398-981-9368",  
        "created_at": "2012-10-30T00:10:29.770782Z",  
        "uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/holds/HL6UCSdr1c9MAkGXPxWynqJd",  
        "expires_at": "2012-11-06T07:10:29.765780Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T00:10:29.698459Z",  
            "uri": "/v1/marketplaces/TEST-MP6Um10fLWEHxxxWyXstkONJ/accounts/AC6Uwe4cpseYiTRDmgA8HntV/cards/CCe31b0a54226011e298fd80ee7316ae43",  
            "id": "CCe31b0a54226011e298fd80ee7316ae43",  
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
        "id": "HL6UCSdr1c9MAkGXPxWynqJd" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:31.947029Z",  
            "uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC6X4E30fRVR3IQi6eoeEa43",  
            "credits_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL816-023-8319",  
        "created_at": "2012-10-30T00:10:31.991709Z",  
        "uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/holds/HL6X7Ml2FWteTTMtfBLCLYav",  
        "expires_at": "2012-10-31T07:10:31.974367Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T00:10:31.972131Z",  
            "uri": "/v1/marketplaces/TEST-MP6WTPMbYO7Z3PlnE1lNAZnJ/accounts/AC6X4E30fRVR3IQi6eoeEa43/cards/CCe4760912226011e2b55180ee7316ae43",  
            "id": "CCe4760912226011e2b55180ee7316ae43",  
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
        "id": "HL6X7Ml2FWteTTMtfBLCLYav" 
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
        "first_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:33.879665Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL077-352-0472",  
                "created_at": "2012-10-30T00:10:33.920184Z",  
                "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/holds/HL6Zig4FTTOtRjiPDwdYpZab",  
                "expires_at": "2012-10-31T07:10:33.905000Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T00:10:33.902500Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards/CCe59c9720226011e2968e80ee7316ae43",  
                    "id": "CCe59c9720226011e2968e80ee7316ae43",  
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
                "id": "HL6Zig4FTTOtRjiPDwdYpZab" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:33.879665Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL129-151-2788",  
                "created_at": "2012-10-30T00:10:33.921910Z",  
                "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/holds/HL6Zine2dbBfg3Wb1oZnG4tJ",  
                "expires_at": "2012-10-31T07:10:33.916037Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T00:10:33.902500Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards/CCe59c9720226011e2968e80ee7316ae43",  
                    "id": "CCe59c9720226011e2968e80ee7316ae43",  
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
                "id": "HL6Zine2dbBfg3Wb1oZnG4tJ" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:33.879665Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL775-984-3228",  
                "created_at": "2012-10-30T00:10:33.923417Z",  
                "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/holds/HL6ZiusdFBwIcOVGUvxOgh35",  
                "expires_at": "2012-10-31T07:10:33.916394Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T00:10:33.902500Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards/CCe59c9720226011e2968e80ee7316ae43",  
                    "id": "CCe59c9720226011e2968e80ee7316ae43",  
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
                "id": "HL6ZiusdFBwIcOVGUvxOgh35" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:33.879665Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC6ZfrEBKGrM3WkzJBoHO3uj",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL682-607-2647",  
                "created_at": "2012-10-30T00:10:33.924851Z",  
                "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/holds/HL6ZiAsOuiAvyOZdzNnzqDXt",  
                "expires_at": "2012-10-31T07:10:33.916637Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T00:10:33.902500Z",  
                    "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/cards/CCe59c9720226011e2968e80ee7316ae43",  
                    "id": "CCe59c9720226011e2968e80ee7316ae43",  
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
                "id": "HL6ZiAsOuiAvyOZdzNnzqDXt" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP6Z4o8nehHa5NSA35nmshUf/accounts/AC6ZfrEBKGrM3WkzJBoHO3uj/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:37.845857Z",  
            "uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC73HWTloQ1If7Bp0P2NC9ft",  
            "credits_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL321-872-4666",  
        "created_at": "2012-10-30T00:10:37.885303Z",  
        "uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/holds/HL73KKS4nDVLVNdmJ93C3pOr",  
        "expires_at": "2012-10-31T07:10:37.870368Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T00:10:37.868396Z",  
            "uri": "/v1/marketplaces/TEST-MP73xKOMA3rVXohjoXg0Zpx9/accounts/AC73HWTloQ1If7Bp0P2NC9ft/cards/CCe7f9b03e226011e2bc4b80ee7316ae43",  
            "id": "CCe7f9b03e226011e2bc4b80ee7316ae43",  
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
        "id": "HL73KKS4nDVLVNdmJ93C3pOr" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/holds/HL75U0n7BHFa5LnoOBa7yR0f" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:39.755430Z",  
            "uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC75RaYcSypOSxFMFOYwNMv9",  
            "credits_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/debits/WD75YnZ1t7diSyH0KKyvQfXJ/refunds",  
        "created_at": "2012-10-30T00:10:39.871105Z",  
        "transaction_number": "W106-987-3660",  
        "uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/debits/WD75YnZ1t7diSyH0KKyvQfXJ",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T00:10:39.777317Z",  
            "uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/cards/CCe91d0f60226011e2938c80ee7316ae43",  
            "id": "CCe91d0f60226011e2938c80ee7316ae43",  
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
            "created_at": "2012-10-30T00:10:39.796212Z",  
            "uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/holds/HL75U0n7BHFa5LnoOBa7yR0f",  
            "expires_at": "2012-10-31T07:10:39.779492Z",  
            "transaction_number": "HL688-605-2013",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9",  
            "source_uri": "/v1/marketplaces/TEST-MP75HCyedyUQ4DF874wpi0fx/accounts/AC75RaYcSypOSxFMFOYwNMv9/cards/CCe91d0f60226011e2938c80ee7316ae43",  
            "id": "HL75U0n7BHFa5LnoOBa7yR0f" 
        },  
        "id": "WD75YnZ1t7diSyH0KKyvQfXJ",  
        "available_at": "2012-10-30T07:10:39.857744Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:43.892264Z",  
            "uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7avElBjwqi4WqmbUoS57eb",  
            "credits_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL810-409-0609",  
        "created_at": "2012-10-30T00:10:43.933042Z",  
        "uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/holds/HL7aytpBJLJfUNUzu3uHLGi7",  
        "expires_at": "2012-10-31T07:10:43.918373Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T00:10:43.916001Z",  
            "uri": "/v1/marketplaces/TEST-MP7alid0MqmkR8bGMBGEPfcT/accounts/AC7avElBjwqi4WqmbUoS57eb/cards/CCeb9491aa226011e2b68a80ee7316ae43",  
            "id": "CCeb9491aa226011e2b68a80ee7316ae43",  
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
        "id": "HL7aytpBJLJfUNUzu3uHLGi7" 
    } 
 

