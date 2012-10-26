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
        "holds_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:32:47.818501Z",
        "updated_at": "2012-10-26T14:32:47.818504Z",
        "uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6",
        "refunds_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC5lGHdYhReLP6tf1ylF7KV6",
        "credits_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:32:47.879401Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:32:47.814093Z",
        "updated_at": "2012-10-26T14:32:47.814096Z",
        "uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/accounts/AC5lGHdYhReLP6tf1ylF7KV6/bank_accounts/BA5lGnKEZrTsA6ypeMJcP8Uc",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA5lGnKEZrTsA6ypeMJcP8Uc"
      },
      "uri": "/v1/marketplaces/TEST-MP5lzfdOBJidGcma3J5vx4K8/credits/CR5lKiW6ZXoAwlHA0iApc8sI",
      "updated_at": "2012-10-26T14:32:47.879403Z",
      "transaction_number": "CR812-029-5702",
      "state": "cleared",
      "meta": {},
      "id": "CR5lKiW6ZXoAwlHA0iApc8sI",
      "available_at": "2012-10-26T21:32:47.863500Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:32:49.066016Z",
        "updated_at": "2012-10-26T14:32:49.066019Z",
        "uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2",
        "refunds_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC5n5GGCVVdXmoT8NAiurqn2",
        "credits_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:32:49.125963Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:32:49.061665Z",
        "updated_at": "2012-10-26T14:32:49.061668Z",
        "uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/accounts/AC5n5GGCVVdXmoT8NAiurqn2/bank_accounts/BA5n5nBYBXI0Vd1otvBHm4LO",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA5n5nBYBXI0Vd1otvBHm4LO"
      },
      "uri": "/v1/marketplaces/TEST-MP5mYg9SqTnP6Ir9VH4sICY4/credits/CR5n9g2WKuUZtURUMuRtAVZa",
      "updated_at": "2012-10-26T14:32:49.125965Z",
      "transaction_number": "CR190-209-7011",
      "state": "cleared",
      "meta": {},
      "id": "CR5n9g2WKuUZtURUMuRtAVZa",
      "available_at": "2012-10-26T21:32:49.110223Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:32:50.403203Z",
            "updated_at": "2012-10-26T14:32:50.403205Z",
            "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE",
            "refunds_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC5oAW5q96lExtA3wYoOl3QE",
            "credits_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T14:32:50.491351Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:32:50.398666Z",
            "updated_at": "2012-10-26T14:32:50.398669Z",
            "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/bank_accounts/BA5oABYrc3D0MShnPgv4g9w0",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA5oABYrc3D0MShnPgv4g9w0"
          },
          "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/credits/CR5oFQCxVrPPRBhrXvewaiIA",
          "updated_at": "2012-10-26T14:32:50.491354Z",
          "transaction_number": "CR565-846-4417",
          "state": "cleared",
          "meta": {},
          "id": "CR5oFQCxVrPPRBhrXvewaiIA",
          "available_at": "2012-10-26T21:32:50.465100Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:32:50.403203Z",
            "updated_at": "2012-10-26T14:32:50.403205Z",
            "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE",
            "refunds_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC5oAW5q96lExtA3wYoOl3QE",
            "credits_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T14:32:50.492113Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:32:50.398666Z",
            "updated_at": "2012-10-26T14:32:50.398669Z",
            "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/accounts/AC5oAW5q96lExtA3wYoOl3QE/bank_accounts/BA5oABYrc3D0MShnPgv4g9w0",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA5oABYrc3D0MShnPgv4g9w0"
          },
          "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/credits/CR5oFY6xVf036P04IJ6pcyoY",
          "updated_at": "2012-10-26T14:32:50.492115Z",
          "transaction_number": "CR596-895-4950",
          "state": "cleared",
          "meta": {},
          "id": "CR5oFY6xVf036P04IJ6pcyoY",
          "available_at": "2012-10-26T21:32:50.474461Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP5otL4IhYnN9acDbnqZfVFq/credits?limit=10&offset=0"
    }



Update a Credit
---------------

.. code::

    PUT /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id
    PUT /v1/marketplaces/:marketplace_id/credits/:credit_id



 Request
~~~~~~~

``description``
: **required**
: Sequence of characters.

``meta``
: **required**
: Single level mapping from string keys to string values.

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




