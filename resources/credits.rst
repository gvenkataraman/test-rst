Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_

Credit an Account
-----------------

.. code::

    POST /v1/marketplaces/:marketplace_id/accounts/:account_id/credits    POST /v1/marketplaces/:marketplace_id/credits


Request
~~~~~~~

``amount``
: **required**
: If the resolving URI references a hold then this is hold amount. You can
: always capture less than the hold amount (e.g. a partial capture).
: Otherwise its the maximum per debit amount for your marketplace.

``appears_on_statement_as``
: **required**
: Text that will appear on the buyer's statement. Characters that can be
: used are limited to:
: 
: - ASCII letters (``a-z`` and ``A-Z``)
: - Digits (``0-9``)
: - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``)
: 
: Any other characters will be rejected.

``meta``
: **required**
: Single level mapping from string keys to string values.

``description``
: **required**
: Sequence of characters.

``account_uri``
: **required**
: URI.

``merchant_uri``
: **required**
: URI.

``hold_uri``
: **required**
: URI.
: 
: If no ``hold`` is provided one my be generated and captured if the
: source is a card.

Exactly one of

    ``source_uri``
    : *required* **string**
    : URI.

    ``bank_account_uri``
    : *required* **string**
    : URI.

    ``card_uri``
    : *required* **string**
    : URI.

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
        "holds_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:27:12.376200Z",
        "updated_at": "2012-10-26T14:27:12.376202Z",
        "uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc",
        "refunds_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC73tnC4UO52gnMb4l0Vnggc",
        "credits_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:27:12.453382Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:27:12.371919Z",
        "updated_at": "2012-10-26T14:27:12.371922Z",
        "uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/accounts/AC73tnC4UO52gnMb4l0Vnggc/bank_accounts/BA73t4IpZ5F8zEhn79QzpQwc",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA73t4IpZ5F8zEhn79QzpQwc"
      },
      "uri": "/v1/marketplaces/TEST-MP73nmBNo6LwRQO3TWmfU4fy/credits/CR73xWEaWW0Iyt8d91GlavpW",
      "updated_at": "2012-10-26T14:27:12.453385Z",
      "transaction_number": "CR275-143-9767",
      "state": "cleared",
      "meta": {},
      "id": "CR73xWEaWW0Iyt8d91GlavpW",
      "available_at": "2012-10-26T21:27:12.433257Z"
    }



Retrieve a Credit
-----------------

.. code::

    GET /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id    GET /v1/marketplaces/:marketplace_id/credits/:credit_id


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
        "holds_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:27:13.625494Z",
        "updated_at": "2012-10-26T14:27:13.625497Z",
        "uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU",
        "refunds_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC74SuZxuhze5KMqPeEwrKGU",
        "credits_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:27:13.693867Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:27:13.621026Z",
        "updated_at": "2012-10-26T14:27:13.621029Z",
        "uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/accounts/AC74SuZxuhze5KMqPeEwrKGU/bank_accounts/BA74SbdsQ8MXIvH9Y9QxrlNq",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA74SbdsQ8MXIvH9Y9QxrlNq"
      },
      "uri": "/v1/marketplaces/TEST-MP74MxjVr2B8GNNeTx1W2zqY/credits/CR74WzWwtLGvmINRNaeU2qK8",
      "updated_at": "2012-10-26T14:27:13.693869Z",
      "transaction_number": "CR705-171-4637",
      "state": "cleared",
      "meta": {},
      "id": "CR74WzWwtLGvmINRNaeU2qK8",
      "available_at": "2012-10-26T21:27:13.677318Z"
    }



List All Credits
----------------

.. code::

    GET /v1/marketplaces/:marketplace_id/accounts/:account_id/credits    GET /v1/marketplaces/:marketplace_id/credits


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
      "first_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:27:14.899379Z",
            "updated_at": "2012-10-26T14:27:14.899381Z",
            "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU",
            "refunds_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC76jkpgQxRmfWbzNUofIrUU",
            "credits_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T14:27:14.982748Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:27:14.895064Z",
            "updated_at": "2012-10-26T14:27:14.895067Z",
            "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/bank_accounts/BA76j1pYUvBYqwWeVDt2xTI8",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA76j1pYUvBYqwWeVDt2xTI8"
          },
          "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/credits/CR76nVWiPFpn9ZfgWikUu7n6",
          "updated_at": "2012-10-26T14:27:14.982751Z",
          "transaction_number": "CR862-828-9817",
          "state": "cleared",
          "meta": {},
          "id": "CR76nVWiPFpn9ZfgWikUu7n6",
          "available_at": "2012-10-26T21:27:14.956809Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:27:14.899379Z",
            "updated_at": "2012-10-26T14:27:14.899381Z",
            "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU",
            "refunds_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC76jkpgQxRmfWbzNUofIrUU",
            "credits_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T14:27:14.983497Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:27:14.895064Z",
            "updated_at": "2012-10-26T14:27:14.895067Z",
            "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/accounts/AC76jkpgQxRmfWbzNUofIrUU/bank_accounts/BA76j1pYUvBYqwWeVDt2xTI8",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA76j1pYUvBYqwWeVDt2xTI8"
          },
          "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/credits/CR76o3qQ4fHrsZe8E6bm73c8",
          "updated_at": "2012-10-26T14:27:14.983499Z",
          "transaction_number": "CR689-961-3398",
          "state": "cleared",
          "meta": {},
          "id": "CR76o3qQ4fHrsZe8E6bm73c8",
          "available_at": "2012-10-26T21:27:14.966232Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP76bPyt3kFjx2L4vSNgbONm/credits?limit=10&offset=0"
    }




