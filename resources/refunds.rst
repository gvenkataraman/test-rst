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
        "debit_uri": "/v1/marketplaces/TEST-MP1TRmbsqDnrlijt6lJ34ZYo/debits/WD1U3gLM9MJejAmLhZ0p7ThO",  
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
            "holds_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:00:03.504382Z",  
            "uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1VTBh4j0ucPopR6EtBiwM4",  
            "credits_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T10:00:03.675378Z",  
        "uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/refunds/RF1W4OW9GQRHhC8B5PdoBxUU",  
        "transaction_number": "RF664-198-8962",  
        "amount": 1234,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W277-249-2128",  
            "source_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/accounts/AC1VTBh4j0ucPopR6EtBiwM4/bank_accounts/BA1VTi1qANSdDKbapGgn5fjC",  
            "created_at": "2012-10-30T10:00:03.582240Z",  
            "uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/debits/WD1VY8zpnRWRS17rgHOSb9U8",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1VMgGCIkH1rtVtlpgS0Fak/debits/WD1VY8zpnRWRS17rgHOSb9U8/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD1VY8zpnRWRS17rgHOSb9U8",  
            "available_at": "2012-10-30T17:00:03.569958Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF1W4OW9GQRHhC8B5PdoBxUU" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:00:05.121882Z",  
            "uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1XIosATzZx2FZKmVT29YWg",  
            "credits_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-30T10:00:05.211383Z",  
        "uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/refunds/RF1XNnjLY6PCQ0FFdB5HN3wM",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W085-012-4098",  
            "source_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/accounts/AC1XIosATzZx2FZKmVT29YWg/bank_accounts/BA1XI4dzmEn3noLsuwkVcSvW",  
            "created_at": "2012-10-30T10:00:05.207564Z",  
            "uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/debits/WD1XNgwVG6mNZX2rw5lJnw4k",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1XBMACECXJjRbVRyoDn1qY/debits/WD1XNgwVG6mNZX2rw5lJnw4k/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD1XNgwVG6mNZX2rw5lJnw4k",  
            "available_at": "2012-10-30T17:00:05.192367Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF1XNnjLY6PCQ0FFdB5HN3wM" 
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
        "first_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/refunds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:00:06.653323Z",  
                    "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1ZrbwfFSxIy5jkicmSH5Zy",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/cards" 
                },  
                "fee": -43,  
                "description": "abc123",  
                "created_at": "2012-10-30T10:00:06.759731Z",  
                "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/refunds/RF1ZwE3SOBmQyJgKMVIVjtgU",  
                "transaction_number": "RF111-222-3333",  
                "amount": 1254,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 43,  
                    "description": "abc123",  
                    "transaction_number": "W041-379-7801",  
                    "source_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/bank_accounts/BA1ZqRM3mvHWT48TK9tQL4Ak",  
                    "created_at": "2012-10-30T10:00:06.751945Z",  
                    "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/debits/WD1Zwxnto6qis0MqqnHE05uc",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/debits/WD1Zwxnto6qis0MqqnHE05uc/refunds",  
                    "amount": 1254,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD1Zwxnto6qis0MqqnHE05uc",  
                    "available_at": "2012-10-30T17:00:06.730656Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF1ZwE3SOBmQyJgKMVIVjtgU" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:00:06.653323Z",  
                    "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1ZrbwfFSxIy5jkicmSH5Zy",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/cards" 
                },  
                "fee": -15,  
                "description": "abc123",  
                "created_at": "2012-10-30T10:00:06.760425Z",  
                "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/refunds/RF1ZwRI7VlSgfXLfdT0Cakni",  
                "transaction_number": "RF111-222-3333",  
                "amount": 431,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 15,  
                    "description": "abc123",  
                    "transaction_number": "W864-348-5021",  
                    "source_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/accounts/AC1ZrbwfFSxIy5jkicmSH5Zy/bank_accounts/BA1ZqRM3mvHWT48TK9tQL4Ak",  
                    "created_at": "2012-10-30T10:00:06.752706Z",  
                    "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/debits/WD1ZwLJWGdSOFXSNOd4mF15O",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/debits/WD1ZwLJWGdSOFXSNOd4mF15O/refunds",  
                    "amount": 431,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD1ZwLJWGdSOFXSNOd4mF15O",  
                    "available_at": "2012-10-30T17:00:06.733895Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF1ZwRI7VlSgfXLfdT0Cakni" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/refunds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1Zl5e8KEfno39OlXW2shIo/refunds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:00:09.896706Z",  
            "uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC235m5aXtnUymSGR3Za60de",  
            "credits_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/cards" 
        },  
        "fee": -43,  
        "description": "my new description",  
        "created_at": "2012-10-30T10:00:10.004619Z",  
        "uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/refunds/RF23aTJ6RGXYwhokO9CnLnLe",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W647-424-5952",  
            "source_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/accounts/AC235m5aXtnUymSGR3Za60de/bank_accounts/BA2352Y73WNClaPRhnoRlAZ6",  
            "created_at": "2012-10-30T10:00:10.002966Z",  
            "uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/debits/WD23aMvsE4amDiF3RD2vLRkw",  
            "refunds_uri": "/v1/marketplaces/TEST-MP22Yr3sD28xjsIQ361FBeMA/debits/WD23aMvsE4amDiF3RD2vLRkw/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD23aMvsE4amDiF3RD2vLRkw",  
            "available_at": "2012-10-30T17:00:09.975165Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF23aTJ6RGXYwhokO9CnLnLe" 
    } 
 

