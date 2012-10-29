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
        "debit_uri": "/v1/marketplaces/TEST-MP3boUAqloMiEuP9HDFIATzK/debits/WD3bBiPAqmJyELneHBaLR3a4",  
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
            "holds_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:50:26.700168Z",  
            "uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3drrJXD1zSrDQPOoD2bzQU",  
            "credits_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-29T16:50:26.885630Z",  
        "uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/refunds/RF3dDMw92fIX0LmfVFsmdbww",  
        "transaction_number": "RF381-112-7045",  
        "amount": 1234,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W348-177-5977",  
            "source_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/accounts/AC3drrJXD1zSrDQPOoD2bzQU/bank_accounts/BA3dr9ib6vKtVnYyZofGZvms",  
            "created_at": "2012-10-29T16:50:26.798160Z",  
            "uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/debits/WD3dx5GZ5h5LmUsk1NigqM7y",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3dk6DClcKgVUM6PCO6HgWM/debits/WD3dx5GZ5h5LmUsk1NigqM7y/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD3dx5GZ5h5LmUsk1NigqM7y",  
            "available_at": "2012-10-29T23:50:26.781923Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF3dDMw92fIX0LmfVFsmdbww" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:50:28.399256Z",  
            "uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3flVzM7486B74d0djlEp3S",  
            "credits_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/cards" 
        },  
        "fee": -43,  
        "description": "abc123",  
        "created_at": "2012-10-29T16:50:28.483388Z",  
        "uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/refunds/RF3fqLMQBegns1N50BM5FOde",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": {},  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W952-962-6422",  
            "source_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/accounts/AC3flVzM7486B74d0djlEp3S/bank_accounts/BA3flBZe5XzK26C7sC0mmCag",  
            "created_at": "2012-10-29T16:50:28.481468Z",  
            "uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/debits/WD3fqGoQXAkcu4AUn6gv6nli",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3fetCiCTOPL6gkLhVZ17A8/debits/WD3fqGoQXAkcu4AUn6gv6nli/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD3fqGoQXAkcu4AUn6gv6nli",  
            "available_at": "2012-10-29T23:50:28.467788Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF3fqLMQBegns1N50BM5FOde" 
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
        "first_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/refunds?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:50:29.988037Z",  
                    "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC3h8IA0K4r35IfIEgHgI484",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/cards" 
                },  
                "fee": -43,  
                "description": "abc123",  
                "created_at": "2012-10-29T16:50:30.089535Z",  
                "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/refunds/RF3hdUctY8ikPZzq5pzrykwQ",  
                "transaction_number": "RF111-222-3333",  
                "amount": 1254,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 43,  
                    "description": "abc123",  
                    "transaction_number": "W547-159-0240",  
                    "source_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/bank_accounts/BA3h8pdWamiNaIS8CkLloCZS",  
                    "created_at": "2012-10-29T16:50:30.080600Z",  
                    "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/debits/WD3hdLKaDcnleHnG1UjMXC9S",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/debits/WD3hdLKaDcnleHnG1UjMXC9S/refunds",  
                    "amount": 1254,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD3hdLKaDcnleHnG1UjMXC9S",  
                    "available_at": "2012-10-29T23:50:30.061326Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF3hdUctY8ikPZzq5pzrykwQ" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:50:29.988037Z",  
                    "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC3h8IA0K4r35IfIEgHgI484",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/cards" 
                },  
                "fee": -15,  
                "description": "abc123",  
                "created_at": "2012-10-29T16:50:30.090101Z",  
                "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/refunds/RF3heaTYiAwR30x03cE5f6QY",  
                "transaction_number": "RF111-222-3333",  
                "amount": 431,  
                "meta": {},  
                "debit": { 
                    "hold_uri": null,  
                    "fee": 15,  
                    "description": "abc123",  
                    "transaction_number": "W879-321-0701",  
                    "source_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/accounts/AC3h8IA0K4r35IfIEgHgI484/bank_accounts/BA3h8pdWamiNaIS8CkLloCZS",  
                    "created_at": "2012-10-29T16:50:30.081103Z",  
                    "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/debits/WD3he3qvxAuuRz4CeyKKNxje",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/debits/WD3he3qvxAuuRz4CeyKKNxje/refunds",  
                    "amount": 431,  
                    "meta": {},  
                    "appears_on_statement_as": "PND*TESTS",  
                    "id": "WD3he3qvxAuuRz4CeyKKNxje",  
                    "available_at": "2012-10-29T23:50:30.065303Z" 
                },  
                "appears_on_statement_as": "PND*TESTS",  
                "id": "RF3heaTYiAwR30x03cE5f6QY" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/refunds?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP3h1mlrcs0kB0RpTtVfIIXq/refunds?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:50:33.240686Z",  
            "uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC3kNxwOQpyRe9lS1j4vQ8W8",  
            "credits_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/cards" 
        },  
        "fee": -43,  
        "description": "my new description",  
        "created_at": "2012-10-29T16:50:33.350621Z",  
        "uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/refunds/RF3kT0zOruiyiPDoMZ4c4hne",  
        "transaction_number": "RF111-222-3333",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "debit": { 
            "hold_uri": null,  
            "fee": 43,  
            "description": "abc123",  
            "transaction_number": "W076-386-3566",  
            "source_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/accounts/AC3kNxwOQpyRe9lS1j4vQ8W8/bank_accounts/BA3kNfp8LBZ3uAiDD3P5PyFS",  
            "created_at": "2012-10-29T16:50:33.348187Z",  
            "uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/debits/WD3kSSQgwIswi2jMCVS7SjE8",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3kHml0giZc2DNNPlOBsiFu/debits/WD3kSSQgwIswi2jMCVS7SjE8/refunds",  
            "amount": 1254,  
            "meta": {},  
            "appears_on_statement_as": "PND*TESTS",  
            "id": "WD3kSSQgwIswi2jMCVS7SjE8",  
            "available_at": "2012-10-29T23:50:33.318164Z" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "id": "RF3kT0zOruiyiPDoMZ4c4hne" 
    } 
 

