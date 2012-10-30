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
            "holds_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:13.859587Z",  
            "uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6CJolzmjxA9c8aVbaAWHK3",  
            "credits_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/debits/WD6CS4Tl0t5RKF2ZDyxxrOdZ/refunds",  
        "created_at": "2012-10-30T00:10:13.994612Z",  
        "transaction_number": "W844-388-0957",  
        "uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/debits/WD6CS4Tl0t5RKF2ZDyxxrOdZ",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:10:13.855765Z",  
            "uri": "/v1/marketplaces/TEST-MP6CCwFRBjsgyjBQImbzZEpJ/accounts/AC6CJolzmjxA9c8aVbaAWHK3/bank_accounts/BA6CJ6Hnp5VQLrucuQDRtv9h",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6CJ6Hnp5VQLrucuQDRtv9h" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD6CS4Tl0t5RKF2ZDyxxrOdZ",  
        "available_at": "2012-10-30T07:10:13.983479Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:15.843831Z",  
            "uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6EXKPtjkEBRoWE8TyCWmMX",  
            "credits_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/debits/WD6F2NugK6GkWlKvfAxvA9F1/refunds",  
        "created_at": "2012-10-30T00:10:15.925991Z",  
        "transaction_number": "W960-051-1889",  
        "uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/debits/WD6F2NugK6GkWlKvfAxvA9F1",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:10:15.839774Z",  
            "uri": "/v1/marketplaces/TEST-MP6ER8tKkp5OfSBscjmgjGxR/accounts/AC6EXKPtjkEBRoWE8TyCWmMX/bank_accounts/BA6EXt8kxKQFDRRlwn9PdqqD",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6EXt8kxKQFDRRlwn9PdqqD" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD6F2NugK6GkWlKvfAxvA9F1",  
        "available_at": "2012-10-30T07:10:15.916745Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:17.731152Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC6H5mLq6g5wc6Fr0zkIOQcr",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T00:10:17.745940Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/cards/CCdbfa474e226011e28a1080ee7316ae43",  
                    "id": "CCdbfa474e226011e28a1080ee7316ae43",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-30T00:10:17.776115Z",  
                "transaction_number": "W345-922-5677",  
                "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6H7aDPyhZ4caWcRooukJjR",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6H7aDPyhZ4caWcRooukJjR/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-30T00:10:17.782828Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/holds/HL6H8S9Fp8CJlkpzj8zCqnOr",  
                    "expires_at": "2012-11-06T07:10:17.755551Z",  
                    "transaction_number": "HL430-318-1781",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr",  
                    "source_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5mLq6g5wc6Fr0zkIOQcr/cards/CCdbfa474e226011e28a1080ee7316ae43",  
                    "id": "HL6H8S9Fp8CJlkpzj8zCqnOr" 
                },  
                "id": "WD6H7aDPyhZ4caWcRooukJjR",  
                "available_at": "2012-10-30T07:10:17.756231Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:17.730081Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6H5i0ig3PT95sJS88A8Grh",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T00:10:17.726093Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/bank_accounts/BA6H50dN6yLojLL1NNYcuWGv",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA6H50dN6yLojLL1NNYcuWGv" 
                },  
                "created_at": "2012-10-30T00:10:17.819233Z",  
                "transaction_number": "W870-346-1452",  
                "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6HamipMAOmK9M9yuIUAVFh",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6HamipMAOmK9M9yuIUAVFh/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD6HamipMAOmK9M9yuIUAVFh",  
                "available_at": "2012-10-30T07:10:17.803325Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:17.730081Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6H5i0ig3PT95sJS88A8Grh",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T00:10:17.726093Z",  
                    "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/accounts/AC6H5i0ig3PT95sJS88A8Grh/bank_accounts/BA6H50dN6yLojLL1NNYcuWGv",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA6H50dN6yLojLL1NNYcuWGv" 
                },  
                "created_at": "2012-10-30T00:10:17.819944Z",  
                "transaction_number": "W297-309-8100",  
                "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6HasYPd5KUQSgtV2KbUjrZ",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits/WD6HasYPd5KUQSgtV2KbUjrZ/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD6HasYPd5KUQSgtV2KbUjrZ",  
                "available_at": "2012-10-30T07:10:17.805105Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP6GYpjRAlVrq8id7pShY6Nt/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:22.206947Z",  
            "uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6M7sjGoBmgK58HWCGiH391",  
            "credits_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/debits/WD6MdoUORACeAvE0InbHJX6X/refunds",  
        "created_at": "2012-10-30T00:10:22.308844Z",  
        "transaction_number": "W703-553-2671",  
        "uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/debits/WD6MdoUORACeAvE0InbHJX6X",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:10:22.201559Z",  
            "uri": "/v1/marketplaces/TEST-MP6LZctG7FDGRggmnptwn6jF/accounts/AC6M7sjGoBmgK58HWCGiH391/bank_accounts/BA6M73K4kHg1xOFEHuMFlqRt",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6M73K4kHg1xOFEHuMFlqRt" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD6MdoUORACeAvE0InbHJX6X",  
        "available_at": "2012-10-30T07:10:22.292829Z" 
    } 
 

