Debits
=======

- `Debit an Account`_
- `Retrieve a Debit`_
- `List All Debits`_
- `Update a Debit`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the debit. 
 
``amount`` 
    **integer**. The amount of the debit. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this debit. 
 
``description`` 
    **string**. Free-text description of the debit. 
 
``hold`` 
    **object**. The original hold for this debit, if this debit was to a card. 
    If the debit was to a bank account, this field will be null.  
 
``refunds_uri`` 
    **string**. URI for any partial or complete refunds of this debit. 
 
``appears_on_statement_as`` 
    **string**. The text that will appear on the buyer's statement. 
 
``account`` 
    **object**. The account to which this debit is associated. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    debit was created. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``available_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    transaction is guaranteed to clear. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``source`` 
    **object**. The funding source (card or bank account) for this debit.  
 

Debit an Account
----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/debits 
    POST /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold)/debits 
    POST /v1/marketplaces/(marketplace:marketplace)/debits 
 

Request
~~~~~~~

``amount`` 
    *optional* **integer** or **null**. If the resolving URI references a hold then this is hold amount. You can 
    always capture less than the hold amount (e.g. a partial capture). 
    Otherwise its the maximum per debit amount for your marketplace. Value must be >= the minimum per debit ``amount`` for *your* 
    marketplace. Value must be <= the maximum per debit ``amount`` for *your* 
    marketplace. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``description`` 
    *optional* **string** or **null**.  
 
``merchant_uri`` 
    *optional* **string** or **null**. URI referencing the merchant account on behalf of whom the 
    debit is being done. This is different from marketplace. 
    In a peer-to-peer transaction, there are three parties: 
 
    1. Marketplace 
    2. Seller/Service provider 
    3. Buyer 
 
    This merchant account represents 2. 
 
``hold_uri`` 
    *optional* **string** or **null**. If no ``hold`` is provided one my be generated and captured if the 
    source is a card. 
 
``source_uri`` 
    *optional* **string** or **null**.  
 
``bank_account_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 1234 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:03.376505Z",  
            "uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2UuGKj39HUBUjAdIkkH9WI",  
            "credits_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/debits/WD2UCyPTxQVtCiJTMdpLaoO8/refunds",  
        "created_at": "2012-10-29T16:00:03.499205Z",  
        "transaction_number": "W489-416-4323",  
        "uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/debits/WD2UCyPTxQVtCiJTMdpLaoO8",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:00:03.372348Z",  
            "uri": "/v1/marketplaces/TEST-MP2Una9KiG2QDyeD13pcfUNu/accounts/AC2UuGKj39HUBUjAdIkkH9WI/bank_accounts/BA2UuogEbRW1nqwt5G22qHY0",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2UuogEbRW1nqwt5G22qHY0" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD2UCyPTxQVtCiJTMdpLaoO8",  
        "available_at": "2012-10-29T23:00:03.488655Z" 
    } 
 

Retrieve a Debit
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/debits/(debit:debit) 
    GET /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold)/debits/(debit:debit) 
    GET /v1/marketplaces/(marketplace:marketplace)/debits/(debit:debit) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:05.076127Z",  
            "uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2WpdAGyWlXYhWBFvHZKT4M",  
            "credits_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/debits/WD2WtnmhrM2WbPSiUEl8S8Nm/refunds",  
        "created_at": "2012-10-29T16:00:05.143506Z",  
        "transaction_number": "W348-013-5497",  
        "uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/debits/WD2WtnmhrM2WbPSiUEl8S8Nm",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:00:05.072140Z",  
            "uri": "/v1/marketplaces/TEST-MP2WimZbLNpQp2M39lQSRLY8/accounts/AC2WpdAGyWlXYhWBFvHZKT4M/bank_accounts/BA2WoURdahlkrlqnFm6f2nZ2",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2WoURdahlkrlqnFm6f2nZ2" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD2WtnmhrM2WbPSiUEl8S8Nm",  
        "available_at": "2012-10-29T23:00:05.136329Z" 
    } 
 

