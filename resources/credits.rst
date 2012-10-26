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

``description``: *optional* **string**. 

``meta``: *optional* **object**. Single level mapping from string keys to string values.

``appears_on_statement_as``: *optional* **string**. 

    Text that will appear on the buyer's statement. Characters that can be
    used are limited to:

    - ASCII letters (``a-z`` and ``A-Z``)
    - Digits (``0-9``)
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``)

    Any other characters will be rejected. Length must be **<=** ``22``.

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
        "holds_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:49:53.682717Z",
        "updated_at": "2012-10-26T15:49:53.682719Z",
        "uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G",
        "refunds_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC3yN3a39iXMEk4TypefT91G",
        "credits_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:49:53.760737Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:49:53.678127Z",
        "updated_at": "2012-10-26T15:49:53.678131Z",
        "uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/accounts/AC3yN3a39iXMEk4TypefT91G/bank_accounts/BA3yMILUyUbKWOovC84ESueo",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA3yMILUyUbKWOovC84ESueo"
      },
      "uri": "/v1/marketplaces/TEST-MP3yFuUhYiptrCzxt2MIz42g/credits/CR3yRGYlvdoO6Za6EH2VxUdS",
      "updated_at": "2012-10-26T15:49:53.760740Z",
      "transaction_number": "CR736-568-3818",
      "state": "cleared",
      "meta": {},
      "id": "CR3yRGYlvdoO6Za6EH2VxUdS",
      "available_at": "2012-10-26T22:49:53.740883Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:49:55.031794Z",
        "updated_at": "2012-10-26T15:49:55.031797Z",
        "uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du",
        "refunds_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC3Aj7YwZTucbWK3Gqhb44du",
        "credits_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:49:55.091019Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:49:55.027828Z",
        "updated_at": "2012-10-26T15:49:55.027830Z",
        "uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/accounts/AC3Aj7YwZTucbWK3Gqhb44du/bank_accounts/BA3AiQEaRZz83ZN0dyT5u0MA",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA3AiQEaRZz83ZN0dyT5u0MA"
      },
      "uri": "/v1/marketplaces/TEST-MP3AcWO3vLJaESQAQUXF9Vis/credits/CR3Amz2ZCZeqoQDN298oa7be",
      "updated_at": "2012-10-26T15:49:55.091021Z",
      "transaction_number": "CR788-561-9589",
      "state": "cleared",
      "meta": {},
      "id": "CR3Amz2ZCZeqoQDN298oa7be",
      "available_at": "2012-10-26T22:49:55.074901Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:49:56.258819Z",
            "updated_at": "2012-10-26T15:49:56.258821Z",
            "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI",
            "refunds_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC3BGGEbdxSSrt2DT6oTEiMI",
            "credits_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:49:56.339792Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:49:56.254380Z",
            "updated_at": "2012-10-26T15:49:56.254383Z",
            "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/bank_accounts/BA3BGn3TOPTrplIFON5bEQXq",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA3BGn3TOPTrplIFON5bEQXq"
          },
          "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/credits/CR3BLoGmCwItaT5BxQR7j564",
          "updated_at": "2012-10-26T15:49:56.339794Z",
          "transaction_number": "CR229-892-0773",
          "state": "cleared",
          "meta": {},
          "id": "CR3BLoGmCwItaT5BxQR7j564",
          "available_at": "2012-10-26T22:49:56.317918Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:49:56.258819Z",
            "updated_at": "2012-10-26T15:49:56.258821Z",
            "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI",
            "refunds_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC3BGGEbdxSSrt2DT6oTEiMI",
            "credits_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:49:56.340348Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:49:56.254380Z",
            "updated_at": "2012-10-26T15:49:56.254383Z",
            "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/accounts/AC3BGGEbdxSSrt2DT6oTEiMI/bank_accounts/BA3BGn3TOPTrplIFON5bEQXq",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA3BGn3TOPTrplIFON5bEQXq"
          },
          "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/credits/CR3BLw9i8JCYiyhKpULT9Yva",
          "updated_at": "2012-10-26T15:49:56.340349Z",
          "transaction_number": "CR252-890-0946",
          "state": "cleared",
          "meta": {},
          "id": "CR3BLw9i8JCYiyhKpULT9Yva",
          "available_at": "2012-10-26T22:49:56.327149Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP3BzHCMF2672VRqz3bDPwW0/credits?limit=10&offset=0"
    }



Update a Credit
---------------

.. code::

    PUT /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id
    PUT /v1/marketplaces/:marketplace_id/credits/:credit_id

Request
~~~~~~~

``description``: *optional* **string**. 

``meta``: *optional* **object**. Single level mapping from string keys to string values.

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
        "balance": 0,
        "holds_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:49:58.868156Z",
        "updated_at": "2012-10-26T15:49:58.868159Z",
        "uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o",
        "refunds_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC3ECE1VdWTCUdRQkp0Kmi6o",
        "credits_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/cards"
      },
      "fee": 25,
      "description": "my new description",
      "amount": 1254,
      "created_at": "2012-10-26T15:49:58.953031Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:49:58.863647Z",
        "updated_at": "2012-10-26T15:49:58.863650Z",
        "uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/accounts/AC3ECE1VdWTCUdRQkp0Kmi6o/bank_accounts/BA3ECjYXyQCU6XwYI2WbItOA",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA3ECjYXyQCU6XwYI2WbItOA"
      },
      "uri": "/v1/marketplaces/TEST-MP3Ev5X9rbrmrYJqBW5Ea8Yc/credits/CR3EHatIV9WpYyTNTADlgjze",
      "updated_at": "2012-10-26T15:49:59.012035Z",
      "transaction_number": "CR466-531-4204",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR3EHatIV9WpYyTNTADlgjze",
      "available_at": "2012-10-26T22:49:58.924684Z"
    }




