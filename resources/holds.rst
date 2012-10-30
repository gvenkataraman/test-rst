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
    **object**. The captured debit associated with this hold.See `Debit <./debits.rst>`_. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``account`` 
    **object**. The account against which this hold was created.See `Account <./accounts.rst>`_. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``is_void`` 
    **boolean**. A boolean flag indicating if the hold has been voided or not.  
 
``source`` 
    **object**. The funding source for this hold.See `Card <./cards.rst>`_. 
 

Create a Hold
-------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts/(account-id)/holds 
    POST /v1/marketplaces/(marketplace-id)/holds 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:24.382687Z",  
            "uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC1dTwLt3k18mxojA9aEVCF6",  
            "credits_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL380-323-2245",  
        "created_at": "2012-10-30T09:59:24.464030Z",  
        "uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/holds/HL1dZb9z3AqJRCdYvQF438Yk",  
        "expires_at": "2012-11-06T16:59:24.459890Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T09:59:24.401518Z",  
            "uri": "/v1/marketplaces/TEST-MP1dJVteyRT5NjhvRss1HR2Y/accounts/AC1dTwLt3k18mxojA9aEVCF6/cards/CC283afb0622b311e28a3880ee7316ae44",  
            "id": "CC283afb0622b311e28a3880ee7316ae44",  
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
        "id": "HL1dZb9z3AqJRCdYvQF438Yk" 
    } 
 

Retrieve a Hold
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/holds/(hold-id) 
    GET /v1/marketplaces/(marketplace-id)/holds/(hold-id) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:25.988664Z",  
            "uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC1fHwHBgYmCYZ4SN7CTmPly",  
            "credits_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL931-107-2417",  
        "created_at": "2012-10-30T09:59:26.020363Z",  
        "uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/holds/HL1fJIWuruKXbKoNJR9CJGkI",  
        "expires_at": "2012-10-31T16:59:26.007975Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T09:59:26.006279Z",  
            "uri": "/v1/marketplaces/TEST-MP1fxO24gD9zqLwt7sKlviN6/accounts/AC1fHwHBgYmCYZ4SN7CTmPly/cards/CC292fe71022b311e2b77980ee7316ae44",  
            "id": "CC292fe71022b311e2b77980ee7316ae44",  
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
        "id": "HL1fJIWuruKXbKoNJR9CJGkI" 
    } 
 

List all Holds
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/holds 
    GET /v1/marketplaces/(marketplace-id)/holds 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:27.497184Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC1hoIMIzs49pFlGnHtBkbw8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL149-281-3968",  
                "created_at": "2012-10-30T09:59:27.530250Z",  
                "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/holds/HL1hr0BoD3btVvD4KI0chqrq",  
                "expires_at": "2012-10-31T16:59:27.516256Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T09:59:27.514244Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards/CC2a1601b422b311e2bb6c80ee7316ae44",  
                    "id": "CC2a1601b422b311e2bb6c80ee7316ae44",  
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
                "id": "HL1hr0BoD3btVvD4KI0chqrq" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:27.497184Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC1hoIMIzs49pFlGnHtBkbw8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL551-267-2992",  
                "created_at": "2012-10-30T09:59:27.531954Z",  
                "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/holds/HL1hr7Pjt4y1lnutawzlzhWs",  
                "expires_at": "2012-10-31T16:59:27.526495Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T09:59:27.514244Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards/CC2a1601b422b311e2bb6c80ee7316ae44",  
                    "id": "CC2a1601b422b311e2bb6c80ee7316ae44",  
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
                "id": "HL1hr7Pjt4y1lnutawzlzhWs" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:27.497184Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC1hoIMIzs49pFlGnHtBkbw8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL524-740-6266",  
                "created_at": "2012-10-30T09:59:27.533498Z",  
                "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/holds/HL1hregYPMvxhbMay7ehBYTq",  
                "expires_at": "2012-10-31T16:59:27.526723Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T09:59:27.514244Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards/CC2a1601b422b311e2bb6c80ee7316ae44",  
                    "id": "CC2a1601b422b311e2bb6c80ee7316ae44",  
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
                "id": "HL1hregYPMvxhbMay7ehBYTq" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:27.497184Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC1hoIMIzs49pFlGnHtBkbw8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL830-081-2703",  
                "created_at": "2012-10-30T09:59:27.535228Z",  
                "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/holds/HL1hrlGGVeEU2boRKHhHUNsE",  
                "expires_at": "2012-10-31T16:59:27.526910Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T09:59:27.514244Z",  
                    "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/cards/CC2a1601b422b311e2bb6c80ee7316ae44",  
                    "id": "CC2a1601b422b311e2bb6c80ee7316ae44",  
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
                "id": "HL1hrlGGVeEU2boRKHhHUNsE" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1hf9eMh3wZ9G9zwe3FBI4k/accounts/AC1hoIMIzs49pFlGnHtBkbw8/holds?limit=10&offset=0" 
    } 
 

