Refunds
=======

- `Refund an Account`_
- `Retrieve a Refund`_
- `List All Refunds`_
- `Update a Refund`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    refund was issued. 
 
``amount`` 
    **integer**. The amount of the refund. 
 
``fee`` 
    **integer**. The fee reversed by Balanced for this refund. 
 
``description`` 
    **string**. Free-text description of the refund. 
 
``account`` 
    **object**. Account receiving the refund. 
 
``appears_on_statement_as`` 
    **string**. Text that will appear on the statement describing this refund. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``debit`` 
    **object**. The original debit associated with the refund.  
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 

Refund an Account
----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts/(account-id)/refunds 
    POST /v1/marketplaces/(marketplace-id)/refunds 
 

Request
~~~~~~~

``amount`` 
    *optional* **integer** or **null**. Value must be **>=** ``1``. Value must be <= the remaining un-refunded amount on the original 
    ``debit``. 
 
``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``debit_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "debit_uri": "/v1/marketplaces/TEST-MP6f7GfuJCJZ8EH173A3CM3a/debits/WD6fjmHxZEur07AjXeStGKs4",  
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
            "holds_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:11:12.212358Z",  
            "uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6gWu2y1F7dCvBbbUyeREWw",  
            "credits_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T10:11:12.384604Z",  
        "uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/refunds/RF6h7Ns94qKPBnwduXP3AEOo",  
        "transaction_number": "RF553-361-9697",  
        "amount": 1234,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W088-167-7440",  
            "source_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/accounts/AC6gWu2y1F7dCvBbbUyeREWw/bank_accounts/BA6gWbrErG8h41gOj2zpC256",  
            "created_at": "2012-10-30T10:11:12.291044Z",  
            "uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/debits/WD6h15e8t5B05qbex5qzY8OU",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6gP9nhhRbkGAKCVryufG4Y/debits/WD6h15e8t5B05qbex5qzY8OU/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD6h15e8t5B05qbex5qzY8OU",  
            "available_at": "2012-10-30T17:11:12.278759Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF6h7Ns94qKPBnwduXP3AEOo" 
    } 
 

Retrieve a Refund
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/refunds/(refund-id) 
    GET /v1/marketplaces/(marketplace-id)/refunds/(refund-id) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:11:13.695994Z",  
            "uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6iBWqsJdGu0XWTdW6xWWbO",  
            "credits_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T10:11:13.800917Z",  
        "uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/refunds/RF6iHGzSfB2ZDmncTo5Onsr2",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W325-933-3482",  
            "source_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/accounts/AC6iBWqsJdGu0XWTdW6xWWbO/bank_accounts/BA6iBCYdUoASTwyxkkrcPGsc",  
            "created_at": "2012-10-30T10:11:13.795897Z",  
            "uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/debits/WD6iHyJ5C7ZUiywkYvddcjPe",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6iuCv1Ta5gN6uWK57uV4fq/debits/WD6iHyJ5C7ZUiywkYvddcjPe/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD6iHyJ5C7ZUiywkYvddcjPe",  
            "available_at": "2012-10-30T17:11:13.777335Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF6iHGzSfB2ZDmncTo5Onsr2" 
    } 
 

List All refunds
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/refunds 
    GET /v1/marketplaces/(marketplace-id)/refunds 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/refunds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:11:15.225863Z",  
                    "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6kkCJXptp7ZaKAOdC38CWM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/cards" 
                },  
                "fee": -43,  
                "description": "abc123",  
                "created_at": "2012-10-30T10:11:15.341304Z",  
                "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/refunds/RF6kqrpKIg2etGaYD9r6YC7q",  
                "transaction_number": "RF111-222-3333",  
                "amount": 1254,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 43,  
                    "description": "abc123",  
                    "transaction_number": "W338-060-7722",  
                    "source_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/bank_accounts/BA6kkjdHiHRBUooqPg7wAhak",  
                    "created_at": "2012-10-30T10:11:15.332517Z",  
                    "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/debits/WD6kqjE3QjGMdLOoGMkOpVPK",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/debits/WD6kqjE3QjGMdLOoGMkOpVPK/refunds",  
                    "amount": 1254,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD6kqjE3QjGMdLOoGMkOpVPK",  
                    "available_at": "2012-10-30T17:11:15.308248Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF6kqrpKIg2etGaYD9r6YC7q" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:11:15.225863Z",  
                    "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6kkCJXptp7ZaKAOdC38CWM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/cards" 
                },  
                "fee": -15,  
                "description": "abc123",  
                "created_at": "2012-10-30T10:11:15.341995Z",  
                "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/refunds/RF6kqH7jZc8p9hSIsVcjkTl2",  
                "transaction_number": "RF111-222-3333",  
                "amount": 431,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 15,  
                    "description": "abc123",  
                    "transaction_number": "W657-822-3494",  
                    "source_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/accounts/AC6kkCJXptp7ZaKAOdC38CWM/bank_accounts/BA6kkjdHiHRBUooqPg7wAhak",  
                    "created_at": "2012-10-30T10:11:15.333252Z",  
                    "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/debits/WD6kqA1YXQNyHSdbaog5vU4k",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/debits/WD6kqA1YXQNyHSdbaog5vU4k/refunds",  
                    "amount": 431,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD6kqA1YXQNyHSdbaog5vU4k",  
                    "available_at": "2012-10-30T17:11:15.311942Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF6kqH7jZc8p9hSIsVcjkTl2" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/refunds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP6kdf7BH4HtJVrISAyLuxsU/refunds?limit=10&offset=0" 
    } 
 

Update a Refund
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/refunds 
    GET /v1/marketplaces/(marketplace-id)/refunds 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:11:18.417838Z",  
            "uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6nVd9vxZstNe83zaicK50w",  
            "credits_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/cards" 
        },  
        "fee": -43,  
        "description": "my new description",  
        "created_at": "2012-10-30T10:11:18.529011Z",  
        "uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/refunds/RF6o0Wr2AJAtMTe9hiCoIieU",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W878-704-0081",  
            "source_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/accounts/AC6nVd9vxZstNe83zaicK50w/bank_accounts/BA6nUTKKMjGWzlrgOktutfb6",  
            "created_at": "2012-10-30T10:11:18.525763Z",  
            "uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/debits/WD6o0OB3Oseb2KLDMhHDqaQ4",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6nNS3Y7mjESarH0gr78Njm/debits/WD6o0OB3Oseb2KLDMhHDqaQ4/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD6o0OB3Oseb2KLDMhHDqaQ4",  
            "available_at": "2012-10-30T17:11:18.498981Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF6o0Wr2AJAtMTe9hiCoIieU" 
    } 
 

