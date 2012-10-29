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
            "holds_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:32.366699Z",  
            "uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4DRTxiuquYwfqf48XU5moA",  
            "credits_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL774-303-9026",  
        "created_at": "2012-10-29T15:11:32.453114Z",  
        "uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/holds/HL4DXTABLXSld9zQiIbctN4g",  
        "expires_at": "2012-11-05T22:11:32.448893Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:11:32.388689Z",  
            "uri": "/v1/marketplaces/TEST-MP4DI4vbSU22774pZpcINBdi/accounts/AC4DRTxiuquYwfqf48XU5moA/cards/CC98914548221511e2b1c780ee7316ae44",  
            "id": "CC98914548221511e2b1c780ee7316ae44",  
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
        "id": "HL4DXTABLXSld9zQiIbctN4g" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:34.003310Z",  
            "uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4FI0P9sw5knFtVM6s68Puk",  
            "credits_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL363-332-2111",  
        "created_at": "2012-10-29T15:11:34.045666Z",  
        "uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/holds/HL4FKXlhxMC0KwLVwruRNgKo",  
        "expires_at": "2012-10-30T22:11:34.030074Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:11:34.027839Z",  
            "uri": "/v1/marketplaces/TEST-MP4Fy3NpMrYG8nXgbUc6UIoA/accounts/AC4FI0P9sw5knFtVM6s68Puk/cards/CC998b4994221511e29b4f80ee7316ae44",  
            "id": "CC998b4994221511e29b4f80ee7316ae44",  
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
        "id": "HL4FKXlhxMC0KwLVwruRNgKo" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:35.622265Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL802-456-2985",  
                "created_at": "2012-10-29T15:11:35.661654Z",  
                "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/holds/HL4HzE5po2IKyXhPs6PzO5XC",  
                "expires_at": "2012-10-30T22:11:35.644323Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:11:35.642106Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards/CC9a819ba0221511e28eb580ee7316ae44",  
                    "id": "CC9a819ba0221511e28eb580ee7316ae44",  
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
                "id": "HL4HzE5po2IKyXhPs6PzO5XC" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:35.622265Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL013-622-5322",  
                "created_at": "2012-10-29T15:11:35.663138Z",  
                "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/holds/HL4HzKVt6NWHLGuuP6qTLIfW",  
                "expires_at": "2012-10-30T22:11:35.656767Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:11:35.642106Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards/CC9a819ba0221511e28eb580ee7316ae44",  
                    "id": "CC9a819ba0221511e28eb580ee7316ae44",  
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
                "id": "HL4HzKVt6NWHLGuuP6qTLIfW" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:35.622265Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL211-607-0811",  
                "created_at": "2012-10-29T15:11:35.664502Z",  
                "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/holds/HL4HzQVNj6rzANpU16hnDK60",  
                "expires_at": "2012-10-30T22:11:35.657079Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:11:35.642106Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards/CC9a819ba0221511e28eb580ee7316ae44",  
                    "id": "CC9a819ba0221511e28eb580ee7316ae44",  
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
                "id": "HL4HzQVNj6rzANpU16hnDK60" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:35.622265Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC4HwV8a1BqVhxRUGViV5Ipu",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL560-061-1375",  
                "created_at": "2012-10-29T15:11:35.665809Z",  
                "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/holds/HL4HzWL879QoFrYmQcBqnQ4Q",  
                "expires_at": "2012-10-30T22:11:35.657380Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:11:35.642106Z",  
                    "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/cards/CC9a819ba0221511e28eb580ee7316ae44",  
                    "id": "CC9a819ba0221511e28eb580ee7316ae44",  
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
                "id": "HL4HzWL879QoFrYmQcBqnQ4Q" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4Hny04l2QIxmPWCIuaVfc8/accounts/AC4HwV8a1BqVhxRUGViV5Ipu/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:38.979233Z",  
            "uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4Lj07qdPHKKrBQVc4UVUQk",  
            "credits_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL989-695-2410",  
        "created_at": "2012-10-29T15:11:39.021773Z",  
        "uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/holds/HL4LlWO0sycCNZ0y5QFz7BOY",  
        "expires_at": "2012-10-30T22:11:39.005337Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:11:39.003132Z",  
            "uri": "/v1/marketplaces/TEST-MP4L8OmHemODIvYGgNqMckhS/accounts/AC4Lj07qdPHKKrBQVc4UVUQk/cards/CC9c82738e221511e2a25880ee7316ae44",  
            "id": "CC9c82738e221511e2a25880ee7316ae44",  
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
        "id": "HL4LlWO0sycCNZ0y5QFz7BOY" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/holds/HL4NkaHQ87jowGg1AS57HrAE" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:40.731709Z",  
            "uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4NhcKrOVbIvIlTwUUsxQ7a",  
            "credits_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/debits/WD4NoZFIgbcqBvgbxHTwwYF6/refunds",  
        "created_at": "2012-10-29T15:11:40.854790Z",  
        "transaction_number": "W466-934-3064",  
        "uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/debits/WD4NoZFIgbcqBvgbxHTwwYF6",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:11:40.756306Z",  
            "uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/cards/CC9d8df816221511e2a10980ee7316ae44",  
            "id": "CC9d8df816221511e2a10980ee7316ae44",  
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
            "created_at": "2012-10-29T15:11:40.774446Z",  
            "uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/holds/HL4NkaHQ87jowGg1AS57HrAE",  
            "expires_at": "2012-10-30T22:11:40.758578Z",  
            "transaction_number": "HL396-964-6417",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a",  
            "source_uri": "/v1/marketplaces/TEST-MP4N6svZXTyvYlbyjH0zM4y8/accounts/AC4NhcKrOVbIvIlTwUUsxQ7a/cards/CC9d8df816221511e2a10980ee7316ae44",  
            "id": "HL4NkaHQ87jowGg1AS57HrAE" 
        },  
        "id": "WD4NoZFIgbcqBvgbxHTwwYF6",  
        "available_at": "2012-10-29T22:11:40.842269Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:43.898130Z",  
            "uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC4QQ0CpRPqfeuH4Esiczdf6",  
            "credits_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL415-299-0997",  
        "created_at": "2012-10-29T15:11:43.939293Z",  
        "uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/holds/HL4QSS2vNZKVaYyYpJ34sZiQ",  
        "expires_at": "2012-10-30T22:11:43.925641Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:11:43.923016Z",  
            "uri": "/v1/marketplaces/TEST-MP4QG92XJKgCrosvgpmgDY8s/accounts/AC4QQ0CpRPqfeuH4Esiczdf6/cards/CC9f71130c221511e2aed980ee7316ae44",  
            "id": "CC9f71130c221511e2aed980ee7316ae44",  
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
        "id": "HL4QSS2vNZKVaYyYpJ34sZiQ" 
    } 
 

