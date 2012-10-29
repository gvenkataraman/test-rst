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
            "holds_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:55:57.120738Z",  
            "uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3g6Bn7NkWVK2H1OcruXr92",  
            "credits_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/debits/WD3gdfnvY0h7w8cnGUbHSh5G/refunds",  
        "created_at": "2012-10-29T14:55:57.223184Z",  
        "transaction_number": "W518-581-4776",  
        "uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/debits/WD3gdfnvY0h7w8cnGUbHSh5G",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:55:57.117888Z",  
            "uri": "/v1/marketplaces/TEST-MP3g1y32ZyaiY9IBWPfELjxi/accounts/AC3g6Bn7NkWVK2H1OcruXr92/bank_accounts/BA3g6oAuxP768EoDRgPBgxZa",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA3g6oAuxP768EoDRgPBgxZa" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD3gdfnvY0h7w8cnGUbHSh5G",  
        "available_at": "2012-10-29T21:55:57.215478Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:55:58.391650Z",  
            "uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3hxdkWx4EkBS4J6fIbxK2E",  
            "credits_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/debits/WD3hCR3Lakj2q0JPhgZD6VCc/refunds",  
        "created_at": "2012-10-29T14:55:58.483327Z",  
        "transaction_number": "W437-600-2209",  
        "uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/debits/WD3hCR3Lakj2q0JPhgZD6VCc",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:55:58.387514Z",  
            "uri": "/v1/marketplaces/TEST-MP3hpSU9eF8yjYiGls5uU6Ww/accounts/AC3hxdkWx4EkBS4J6fIbxK2E/bank_accounts/BA3hwV2h41Yu7QEyl6WkpdVa",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA3hwV2h41Yu7QEyl6WkpdVa" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD3hCR3Lakj2q0JPhgZD6VCc",  
        "available_at": "2012-10-29T21:55:58.473297Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:55:59.674481Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC3iYFI6lljRQHWVRo6G467W",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T14:55:59.690684Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/cards/CC6ca1868e221311e2bbfa80ee7316ae44",  
                    "id": "CC6ca1868e221311e2bbfa80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-29T14:55:59.725473Z",  
                "transaction_number": "W851-697-3367",  
                "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j0HuiP6oEjAjbxZMjAyos",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j0HuiP6oEjAjbxZMjAyos/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-29T14:55:59.732400Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/holds/HL3j2C7GemOwruikNiF6rBu4",  
                    "expires_at": "2012-11-05T21:55:59.701929Z",  
                    "transaction_number": "HL622-690-9952",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W",  
                    "source_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYFI6lljRQHWVRo6G467W/cards/CC6ca1868e221311e2bbfa80ee7316ae44",  
                    "id": "HL3j2C7GemOwruikNiF6rBu4" 
                },  
                "id": "WD3j0HuiP6oEjAjbxZMjAyos",  
                "available_at": "2012-10-29T21:55:59.702709Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:55:59.673225Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC3iYAh9Tlbu2Yjr1GJ1eVus",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T14:55:59.668830Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/bank_accounts/BA3iYgKTMzDXYbXh2JeuGzI0",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA3iYgKTMzDXYbXh2JeuGzI0" 
                },  
                "created_at": "2012-10-29T14:55:59.771530Z",  
                "transaction_number": "W045-605-4955",  
                "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j4eNz5T3QZCcPBnR4wYXG",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j4eNz5T3QZCcPBnR4wYXG/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD3j4eNz5T3QZCcPBnR4wYXG",  
                "available_at": "2012-10-29T21:55:59.755105Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:55:59.673225Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC3iYAh9Tlbu2Yjr1GJ1eVus",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T14:55:59.668830Z",  
                    "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/accounts/AC3iYAh9Tlbu2Yjr1GJ1eVus/bank_accounts/BA3iYgKTMzDXYbXh2JeuGzI0",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA3iYgKTMzDXYbXh2JeuGzI0" 
                },  
                "created_at": "2012-10-29T14:55:59.772289Z",  
                "transaction_number": "W919-879-4980",  
                "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j4mvLUG5flXRQoZ6Kffla",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits/WD3j4mvLUG5flXRQoZ6Kffla/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD3j4mvLUG5flXRQoZ6Kffla",  
                "available_at": "2012-10-29T21:55:59.756802Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP3iReYduTSgBs52QhrYQEja/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:02.519019Z",  
            "uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3mb25YHTX5235p42iGt4Gg",  
            "credits_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/debits/WD3mgr23mcWkD5OjyNm4o1OA/refunds",  
        "created_at": "2012-10-29T14:56:02.612500Z",  
        "transaction_number": "W097-678-3997",  
        "uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/debits/WD3mgr23mcWkD5OjyNm4o1OA",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:56:02.515268Z",  
            "uri": "/v1/marketplaces/TEST-MP3m5oyGHGwh293ucuweCv6A/accounts/AC3mb25YHTX5235p42iGt4Gg/bank_accounts/BA3maLjoBV0VK8Dx7JrK9Q20",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA3maLjoBV0VK8Dx7JrK9Q20" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD3mgr23mcWkD5OjyNm4o1OA",  
        "available_at": "2012-10-29T21:56:02.597316Z" 
    } 
 

