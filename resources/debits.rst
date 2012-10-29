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
            "holds_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:20.173342Z",  
            "uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4q9ClOOZjww6VVMtak63BO",  
            "credits_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/debits/WD4qi86wIgJK46VVkFyYgW4A/refunds",  
        "created_at": "2012-10-29T15:11:20.305539Z",  
        "transaction_number": "W381-771-1403",  
        "uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/debits/WD4qi86wIgJK46VVkFyYgW4A",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:20.169167Z",  
            "uri": "/v1/marketplaces/TEST-MP4q2fxAUFXot97Bc5WcLwag/accounts/AC4q9ClOOZjww6VVMtak63BO/bank_accounts/BA4q9jRCIUpMdQSzHQTteVus",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4q9jRCIUpMdQSzHQTteVus" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD4qi86wIgJK46VVkFyYgW4A",  
        "available_at": "2012-10-29T22:11:20.294672Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:21.699769Z",  
            "uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4rS4wvNkiYjD8nL79JPSBu",  
            "credits_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/debits/WD4rWl8HDIlKNGwZjPmLvqL2/refunds",  
        "created_at": "2012-10-29T15:11:21.770863Z",  
        "transaction_number": "W030-435-5183",  
        "uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/debits/WD4rWl8HDIlKNGwZjPmLvqL2",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:21.696860Z",  
            "uri": "/v1/marketplaces/TEST-MP4rKPqe5ppj67QWv3c0Vgt6/accounts/AC4rS4wvNkiYjD8nL79JPSBu/bank_accounts/BA4rRRjBQZgcJ60bvKGv9GC0",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4rRRjBQZgcJ60bvKGv9GC0" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD4rWl8HDIlKNGwZjPmLvqL2",  
        "available_at": "2012-10-29T22:11:21.761766Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:23.323221Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC4tHgRiOuPXhy3PhUMifCDi",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:11:23.339055Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/cards/CC932b25ce221511e2976380ee7316ae44",  
                    "id": "CC932b25ce221511e2976380ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-29T15:11:23.364814Z",  
                "transaction_number": "W448-640-0673",  
                "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tIXP611VM3LTSJOqZM7gU",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tIXP611VM3LTSJOqZM7gU/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-29T15:11:23.370799Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/holds/HL4tKuxS70rn9ssq1nDPxxKk",  
                    "expires_at": "2012-11-05T22:11:23.346267Z",  
                    "transaction_number": "HL931-555-1747",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi",  
                    "source_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHgRiOuPXhy3PhUMifCDi/cards/CC932b25ce221511e2976380ee7316ae44",  
                    "id": "HL4tKuxS70rn9ssq1nDPxxKk" 
                },  
                "id": "WD4tIXP611VM3LTSJOqZM7gU",  
                "available_at": "2012-10-29T22:11:23.346757Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:23.322078Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4tHbJokCHs8WISZOzrqzWI",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:11:23.317761Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/bank_accounts/BA4tGSCB3uG5sDOaTpYpYvMU",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA4tGSCB3uG5sDOaTpYpYvMU" 
                },  
                "created_at": "2012-10-29T15:11:23.406936Z",  
                "transaction_number": "W623-287-1681",  
                "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tLZ6TbhPWxqEOzaEsHoqM",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tLZ6TbhPWxqEOzaEsHoqM/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD4tLZ6TbhPWxqEOzaEsHoqM",  
                "available_at": "2012-10-29T22:11:23.391247Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:23.322078Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4tHbJokCHs8WISZOzrqzWI",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:11:23.317761Z",  
                    "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/accounts/AC4tHbJokCHs8WISZOzrqzWI/bank_accounts/BA4tGSCB3uG5sDOaTpYpYvMU",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA4tGSCB3uG5sDOaTpYpYvMU" 
                },  
                "created_at": "2012-10-29T15:11:23.407677Z",  
                "transaction_number": "W698-554-4529",  
                "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tM58P5XInxSmWAUqClsGM",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits/WD4tM58P5XInxSmWAUqClsGM/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD4tM58P5XInxSmWAUqClsGM",  
                "available_at": "2012-10-29T22:11:23.392969Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4tzQjddubbnpXf3zBS37SI/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:26.920000Z",  
            "uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4xK532HQIrPw4kq0PiDpm4",  
            "credits_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/debits/WD4xPe20aeVHZnuvGaNj2ne4/refunds",  
        "created_at": "2012-10-29T15:11:27.006614Z",  
        "transaction_number": "W625-299-5934",  
        "uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/debits/WD4xPe20aeVHZnuvGaNj2ne4",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:26.915791Z",  
            "uri": "/v1/marketplaces/TEST-MP4xDzB87egARaLusu4a76nO/accounts/AC4xK532HQIrPw4kq0PiDpm4/bank_accounts/BA4xJMtdBrZdoAgrqiNAz8LW",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4xJMtdBrZdoAgrqiNAz8LW" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD4xPe20aeVHZnuvGaNj2ne4",  
        "available_at": "2012-10-29T22:11:26.994057Z" 
    } 
 