List All Debits
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/debits 
    GET /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold)/debits 
    GET /v1/marketplaces/(marketplace:marketplace)/debits 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:06.672766Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC2YcxPIjNIGJ6ZQEbq0rqG8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:00:06.689845Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/cards/CC619ee34a221c11e2868e80ee7316ae44",  
                    "id": "CC619ee34a221c11e2868e80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-29T16:00:06.722445Z",  
                "transaction_number": "W381-053-7391",  
                "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YeCS1Khz7as6YxyjZ07vS",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YeCS1Khz7as6YxyjZ07vS/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-29T16:00:06.728077Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/holds/HL2YgkRCl6JMcj7Iqvd4VuKg",  
                    "expires_at": "2012-11-05T23:00:06.700845Z",  
                    "transaction_number": "HL555-330-2279",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8",  
                    "source_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcxPIjNIGJ6ZQEbq0rqG8/cards/CC619ee34a221c11e2868e80ee7316ae44",  
                    "id": "HL2YgkRCl6JMcj7Iqvd4VuKg" 
                },  
                "id": "WD2YeCS1Khz7as6YxyjZ07vS",  
                "available_at": "2012-10-29T23:00:06.701638Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:06.671322Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2YcqGTfj3Mo8CKcSD9M1ve",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:00:06.666387Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/bank_accounts/BA2Yc5ZbrZa0XInyMqkcayCo",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2Yc5ZbrZa0XInyMqkcayCo" 
                },  
                "created_at": "2012-10-29T16:00:06.763608Z",  
                "transaction_number": "W679-447-5895",  
                "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YhJXhnOVC0xvwSYWxB7ak",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YhJXhnOVC0xvwSYWxB7ak/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD2YhJXhnOVC0xvwSYWxB7ak",  
                "available_at": "2012-10-29T23:00:06.747923Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:06.671322Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2YcqGTfj3Mo8CKcSD9M1ve",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:00:06.666387Z",  
                    "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/accounts/AC2YcqGTfj3Mo8CKcSD9M1ve/bank_accounts/BA2Yc5ZbrZa0XInyMqkcayCo",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2Yc5ZbrZa0XInyMqkcayCo" 
                },  
                "created_at": "2012-10-29T16:00:06.764458Z",  
                "transaction_number": "W765-441-4338",  
                "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YhR4LmkLSH4e1XPMZMOZC",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits/WD2YhR4LmkLSH4e1XPMZMOZC/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD2YhR4LmkLSH4e1XPMZMOZC",  
                "available_at": "2012-10-29T23:00:06.749633Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP2Y4OI4eMTBUWduTqd9t0pK/debits?limit=10&offset=0" 
    } 
 

Update a Debit
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/debits 
    GET /v1/marketplaces/(marketplace:marketplace)/holds/(hold:hold)/debits 
    GET /v1/marketplaces/(marketplace:marketplace)/debits 
 

Request
~~~~~~~

``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``description`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "meta": { 
            "my-id": "0987654321" 
        },  
        "description": "my new description" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:10.511834Z",  
            "uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC32wfhqnNzaewcxU0KSI4Ru",  
            "credits_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/debits/WD32C5fU5PLzoG3cVh4UAm1e/refunds",  
        "created_at": "2012-10-29T16:00:10.611183Z",  
        "transaction_number": "W784-819-7287",  
        "uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/debits/WD32C5fU5PLzoG3cVh4UAm1e",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:00:10.507427Z",  
            "uri": "/v1/marketplaces/TEST-MP32oG9fumEulj6IUKFIl0IA/accounts/AC32wfhqnNzaewcxU0KSI4Ru/bank_accounts/BA32vW6BOJ5SASk1IgkFOUEQ",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA32vW6BOJ5SASk1IgkFOUEQ" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD32C5fU5PLzoG3cVh4UAm1e",  
        "available_at": "2012-10-29T23:00:10.596193Z" 
    } 
 

