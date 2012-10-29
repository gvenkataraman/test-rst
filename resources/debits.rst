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
            "holds_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:57.936019Z",  
            "uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7kZqzc16hmQDt80LhKe60s",  
            "credits_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/debits/WD7l8JneptvF7BwzEPJwAJve/refunds",  
        "created_at": "2012-10-29T15:56:58.080715Z",  
        "transaction_number": "W655-673-1550",  
        "uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/debits/WD7l8JneptvF7BwzEPJwAJve",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:56:57.931587Z",  
            "uri": "/v1/marketplaces/TEST-MP7kS33Op0dQovzomFVIgQkY/accounts/AC7kZqzc16hmQDt80LhKe60s/bank_accounts/BA7kZ6YnnBa4KJSUZRZtDY2w",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA7kZ6YnnBa4KJSUZRZtDY2w" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD7l8JneptvF7BwzEPJwAJve",  
        "available_at": "2012-10-29T22:56:58.068651Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:59.479607Z",  
            "uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7mJ3PALjk4Na0qYxyIK77C",  
            "credits_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/debits/WD7mNQK8JbClTBNlwyTC4e4Q/refunds",  
        "created_at": "2012-10-29T15:56:59.557922Z",  
        "transaction_number": "W779-636-6781",  
        "uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/debits/WD7mNQK8JbClTBNlwyTC4e4Q",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:56:59.475313Z",  
            "uri": "/v1/marketplaces/TEST-MP7mBQUFNsV0sHRRhZISd7c8/accounts/AC7mJ3PALjk4Na0qYxyIK77C/bank_accounts/BA7mIL0dJVV1AEByA0cPw8uM",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA7mIL0dJVV1AEByA0cPw8uM" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD7mNQK8JbClTBNlwyTC4e4Q",  
        "available_at": "2012-10-29T22:56:59.548807Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:01.021742Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC7osBIgugZxiDkAotqMJgTq",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-29T15:57:01.038070Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/cards/CCf2f6ca3e221b11e2a86c80ee7316ae44",  
                    "id": "CCf2f6ca3e221b11e2a86c80ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-29T15:57:01.073087Z",  
                "transaction_number": "W194-098-3342",  
                "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7ouEBTmDYE9OC3re5FRKdu",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7ouEBTmDYE9OC3re5FRKdu/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-29T15:57:01.080234Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/holds/HL7owzAb4OkTF4OBxa4dNiKg",  
                    "expires_at": "2012-11-05T22:57:01.049459Z",  
                    "transaction_number": "HL034-143-4497",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq",  
                    "source_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7osBIgugZxiDkAotqMJgTq/cards/CCf2f6ca3e221b11e2a86c80ee7316ae44",  
                    "id": "HL7owzAb4OkTF4OBxa4dNiKg" 
                },  
                "id": "WD7ouEBTmDYE9OC3re5FRKdu",  
                "available_at": "2012-10-29T22:57:01.050242Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:01.020594Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7oswusnGsCut6ZHZtNoKFK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:57:01.016151Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/bank_accounts/BA7oscPT4DskY7H652lCFRJi",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA7oscPT4DskY7H652lCFRJi" 
                },  
                "created_at": "2012-10-29T15:57:01.120388Z",  
                "transaction_number": "W465-870-7218",  
                "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7oygSBXQOahLJWmoPp5XKI",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7oygSBXQOahLJWmoPp5XKI/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD7oygSBXQOahLJWmoPp5XKI",  
                "available_at": "2012-10-29T22:57:01.103779Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:01.020594Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7oswusnGsCut6ZHZtNoKFK",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:57:01.016151Z",  
                    "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/accounts/AC7oswusnGsCut6ZHZtNoKFK/bank_accounts/BA7oscPT4DskY7H652lCFRJi",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA7oscPT4DskY7H652lCFRJi" 
                },  
                "created_at": "2012-10-29T15:57:01.121124Z",  
                "transaction_number": "W980-942-1661",  
                "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7oyoBm1qXpHTFc6A3DoUgQ",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits/WD7oyoBm1qXpHTFc6A3DoUgQ/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD7oyoBm1qXpHTFc6A3DoUgQ",  
                "available_at": "2012-10-29T22:57:01.105501Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP7ol9Xo6J9SopGnmbvwZXGQ/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:04.408735Z",  
            "uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7sgN2N8Df1pnCCpZgvaRNO",  
            "credits_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/debits/WD7slq7wdbUiGSrlcX3KxR9a/refunds",  
        "created_at": "2012-10-29T15:57:04.489288Z",  
        "transaction_number": "W592-859-4097",  
        "uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/debits/WD7slq7wdbUiGSrlcX3KxR9a",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:57:04.404485Z",  
            "uri": "/v1/marketplaces/TEST-MP7s9rxwfY17yXmGvewDaXpG/accounts/AC7sgN2N8Df1pnCCpZgvaRNO/bank_accounts/BA7sgu3vcAZDzYnhxIli0jB2",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA7sgu3vcAZDzYnhxIli0jB2" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD7slq7wdbUiGSrlcX3KxR9a",  
        "available_at": "2012-10-29T22:57:04.475731Z" 
    } 
 

