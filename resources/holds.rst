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
            "holds_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:09.997919Z",  
            "uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7yyx0hEEk9nfJb3dLmysrq",  
            "credits_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/cards" 
        },  
        "fee": 30,  
        "description": "Something tasty",  
        "transaction_number": "HL076-468-9347",  
        "created_at": "2012-10-29T15:57:10.095093Z",  
        "uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/holds/HL7yFh6TEkxCE12Awj6bQNLe",  
        "expires_at": "2012-11-05T22:57:10.090133Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:57:10.022073Z",  
            "uri": "/v1/marketplaces/TEST-MP7yn5uCFPwyOTuoTKh2MWZm/accounts/AC7yyx0hEEk9nfJb3dLmysrq/cards/CCf852e120221b11e2a4f480ee7316ae44",  
            "id": "CCf852e120221b11e2a4f480ee7316ae44",  
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
        "id": "HL7yFh6TEkxCE12Awj6bQNLe" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:11.512694Z",  
            "uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7Aga709Fy2MoV2eHk1FS1C",  
            "credits_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL447-781-2199",  
        "created_at": "2012-10-29T15:57:11.554291Z",  
        "uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/holds/HL7Aj39Ckp8GEkU89LIvv5ek",  
        "expires_at": "2012-10-30T22:57:11.538575Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:57:11.536327Z",  
            "uri": "/v1/marketplaces/TEST-MP7A6oJoQV7bCEf3m7JzlgKU/accounts/AC7Aga709Fy2MoV2eHk1FS1C/cards/CCf939f1b4221b11e2b6be80ee7316ae44",  
            "id": "CCf939f1b4221b11e2b6be80ee7316ae44",  
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
        "id": "HL7Aj39Ckp8GEkU89LIvv5ek" 
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
        "first_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:12.966729Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC7BTywxMcR9edl4q22Xq9kE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards" 
                },  
                "fee": 30,  
                "description": "Something sweet",  
                "transaction_number": "HL139-012-8193",  
                "created_at": "2012-10-29T15:57:13.011045Z",  
                "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/holds/HL7BWDhQQZHmcNoU4EUIaExS",  
                "expires_at": "2012-10-30T22:57:12.993481Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:57:12.991263Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards/CCfa17f09a221b11e2882580ee7316ae44",  
                    "id": "CCfa17f09a221b11e2882580ee7316ae44",  
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
                "id": "HL7BWDhQQZHmcNoU4EUIaExS" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:12.966729Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC7BTywxMcR9edl4q22Xq9kE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards" 
                },  
                "fee": 30,  
                "description": "Something sour",  
                "transaction_number": "HL057-797-1958",  
                "created_at": "2012-10-29T15:57:13.012490Z",  
                "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/holds/HL7BWKfpUQHigqgWFMbQpMNe",  
                "expires_at": "2012-10-30T22:57:13.006104Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:57:12.991263Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards/CCfa17f09a221b11e2882580ee7316ae44",  
                    "id": "CCfa17f09a221b11e2882580ee7316ae44",  
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
                "id": "HL7BWKfpUQHigqgWFMbQpMNe" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:12.966729Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC7BTywxMcR9edl4q22Xq9kE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards" 
                },  
                "fee": 30,  
                "description": "Something spicy",  
                "transaction_number": "HL582-930-9459",  
                "created_at": "2012-10-29T15:57:13.013850Z",  
                "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/holds/HL7BWQ7qURJoDY8CdMoG7hti",  
                "expires_at": "2012-10-30T22:57:13.006426Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:57:12.991263Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards/CCfa17f09a221b11e2882580ee7316ae44",  
                    "id": "CCfa17f09a221b11e2882580ee7316ae44",  
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
                "id": "HL7BWQ7qURJoDY8CdMoG7hti" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:12.966729Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/transactions",  
                    "email_address": "email.9@y.com",  
                    "id": "AC7BTywxMcR9edl4q22Xq9kE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards" 
                },  
                "fee": 30,  
                "description": "Something tangy",  
                "transaction_number": "HL207-321-1433",  
                "created_at": "2012-10-29T15:57:13.015164Z",  
                "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/holds/HL7BWW1RurPQNwbn1ov1tPMg",  
                "expires_at": "2012-10-30T22:57:13.006732Z",  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:57:12.991263Z",  
                    "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/cards/CCfa17f09a221b11e2882580ee7316ae44",  
                    "id": "CCfa17f09a221b11e2882580ee7316ae44",  
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
                "id": "HL7BWW1RurPQNwbn1ov1tPMg" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP7BJh7JZkeboYEuMIAumJIU/accounts/AC7BTywxMcR9edl4q22Xq9kE/holds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:16.375685Z",  
            "uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7FJh0V4yvX0wcnr9j5s2uE",  
            "credits_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/cards" 
        },  
        "fee": 30,  
        "description": "Something really tasty",  
        "transaction_number": "HL496-660-1480",  
        "created_at": "2012-10-29T15:57:16.417412Z",  
        "uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/holds/HL7FMaCEnbU9mWlgfeb71LPC",  
        "expires_at": "2012-10-30T22:57:16.401727Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:57:16.399544Z",  
            "uri": "/v1/marketplaces/TEST-MP7Fz2SeeoED9KgG0B4XqRs8/accounts/AC7FJh0V4yvX0wcnr9j5s2uE/cards/CCfc2000da221b11e2af2880ee7316ae44",  
            "id": "CCfc2000da221b11e2af2880ee7316ae44",  
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
        "id": "HL7FMaCEnbU9mWlgfeb71LPC" 
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
        "hold_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/holds/HL7HJjzGhRudKdt3sEOyJMJC" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:18.111971Z",  
            "uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7HGlDmsfCfQO5phRB0Lxxq",  
            "credits_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/debits/WD7HO5ee2rQttU8TxfxgZ0oY/refunds",  
        "created_at": "2012-10-29T15:57:18.234730Z",  
        "transaction_number": "W282-513-3210",  
        "uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/debits/WD7HO5ee2rQttU8TxfxgZ0oY",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:57:18.136638Z",  
            "uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/cards/CCfd291098221b11e2a2b180ee7316ae44",  
            "id": "CCfd291098221b11e2a2b180ee7316ae44",  
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
            "created_at": "2012-10-29T15:57:18.154659Z",  
            "uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/holds/HL7HJjzGhRudKdt3sEOyJMJC",  
            "expires_at": "2012-10-30T22:57:18.138886Z",  
            "transaction_number": "HL279-775-6306",  
            "amount": 1233,  
            "meta": {},  
            "is_void": false,  
            "account_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq",  
            "source_uri": "/v1/marketplaces/TEST-MP7Hw2YP4tCcbHpSEpvDVzI8/accounts/AC7HGlDmsfCfQO5phRB0Lxxq/cards/CCfd291098221b11e2a2b180ee7316ae44",  
            "id": "HL7HJjzGhRudKdt3sEOyJMJC" 
        },  
        "id": "WD7HO5ee2rQttU8TxfxgZ0oY",  
        "available_at": "2012-10-29T22:57:18.221749Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/holds",  
            "name": null,  
            "roles": [ 
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:21.687872Z",  
            "uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/transactions",  
            "email_address": "email.9@y.com",  
            "id": "AC7LHI0z9iokojtndpOaGX2c",  
            "credits_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/cards" 
        },  
        "fee": 30,  
        "description": "Something sour",  
        "transaction_number": "HL214-162-5216",  
        "created_at": "2012-10-29T15:57:21.726455Z",  
        "uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/holds/HL7LKnWYRB1oVWBhHnroesZu",  
        "expires_at": "2012-10-30T22:57:21.710874Z",  
        "source": { 
            "expiration_month": 1,  
            "hash": null,  
            "last_four": "1111",  
            "expiration_year": 2015,  
            "created_at": "2012-10-29T15:57:21.708634Z",  
            "uri": "/v1/marketplaces/TEST-MP7LxVhRRJjOMUc1STPeF09u/accounts/AC7LHI0z9iokojtndpOaGX2c/cards/CCff4a2024221b11e2948780ee7316ae44",  
            "id": "CCff4a2024221b11e2948780ee7316ae44",  
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
        "id": "HL7LKnWYRB1oVWBhHnroesZu" 
    } 
 

