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
            "holds_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:16.074087Z",  
            "uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC38M7nTHit4ac80Bv5v4ouM",  
            "credits_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL095-174-6248",  
        "created_at": "2012-10-29T16:00:16.168726Z",  
        "uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/holds/HL38SH3a6cbDlw8maUvD02ry",  
        "expires_at": "2012-11-05T23:00:16.164086Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:00:16.098031Z",  
            "uri": "/v1/marketplaces/TEST-MP38BSHqPdCPtnH7EokdMoFC/accounts/AC38M7nTHit4ac80Bv5v4ouM/cards/CC673bce6c221c11e28a6b80ee7316ae44",  
            "id": "CC673bce6c221c11e28a6b80ee7316ae44",  
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
        "id": "HL38SH3a6cbDlw8maUvD02ry" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:17.630173Z",  
            "uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3awD8iMcTj6Dao1fd1TUig",  
            "credits_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL123-775-9244",  
        "created_at": "2012-10-29T16:00:17.671846Z",  
        "uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/holds/HL3azwvyDrRoP2eLjEHZvhRO",  
        "expires_at": "2012-10-30T23:00:17.656137Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:00:17.653934Z",  
            "uri": "/v1/marketplaces/TEST-MP3aokqQx0es39AfHXHzKZjm/accounts/AC3awD8iMcTj6Dao1fd1TUig/cards/CC68293864221c11e2bfa580ee7316ae44",  
            "id": "CC68293864221c11e2bfa580ee7316ae44",  
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
        "id": "HL3azwvyDrRoP2eLjEHZvhRO" 
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
        "first_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:19.233253Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL464-790-7207",  
                "created_at": "2012-10-29T16:00:19.277271Z",  
                "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/holds/HL3cntwdASOHjmO8nCeq57Pm",  
                "expires_at": "2012-10-30T23:00:19.259972Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:00:19.257739Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards/CC691df1d8221c11e2962e80ee7316ae44",  
                    "id": "CC691df1d8221c11e2962e80ee7316ae44",  
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
                "id": "HL3cntwdASOHjmO8nCeq57Pm" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:19.233253Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL067-565-1568",  
                "created_at": "2012-10-29T16:00:19.278738Z",  
                "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/holds/HL3cnArUjXS8ELLkFHABfSAs",  
                "expires_at": "2012-10-30T23:00:19.272355Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:00:19.257739Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards/CC691df1d8221c11e2962e80ee7316ae44",  
                    "id": "CC691df1d8221c11e2962e80ee7316ae44",  
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
                "id": "HL3cnArUjXS8ELLkFHABfSAs" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:19.233253Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL178-962-8846",  
                "created_at": "2012-10-29T16:00:19.280079Z",  
                "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/holds/HL3cnGrHhtf9q6quV7swxehS",  
                "expires_at": "2012-10-30T23:00:19.272666Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:00:19.257739Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards/CC691df1d8221c11e2962e80ee7316ae44",  
                    "id": "CC691df1d8221c11e2962e80ee7316ae44",  
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
                "id": "HL3cnGrHhtf9q6quV7swxehS" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:19.233253Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ckpZ2oBY0ZjWwTo3Tl8pK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL915-387-3210",  
                "created_at": "2012-10-29T16:00:19.281399Z",  
                "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/holds/HL3cnM8bEs3lZpEZ9Eamw6Y4",  
                "expires_at": "2012-10-30T23:00:19.272967Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:00:19.257739Z",  
                    "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/cards/CC691df1d8221c11e2962e80ee7316ae44",  
                    "id": "CC691df1d8221c11e2962e80ee7316ae44",  
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
                "id": "HL3cnM8bEs3lZpEZ9Eamw6Y4" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP3ca5U2E63KgM3embOsT1A0/accounts/AC3ckpZ2oBY0ZjWwTo3Tl8pK/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:22.479924Z",  
            "uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3fYPyDRKLUMVTKo3PCxpha",  
            "credits_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL707-503-9040",  
        "created_at": "2012-10-29T16:00:22.510664Z",  
        "uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/holds/HL3g0XIuqhmiehzTmUl0FsrO",  
        "expires_at": "2012-10-30T23:00:22.499376Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:00:22.497703Z",  
            "uri": "/v1/marketplaces/TEST-MP3fOIKzlwmkCg6sbzSCcAtK/accounts/AC3fYPyDRKLUMVTKo3PCxpha/cards/CC6b0c7974221c11e2826880ee7316ae44",  
            "id": "CC6b0c7974221c11e2826880ee7316ae44",  
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
        "id": "HL3g0XIuqhmiehzTmUl0FsrO" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/holds/HL3hLCaKL6nlxAoD2hAGwkaE" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:24.027256Z",  
            "uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3hIIAmyrNMPBUlAEF3qibi",  
            "credits_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/debits/WD3hQcDj9YdeT6Yr0Iq9VIkQ/refunds",  
        "created_at": "2012-10-29T16:00:24.142275Z",  
        "transaction_number": "W308-610-5126",  
        "uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/debits/WD3hQcDj9YdeT6Yr0Iq9VIkQ",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:00:24.051100Z",  
            "uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/cards/CC6bf95bcc221c11e2b79080ee7316ae44",  
            "id": "CC6bf95bcc221c11e2b79080ee7316ae44",  
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
            "created_at": "2012-10-29T16:00:24.068973Z",  
            "uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/holds/HL3hLCaKL6nlxAoD2hAGwkaE",  
            "expires_at": "2012-10-30T23:00:24.053289Z",  
            "transaction_number": "HL168-498-9968",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi",  
            "source_uri": "/v1/marketplaces/TEST-MP3hyHJFq9GREgB8nYGsHLso/accounts/AC3hIIAmyrNMPBUlAEF3qibi/cards/CC6bf95bcc221c11e2b79080ee7316ae44",  
            "id": "HL3hLCaKL6nlxAoD2hAGwkaE" 
        },  
        "id": "WD3hQcDj9YdeT6Yr0Iq9VIkQ",  
        "available_at": "2012-10-29T23:00:24.133596Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:27.151330Z",  
            "uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3leA3HRbhC2kILp0hae4M4",  
            "credits_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL263-909-3763",  
        "created_at": "2012-10-29T16:00:27.179781Z",  
        "uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/holds/HL3lgyljWPaDSJfDnbloJWHW",  
        "expires_at": "2012-10-30T23:00:27.168606Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T16:00:27.166847Z",  
            "uri": "/v1/marketplaces/TEST-MP3l4FZjM6vEDgMwXg3ZkpmY/accounts/AC3leA3HRbhC2kILp0hae4M4/cards/CC6dd500f4221c11e2809780ee7316ae44",  
            "id": "CC6dd500f4221c11e2809780ee7316ae44",  
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
        "id": "HL3lgyljWPaDSJfDnbloJWHW" 
    } 
 

