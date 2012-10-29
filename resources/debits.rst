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
            "holds_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:36.834338Z",  
            "uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2jm9QC9PJ6FHNFEGCXia9e",  
            "credits_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/debits/WD2jvrGSrRktEnEeX3FwH164/refunds",  
        "created_at": "2012-10-29T16:49:36.978526Z",  
        "transaction_number": "W888-182-8582",  
        "uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/debits/WD2jvrGSrRktEnEeX3FwH164",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:36.830042Z",  
            "uri": "/v1/marketplaces/TEST-MP2jeQvmVgba3T1ZX04zcaCo/accounts/AC2jm9QC9PJ6FHNFEGCXia9e/bank_accounts/BA2jlQL9YGwnDQxyUJYkjNl2",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2jlQL9YGwnDQxyUJYkjNl2" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD2jvrGSrRktEnEeX3FwH164",  
        "available_at": "2012-10-29T23:49:36.966734Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:38.381400Z",  
            "uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2l62ziSoL63dWaShou3dxa",  
            "credits_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/debits/WD2laqKjRI6NkvpzHrgq58CU/refunds",  
        "created_at": "2012-10-29T16:49:38.452934Z",  
        "transaction_number": "W118-682-4081",  
        "uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/debits/WD2laqKjRI6NkvpzHrgq58CU",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:38.377197Z",  
            "uri": "/v1/marketplaces/TEST-MP2kYGQTEjVJdegkOjdWyEJe/accounts/AC2l62ziSoL63dWaShou3dxa/bank_accounts/BA2l5JUo0tkexoDZU3AtmuCU",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2l5JUo0tkexoDZU3AtmuCU" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD2laqKjRI6NkvpzHrgq58CU",  
        "available_at": "2012-10-29T23:49:38.444816Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:40.047921Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC2mYfPUhl09ZSuJFJ83YUhS",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T16:49:40.065062Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/cards/CC4de3f154222311e2b28980ee7316ae44",  
                    "id": "CC4de3f154222311e2b28980ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-29T16:49:40.101007Z",  
                "transaction_number": "W444-582-5443",  
                "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n0pFuvbBDJlRwtR8pAtrm",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n0pFuvbBDJlRwtR8pAtrm/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-29T16:49:40.108004Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/holds/HL2n2ljAP9QDZkuSh3itF2Qs",  
                    "expires_at": "2012-11-05T23:49:40.077230Z",  
                    "transaction_number": "HL068-168-9437",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS",  
                    "source_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYfPUhl09ZSuJFJ83YUhS/cards/CC4de3f154222311e2b28980ee7316ae44",  
                    "id": "HL2n2ljAP9QDZkuSh3itF2Qs" 
                },  
                "id": "WD2n0pFuvbBDJlRwtR8pAtrm",  
                "available_at": "2012-10-29T23:49:40.078033Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:40.046761Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2mYaFAdTNj5gYI811HuNYo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:49:40.042259Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/bank_accounts/BA2mXQDXEMldWsirS6TxkH2c",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2mXQDXEMldWsirS6TxkH2c" 
                },  
                "created_at": "2012-10-29T16:49:40.146828Z",  
                "transaction_number": "W496-863-6992",  
                "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n3Yf1BELNj20mtXOCU8mM",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n3Yf1BELNj20mtXOCU8mM/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD2n3Yf1BELNj20mtXOCU8mM",  
                "available_at": "2012-10-29T23:49:40.130717Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:40.046761Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2mYaFAdTNj5gYI811HuNYo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:49:40.042259Z",  
                    "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/accounts/AC2mYaFAdTNj5gYI811HuNYo/bank_accounts/BA2mXQDXEMldWsirS6TxkH2c",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2mXQDXEMldWsirS6TxkH2c" 
                },  
                "created_at": "2012-10-29T16:49:40.147573Z",  
                "transaction_number": "W563-029-9218",  
                "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n45VCI4pCu2SErP8CQmkk",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits/WD2n45VCI4pCu2SErP8CQmkk/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD2n45VCI4pCu2SErP8CQmkk",  
                "available_at": "2012-10-29T23:49:40.132376Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP2mQP6Pi5flli1d4urcEtG4/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:43.560681Z",  
            "uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2qVchxaCgJpXDB9s79dflG",  
            "credits_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/debits/WD2r08f7jHF7NwyLtJ6UEDe4/refunds",  
        "created_at": "2012-10-29T16:49:43.643532Z",  
        "transaction_number": "W724-875-3098",  
        "uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/debits/WD2r08f7jHF7NwyLtJ6UEDe4",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:43.556170Z",  
            "uri": "/v1/marketplaces/TEST-MP2qO7QgDGBilflmSRtlKF8M/accounts/AC2qVchxaCgJpXDB9s79dflG/bank_accounts/BA2qUTd9t3jIvETYiFpDqeOM",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2qUTd9t3jIvETYiFpDqeOM" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD2r08f7jHF7NwyLtJ6UEDe4",  
        "available_at": "2012-10-29T23:49:43.631658Z" 
    } 
 

