Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_
- `Update a Credit`_

Credit an Account
-----------------

.. code::

    POST /v1/marketplaces/:marketplace_id/accounts/:account_id/credits
    POST /v1/marketplaces/:marketplace_id/credits

Request
~~~~~~~

``amount``: *required* **integer**. 

``description``: *optional* **string**. Sequence of characters.

``meta``: *optional* **object**. Single level mapping from string keys to string values.

``appears_on_statement_as``: *optional* **string**. 

    Text that will appear on the buyer's statement. Characters that can be
    used are limited to:

    - ASCII letters (``a-z`` and ``A-Z``)
    - Digits (``0-9``)
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``)

    Any other characters will be rejected.

``account_uri``: *optional* **string**. 

Exactly one of

    ``destination_uri``: *required* **string**. 

    ``bank_account_uri``: *required* **string**. 

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
        "balance": 0,
        "holds_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:23:27.963113Z",
        "updated_at": "2012-10-26T15:23:27.963116Z",
        "uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8",
        "refunds_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC5XyqGP9DDRQbzlxq5lDma8",
        "credits_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:23:28.039683Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:23:27.959019Z",
        "updated_at": "2012-10-26T15:23:27.959022Z",
        "uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/accounts/AC5XyqGP9DDRQbzlxq5lDma8/bank_accounts/BA5Xy8qPSyBiF3snvbchseJS",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA5Xy8qPSyBiF3snvbchseJS"
      },
      "uri": "/v1/marketplaces/TEST-MP5XroPjIPJsVrkWPKvOtjvu/credits/CR5XCZ3ncmfIUrCHo8ywzVvS",
      "updated_at": "2012-10-26T15:23:28.039685Z",
      "transaction_number": "CR200-065-6735",
      "state": "cleared",
      "meta": {},
      "id": "CR5XCZ3ncmfIUrCHo8ywzVvS",
      "available_at": "2012-10-26T22:23:28.020068Z"
    }



Retrieve a Credit
-----------------

.. code::

    GET /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id
    GET /v1/marketplaces/:marketplace_id/credits/:credit_id

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
        "balance": 0,
        "holds_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:23:29.234973Z",
        "updated_at": "2012-10-26T15:23:29.234975Z",
        "uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ",
        "refunds_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC5YZ7tfMIUXEvbYcjFnZ6oQ",
        "credits_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:23:29.312928Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:23:29.230645Z",
        "updated_at": "2012-10-26T15:23:29.230648Z",
        "uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/accounts/AC5YZ7tfMIUXEvbYcjFnZ6oQ/bank_accounts/BA5YYOd4PJb7p4H2yLtBb8NK",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA5YYOd4PJb7p4H2yLtBb8NK"
      },
      "uri": "/v1/marketplaces/TEST-MP5YRMw1yneUb0zlhprWylRG/credits/CR5Z3I9Koc36AgA2JPTmMabO",
      "updated_at": "2012-10-26T15:23:29.312931Z",
      "transaction_number": "CR812-578-8764",
      "state": "cleared",
      "meta": {},
      "id": "CR5Z3I9Koc36AgA2JPTmMabO",
      "available_at": "2012-10-26T22:23:29.292151Z"
    }



List All Credits
----------------

.. code::

    GET /v1/marketplaces/:marketplace_id/accounts/:account_id/credits
    GET /v1/marketplaces/:marketplace_id/credits

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
      "first_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:23:30.464415Z",
            "updated_at": "2012-10-26T15:23:30.464418Z",
            "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM",
            "refunds_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC60mRbMiCGsg4y9RB4Kc2qM",
            "credits_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:23:30.540157Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:23:30.460923Z",
            "updated_at": "2012-10-26T15:23:30.460926Z",
            "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/bank_accounts/BA60mBMYnq1eII0R68v4xy5K",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA60mBMYnq1eII0R68v4xy5K"
          },
          "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/credits/CR60qVsG3Um3fr0FEYuklmxm",
          "updated_at": "2012-10-26T15:23:30.540160Z",
          "transaction_number": "CR665-836-2086",
          "state": "cleared",
          "meta": {},
          "id": "CR60qVsG3Um3fr0FEYuklmxm",
          "available_at": "2012-10-26T22:23:30.514459Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:23:30.464415Z",
            "updated_at": "2012-10-26T15:23:30.464418Z",
            "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM",
            "refunds_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC60mRbMiCGsg4y9RB4Kc2qM",
            "credits_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:23:30.540905Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:23:30.460923Z",
            "updated_at": "2012-10-26T15:23:30.460926Z",
            "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/accounts/AC60mRbMiCGsg4y9RB4Kc2qM/bank_accounts/BA60mBMYnq1eII0R68v4xy5K",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA60mBMYnq1eII0R68v4xy5K"
          },
          "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/credits/CR60r2So9mvq0qDmRyxKEb6A",
          "updated_at": "2012-10-26T15:23:30.540907Z",
          "transaction_number": "CR124-525-8958",
          "state": "cleared",
          "meta": {},
          "id": "CR60r2So9mvq0qDmRyxKEb6A",
          "available_at": "2012-10-26T22:23:30.523657Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP60hFvyp0Wb5loLOomFd13u/credits?limit=10&offset=0"
    }



Update a Credit
---------------

.. code::

    PUT /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id
    PUT /v1/marketplaces/:marketplace_id/credits/:credit_id

Request
~~~~~~~

``description``: *optional* **string**. Sequence of characters.

``meta``: *optional* **object**. Single level mapping from string keys to string values.

Body
^^^^

.. code:: javascript

    {
      "meta": {
        "my-id": "0987654321"
      }
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
        "balance": 0,
        "holds_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:23:33.047857Z",
        "updated_at": "2012-10-26T15:23:33.047859Z",
        "uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi",
        "refunds_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC63h0pGBfbleRuU9SvXUhNi",
        "credits_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:23:33.111179Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:23:33.043901Z",
        "updated_at": "2012-10-26T15:23:33.043904Z",
        "uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/accounts/AC63h0pGBfbleRuU9SvXUhNi/bank_accounts/BA63gIOYHaTFKFyuSjPRhv6I",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA63gIOYHaTFKFyuSjPRhv6I"
      },
      "uri": "/v1/marketplaces/TEST-MP63bjC11UpXJBzZChvTJ8A4/credits/CR63kmgBK8XAaujaippsY9BG",
      "updated_at": "2012-10-26T15:23:33.158778Z",
      "transaction_number": "CR075-061-6739",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR63kmgBK8XAaujaippsY9BG",
      "available_at": "2012-10-26T22:23:33.089798Z"
    }




