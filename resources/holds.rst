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
    **object**. The captured debit associated with this hold. See `Debit <./debits.rst>`_. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``account`` 
    **object**. The account against which this hold was created. See `Account <./accounts.rst>`_. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``is_void`` 
    **boolean**. A boolean flag indicating if the hold has been voided or not.  
 
``source`` 
    **object**. The funding source for this hold. See `Card <./cards.rst>`_. 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:37.244856Z",  
            "uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC5DC6wAEbHMil1fRKoRCv6Q",  
            "credits_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL221-260-8774",  
        "created_at": "2012-10-30T10:10:37.324602Z",  
        "uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/holds/HL5DHDl3El7GpwnL78gwuDgU",  
        "expires_at": "2012-11-06T17:10:37.320501Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T10:10:37.262465Z",  
            "uri": "/v1/marketplaces/TEST-MP5Dsp5s8L3aVxNbPMcP3Pqk/accounts/AC5DC6wAEbHMil1fRKoRCv6Q/cards/CCb9497a7222b411e296af80ee7316ae44",  
            "id": "CCb9497a7222b411e296af80ee7316ae44",  
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
        "id": "HL5DHDl3El7GpwnL78gwuDgU" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:38.772904Z",  
            "uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC5FkEpUWG0QUk0GLkAJ8G8s",  
            "credits_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL632-497-9019",  
        "created_at": "2012-10-30T10:10:38.814758Z",  
        "uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/holds/HL5FnyxOyR0oVrS2ge4edbQ8",  
        "expires_at": "2012-10-31T17:10:38.798921Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T10:10:38.796728Z",  
            "uri": "/v1/marketplaces/TEST-MP5FamMDIoXMr4fBClLc6ULi/accounts/AC5FkEpUWG0QUk0GLkAJ8G8s/cards/CCba3368d022b411e28c0980ee7316ae44",  
            "id": "CCba3368d022b411e28c0980ee7316ae44",  
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
        "id": "HL5FnyxOyR0oVrS2ge4edbQ8" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:40.172308Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC5GUeqjBV9NcekmfczSc48A",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL942-156-1852",  
                "created_at": "2012-10-30T10:10:40.213439Z",  
                "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/holds/HL5GX6MjjFaTIMui38OZZfg0",  
                "expires_at": "2012-10-31T17:10:40.199086Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T10:10:40.196834Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards/CCbb090e5e22b411e2883d80ee7316ae44",  
                    "id": "CCbb090e5e22b411e2883d80ee7316ae44",  
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
                "id": "HL5GX6MjjFaTIMui38OZZfg0" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:40.172308Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC5GUeqjBV9NcekmfczSc48A",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL514-898-9368",  
                "created_at": "2012-10-30T10:10:40.214462Z",  
                "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/holds/HL5GXbGydkA4O295frCCIXo8",  
                "expires_at": "2012-10-31T17:10:40.210404Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T10:10:40.196834Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards/CCbb090e5e22b411e2883d80ee7316ae44",  
                    "id": "CCbb090e5e22b411e2883d80ee7316ae44",  
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
                "id": "HL5GXbGydkA4O295frCCIXo8" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:40.172308Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC5GUeqjBV9NcekmfczSc48A",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL922-029-8680",  
                "created_at": "2012-10-30T10:10:40.215355Z",  
                "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/holds/HL5GXfHiUZnb5dGVEGPvek5u",  
                "expires_at": "2012-10-31T17:10:40.210584Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T10:10:40.196834Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards/CCbb090e5e22b411e2883d80ee7316ae44",  
                    "id": "CCbb090e5e22b411e2883d80ee7316ae44",  
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
                "id": "HL5GXfHiUZnb5dGVEGPvek5u" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:40.172308Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC5GUeqjBV9NcekmfczSc48A",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL622-302-7853",  
                "created_at": "2012-10-30T10:10:40.216279Z",  
                "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/holds/HL5GXjy8HZjWJvojAct3N7cU",  
                "expires_at": "2012-10-31T17:10:40.210751Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T10:10:40.196834Z",  
                    "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/cards/CCbb090e5e22b411e2883d80ee7316ae44",  
                    "id": "CCbb090e5e22b411e2883d80ee7316ae44",  
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
                "id": "HL5GXjy8HZjWJvojAct3N7cU" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5GKgecISWBIRr96Fsz6cdK/accounts/AC5GUeqjBV9NcekmfczSc48A/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:43.271205Z",  
            "uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC5Kokq1avp3OwK9HPY3WHuQ",  
            "credits_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL989-222-3093",  
        "created_at": "2012-10-30T10:10:43.312866Z",  
        "uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/holds/HL5KrdEHd4lsytCFSXQ65cQ4",  
        "expires_at": "2012-10-31T17:10:43.297155Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T10:10:43.294963Z",  
            "uri": "/v1/marketplaces/TEST-MP5KdZXY9V2ZtvAuxGIE3mFm/accounts/AC5Kokq1avp3OwK9HPY3WHuQ/cards/CCbce1ca5e22b411e2b09080ee7316ae44",  
            "id": "CCbce1ca5e22b411e2b09080ee7316ae44",  
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
        "id": "HL5KrdEHd4lsytCFSXQ65cQ4" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/holds/HL5M65iH9Rxl0rxEllVKS9GA" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:44.746422Z",  
            "uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC5M3cwHnGSe1DG1IgOzo0NS",  
            "credits_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/debits/WD5MaEETDHIC5dIIQNJ5QT4w/refunds",  
        "created_at": "2012-10-30T10:10:44.860238Z",  
        "transaction_number": "W705-659-6458",  
        "uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/debits/WD5MaEETDHIC5dIIQNJ5QT4w",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T10:10:44.770147Z",  
            "uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/cards/CCbdc2e38622b411e2ac5c80ee7316ae44",  
            "id": "CCbdc2e38622b411e2ac5c80ee7316ae44",  
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
            "created_at": "2012-10-30T10:10:44.787937Z",  
            "uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/holds/HL5M65iH9Rxl0rxEllVKS9GA",  
            "expires_at": "2012-10-31T17:10:44.772370Z",  
            "transaction_number": "HL878-486-1367",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS",  
            "source_uri": "/v1/marketplaces/TEST-MP5LSYeTu3Rm8DiedQYXjhoo/accounts/AC5M3cwHnGSe1DG1IgOzo0NS/cards/CCbdc2e38622b411e2ac5c80ee7316ae44",  
            "id": "HL5M65iH9Rxl0rxEllVKS9GA" 
        },  
        "id": "WD5MaEETDHIC5dIIQNJ5QT4w",  
        "available_at": "2012-10-30T17:10:44.852327Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:47.578901Z",  
            "uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC5PeIVLYWjam4JEKnfB35By",  
            "credits_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL861-949-8492",  
        "created_at": "2012-10-30T10:10:47.613992Z",  
        "uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/holds/HL5Ph9TEsRtXlua4LjatVq3q",  
        "expires_at": "2012-10-31T17:10:47.600280Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-30T10:10:47.598201Z",  
            "uri": "/v1/marketplaces/TEST-MP5P78RXWkgZpGtVbJFs4Xti/accounts/AC5PeIVLYWjam4JEKnfB35By/cards/CCbf72831222b411e29fc480ee7316ae44",  
            "id": "CCbf72831222b411e29fc480ee7316ae44",  
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
        "id": "HL5Ph9TEsRtXlua4LjatVq3q" 
    } 
 