Update a Hold
-------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id)/holds/(hold-id) 
    PUT /v1/marketplaces/(marketplace-id)/holds/(hold-id) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:31.128485Z",  
            "uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC1ltVx203kAtIc7Lb0kS4Xq",  
            "credits_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL819-065-9585",  
        "created_at": "2012-10-30T09:59:31.167627Z",  
        "uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/holds/HL1lwEvlQ4S7SG8wpwu6LOMQ",  
        "expires_at": "2012-10-31T16:59:31.153373Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T09:59:31.151237Z",  
            "uri": "/v1/marketplaces/TEST-MP1lk3lfjjCgPsejODJvEeSE/accounts/AC1ltVx203kAtIc7Lb0kS4Xq/cards/CC2c40c44222b311e2a2a280ee7316ae44",  
            "id": "CC2c40c44222b311e2a2a280ee7316ae44",  
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
        "id": "HL1lwEvlQ4S7SG8wpwu6LOMQ" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/holds/HL1on78dCUCEJvJvAWAvl4AQ" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:33.627354Z",  
            "uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC1oi7LWIqqVp1RBWCJtozUU",  
            "credits_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/debits/WD1osjaqj0z1p9CMnWlszXGA/refunds",  
        "created_at": "2012-10-30T09:59:33.781825Z",  
        "transaction_number": "W688-937-2997",  
        "uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/debits/WD1osjaqj0z1p9CMnWlszXGA",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T09:59:33.664844Z",  
            "uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/cards/CC2dbfd21822b311e2bd2080ee7316ae44",  
            "id": "CC2dbfd21822b311e2bd2080ee7316ae44",  
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
            "created_at": "2012-10-30T09:59:33.698692Z",  
            "uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/holds/HL1on78dCUCEJvJvAWAvl4AQ",  
            "expires_at": "2012-10-31T16:59:33.668987Z",  
            "transaction_number": "HL063-308-3787",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU",  
            "source_uri": "/v1/marketplaces/TEST-MP1o24VQR6yVSpINRoKBLnhO/accounts/AC1oi7LWIqqVp1RBWCJtozUU/cards/CC2dbfd21822b311e2bd2080ee7316ae44",  
            "id": "HL1on78dCUCEJvJvAWAvl4AQ" 
        },  
        "id": "WD1osjaqj0z1p9CMnWlszXGA",  
        "available_at": "2012-10-30T16:59:33.771536Z" 
    } 
 

Void a Hold
-----------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id)/holds/(hold-id) 
    PUT /v1/marketplaces/(marketplace-id)/holds/(hold-id) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:37.454150Z",  
            "uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC1sB39YIs2KbQHt7e9brqSg",  
            "credits_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL088-343-9702",  
        "created_at": "2012-10-30T09:59:37.493061Z",  
        "uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/holds/HL1sDJz4H8X6uCQh9exfDji4",  
        "expires_at": "2012-10-31T16:59:37.477296Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T09:59:37.474768Z",  
            "uri": "/v1/marketplaces/TEST-MP1ssAZKQ0cGVTpvFQ64MChe/accounts/AC1sB39YIs2KbQHt7e9brqSg/cards/CC3005b62822b311e284da80ee7316ae44",  
            "id": "CC3005b62822b311e284da80ee7316ae44",  
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
        "id": "HL1sDJz4H8X6uCQh9exfDji4" 
    } 
 

