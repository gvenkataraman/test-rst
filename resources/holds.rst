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
    hold was will expire and can **NO LONGER BE CAPTURED** 
 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:07.048722Z",  
            "uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3rgU4Ck5n0MLFZGMMwpwDq",  
            "credits_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL661-964-3372",  
        "created_at": "2012-10-29T14:56:07.120368Z",  
        "uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/holds/HL3rlScLm3zdsIlFaHWklvvK",  
        "expires_at": "2012-11-05T21:56:07.116681Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T14:56:07.065573Z",  
            "uri": "/v1/marketplaces/TEST-MP3r6FcTrmRNOBK2TuvwHfSI/accounts/AC3rgU4Ck5n0MLFZGMMwpwDq/cards/CC71084bea221311e2a3e280ee7316ae44",  
            "id": "CC71084bea221311e2a3e280ee7316ae44",  
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
        "id": "HL3rlScLm3zdsIlFaHWklvvK" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:08.343088Z",  
            "uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3sJ9RTh7JuQ9igpnLtAGeE",  
            "credits_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL772-935-4299",  
        "created_at": "2012-10-29T14:56:08.384062Z",  
        "uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/holds/HL3sLZT8yVxwUwJ76EhXElHS",  
        "expires_at": "2012-10-30T21:56:08.367939Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T14:56:08.365641Z",  
            "uri": "/v1/marketplaces/TEST-MP3sBtKxBsrjHYxFZgtvcrqs/accounts/AC3sJ9RTh7JuQ9igpnLtAGeE/cards/CC71ce6c58221311e2b05680ee7316ae44",  
            "id": "CC71ce6c58221311e2b05680ee7316ae44",  
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
        "id": "HL3sLZT8yVxwUwJ76EhXElHS" 
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
        "first_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:56:09.704876Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ug7JLcHZVoVryuVhhqwqo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL681-877-2605",  
                "created_at": "2012-10-29T14:56:09.735046Z",  
                "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/holds/HL3uidHr9YoVmyAtunGXhWba",  
                "expires_at": "2012-10-30T21:56:09.724237Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T14:56:09.722725Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards/CC729dc49e221311e2a90f80ee7316ae44",  
                    "id": "CC729dc49e221311e2a90f80ee7316ae44",  
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
                "id": "HL3uidHr9YoVmyAtunGXhWba" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:56:09.704876Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ug7JLcHZVoVryuVhhqwqo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL059-030-9871",  
                "created_at": "2012-10-29T14:56:09.736100Z",  
                "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/holds/HL3uiiM8d5Mi8ulY702syU1S",  
                "expires_at": "2012-10-30T21:56:09.731867Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T14:56:09.722725Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards/CC729dc49e221311e2a90f80ee7316ae44",  
                    "id": "CC729dc49e221311e2a90f80ee7316ae44",  
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
                "id": "HL3uiiM8d5Mi8ulY702syU1S" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:56:09.704876Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ug7JLcHZVoVryuVhhqwqo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL429-127-4245",  
                "created_at": "2012-10-29T14:56:09.737055Z",  
                "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/holds/HL3uin42y6CMmAhwKOvc01bS",  
                "expires_at": "2012-10-30T21:56:09.732061Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T14:56:09.722725Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards/CC729dc49e221311e2a90f80ee7316ae44",  
                    "id": "CC729dc49e221311e2a90f80ee7316ae44",  
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
                "id": "HL3uin42y6CMmAhwKOvc01bS" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:56:09.704876Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC3ug7JLcHZVoVryuVhhqwqo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL500-638-7660",  
                "created_at": "2012-10-29T14:56:09.738033Z",  
                "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/holds/HL3uira9DGGrfyrMBRtEqbhG",  
                "expires_at": "2012-10-30T21:56:09.732246Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T14:56:09.722725Z",  
                    "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/cards/CC729dc49e221311e2a90f80ee7316ae44",  
                    "id": "CC729dc49e221311e2a90f80ee7316ae44",  
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
                "id": "HL3uira9DGGrfyrMBRtEqbhG" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP3u8iKTYRPwNSbTC1PqDCGU/accounts/AC3ug7JLcHZVoVryuVhhqwqo/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:12.590106Z",  
            "uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3xvj34aPUprHXugguptZXu",  
            "credits_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL915-638-6113",  
        "created_at": "2012-10-29T14:56:12.632188Z",  
        "uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/holds/HL3xyepmhVspEg9boQEpRmx6",  
        "expires_at": "2012-10-30T21:56:12.616503Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T14:56:12.614209Z",  
            "uri": "/v1/marketplaces/TEST-MP3xmwE5nR0O3mzmpKStaq0s/accounts/AC3xvj34aPUprHXugguptZXu/cards/CC7456bc64221311e28a3980ee7316ae44",  
            "id": "CC7456bc64221311e28a3980ee7316ae44",  
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
        "id": "HL3xyepmhVspEg9boQEpRmx6" 
    } 
 

Capture a Hold
--------------

Use `hold_uri` when `creating a debit <./debits.rst#create-a-debit>`_.

Request 
~~~~~~~ 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "hold_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/holds/HL3zf883rOB6auq5XxVVZwPy" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:14.094505Z",  
            "uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3zcdmdyBFi6S2N4qbRQnJO",  
            "credits_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/debits/WD3zjShQVk2imvMezKG7Tani/refunds",  
        "created_at": "2012-10-29T14:56:14.215870Z",  
        "transaction_number": "W736-402-2099",  
        "uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/debits/WD3zjShQVk2imvMezKG7Tani",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T14:56:14.118519Z",  
            "uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/cards/CC753c4720221311e29cd280ee7316ae44",  
            "id": "CC753c4720221311e29cd280ee7316ae44",  
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
            "created_at": "2012-10-29T14:56:14.136494Z",  
            "uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/holds/HL3zf883rOB6auq5XxVVZwPy",  
            "expires_at": "2012-10-30T21:56:14.120761Z",  
            "transaction_number": "HL530-000-2262",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO",  
            "source_uri": "/v1/marketplaces/TEST-MP3z1QVFwXRalu230GfXLK2U/accounts/AC3zcdmdyBFi6S2N4qbRQnJO/cards/CC753c4720221311e29cd280ee7316ae44",  
            "id": "HL3zf883rOB6auq5XxVVZwPy" 
        },  
        "id": "WD3zjShQVk2imvMezKG7Tani",  
        "available_at": "2012-10-29T21:56:14.203234Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:16.957875Z",  
            "uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC3CpTGvo1xcjviNUtSprCPq",  
            "credits_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL654-632-0542",  
        "created_at": "2012-10-29T14:56:16.986496Z",  
        "uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/holds/HL3CrSMfhKLKmbkddULOh2NC",  
        "expires_at": "2012-10-30T21:56:16.975532Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T14:56:16.973921Z",  
            "uri": "/v1/marketplaces/TEST-MP3Cgm8pcFgJ8kCnj35mo9AE/accounts/AC3CpTGvo1xcjviNUtSprCPq/cards/CC76f02fa0221311e2b41f80ee7316ae44",  
            "id": "CC76f02fa0221311e2b41f80ee7316ae44",  
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
        "id": "HL3CrSMfhKLKmbkddULOh2NC" 
    } 
 

