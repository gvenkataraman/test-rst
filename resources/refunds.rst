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
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/refunds 
    POST /v1/marketplaces/(marketplace:marketplace)/refunds 
 

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
        "debit_uri": "/v1/marketplaces/TEST-MP7LYyN6rh1oxCa5IM0M6ygb/debits/WD7M92mK9O3maRG3H6IO8Wcj",  
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
            "holds_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:11:19.091750Z",  
            "uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC12aSpCPeeZhQ7TqnbTcZR",  
            "credits_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T00:11:19.273389Z",  
        "uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/refunds/RF1eq6pRm1SqFaNqa8k6t9h",  
        "transaction_number": "RF604-880-1178",  
        "amount": 1234,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W158-423-3947",  
            "source_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/accounts/AC12aSpCPeeZhQ7TqnbTcZR/bank_accounts/BA11QAaF8QCXl2olwXJo1JF",  
            "created_at": "2012-10-30T00:11:19.191407Z",  
            "uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/debits/WD17YSVyB6rMR5WXFZiaRqP",  
            "refunds_uri": "/v1/marketplaces/TEST-MPUiPLWucSOFR8x79PFHTZ/debits/WD17YSVyB6rMR5WXFZiaRqP/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD17YSVyB6rMR5WXFZiaRqP",  
            "available_at": "2012-10-30T07:11:19.175782Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF1eq6pRm1SqFaNqa8k6t9h" 
    } 
 

Retrieve a Refund
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/refunds/(refund:refund) 
    GET /v1/marketplaces/(marketplace:marketplace)/refunds/(refund:refund) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:11:20.730575Z",  
            "uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2SsfU1BGkY6cYfBqn1GzV",  
            "credits_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T00:11:20.838601Z",  
        "uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/refunds/RF2Yla7CfPRN8RlzzRxsn0n",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W853-480-9810",  
            "source_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/accounts/AC2SsfU1BGkY6cYfBqn1GzV/bank_accounts/BA2S8PxxyxeySJsF1FYYOkz",  
            "created_at": "2012-10-30T00:11:20.833286Z",  
            "uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/debits/WD2YdevPEE4UkEj9tbUX78L",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2KSjBk5q8SBCBV5w2l4oH/debits/WD2YdevPEE4UkEj9tbUX78L/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD2YdevPEE4UkEj9tbUX78L",  
            "available_at": "2012-10-30T07:11:20.813943Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF2Yla7CfPRN8RlzzRxsn0n" 
    } 
 

List All refunds
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/refunds 
    GET /v1/marketplaces/(marketplace:marketplace)/refunds 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/refunds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:11:22.293482Z",  
                    "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4DrpBxm2eaRhoOknOtI55",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/cards" 
                },  
                "fee": -15,  
                "description": "abc123",  
                "created_at": "2012-10-30T00:11:22.405118Z",  
                "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/refunds/RF4JG06SRpejhMckkuZmF9h",  
                "transaction_number": "RF111-222-3333",  
                "amount": 431,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 15,  
                    "description": "abc123",  
                    "transaction_number": "W940-073-6302",  
                    "source_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/bank_accounts/BA4D7BVaPSoChpp7vE9HgLF",  
                    "created_at": "2012-10-30T00:11:22.402056Z",  
                    "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/debits/WD4Jy6nr29W8Hu0dfKjVMLV",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/debits/WD4Jy6nr29W8Hu0dfKjVMLV/refunds",  
                    "amount": 431,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD4Jy6nr29W8Hu0dfKjVMLV",  
                    "available_at": "2012-10-30T07:11:22.381893Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF4JG06SRpejhMckkuZmF9h" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:11:22.293482Z",  
                    "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4DrpBxm2eaRhoOknOtI55",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/cards" 
                },  
                "fee": -43,  
                "description": "abc123",  
                "created_at": "2012-10-30T00:11:22.404592Z",  
                "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/refunds/RF4Jp3BSdCKottRUi4J6QV5",  
                "transaction_number": "RF111-222-3333",  
                "amount": 1254,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 43,  
                    "description": "abc123",  
                    "transaction_number": "W697-896-3059",  
                    "source_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/accounts/AC4DrpBxm2eaRhoOknOtI55/bank_accounts/BA4D7BVaPSoChpp7vE9HgLF",  
                    "created_at": "2012-10-30T00:11:22.401522Z",  
                    "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/debits/WD4JgKWPxZ9Tc0sRep7an3J",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/debits/WD4JgKWPxZ9Tc0sRep7an3J/refunds",  
                    "amount": 1254,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD4JgKWPxZ9Tc0sRep7an3J",  
                    "available_at": "2012-10-30T07:11:22.377930Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF4Jp3BSdCKottRUi4J6QV5" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/refunds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4xnIkbPKDilIckaYlINDt/refunds?limit=10&offset=0" 
    } 
 

Update a Refund
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/refunds 
    GET /v1/marketplaces/(marketplace:marketplace)/refunds 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:11:25.410277Z",  
            "uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC88MeSyvDoNf6J1kT42etR",  
            "credits_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/cards" 
        },  
        "fee": -43,  
        "description": "my new description",  
        "created_at": "2012-10-30T00:11:25.522209Z",  
        "uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/refunds/RF8eGBaeh4HR3LB4NpXR6kH",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W356-489-0947",  
            "source_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/accounts/AC88MeSyvDoNf6J1kT42etR/bank_accounts/BA88sgK2xvnxZ81UcBwIxrR",  
            "created_at": "2012-10-30T00:11:25.517059Z",  
            "uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/debits/WD8eyhHkpKkL6TPBRMw1Bgn",  
            "refunds_uri": "/v1/marketplaces/TEST-MP81b9OmoEeEZWxYe35fTTt/debits/WD8eyhHkpKkL6TPBRMw1Bgn/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD8eyhHkpKkL6TPBRMw1Bgn",  
            "available_at": "2012-10-30T07:11:25.493851Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF8eGBaeh4HR3LB4NpXR6kH" 
    } 
 

