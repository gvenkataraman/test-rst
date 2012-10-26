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

``amount``: **optional** *integer*. 

If the resolving URI references a hold then this is hold amount. You can
always capture less than the hold amount (e.g. a partial capture).
Otherwise its the maximum per debit amount for your marketplace.


``appears_on_statement_as``: **optional** *string*. 

Text that will appear on the buyer's statement. Characters that can be
used are limited to:

- ASCII letters (``a-z`` and ``A-Z``)
- Digits (``0-9``)
- Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``)

Any other characters will be rejected.


``meta``: **optional** *object*. Single level mapping from string keys to string values.


``description``: **optional** *string*. Sequence of characters.


``account_uri``: **optional** *string*. 
``merchant_uri``: **optional** *string*. 
``hold_uri``: **optional** *string*. 

URI.

If no ``hold`` is provided one my be generated and captured if the
source is a card.


Exactly one of

    ``source_uri``: **required** *string*. 
    ``bank_account_uri``: **required** *string*. 
    ``card_uri``: **required** *string*. 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:10:21.796709Z",
        "updated_at": "2012-10-26T15:10:21.796712Z",
        "uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS",
        "refunds_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC7hsRyhNrNR0K6I8bsOtEBS",
        "credits_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:10:21.872874Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:10:21.792526Z",
        "updated_at": "2012-10-26T15:10:21.792529Z",
        "uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/accounts/AC7hsRyhNrNR0K6I8bsOtEBS/bank_accounts/BA7hszexQOSipaa3tSJQ9Md6",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA7hszexQOSipaa3tSJQ9Md6"
      },
      "uri": "/v1/marketplaces/TEST-MP7hlwSdcsbbu9RNrQvdYExm/credits/CR7hxox3Fo8MksfuO3EILtEo",
      "updated_at": "2012-10-26T15:10:21.872876Z",
      "transaction_number": "CR809-821-5733",
      "state": "cleared",
      "meta": {},
      "id": "CR7hxox3Fo8MksfuO3EILtEo",
      "available_at": "2012-10-26T22:10:21.853305Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:10:23.068929Z",
        "updated_at": "2012-10-26T15:10:23.068931Z",
        "uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq",
        "refunds_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC7iTA7GOyj6rdH5eNqqMsjq",
        "credits_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:10:23.145264Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:10:23.064490Z",
        "updated_at": "2012-10-26T15:10:23.064493Z",
        "uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/accounts/AC7iTA7GOyj6rdH5eNqqMsjq/bank_accounts/BA7iTgvx54naGSsgRsbLICZS",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA7iTgvx54naGSsgRsbLICZS"
      },
      "uri": "/v1/marketplaces/TEST-MP7iMdx8urGirByTKdBxxfqk/credits/CR7iYa2JNTJ0tATP9XI2dmLi",
      "updated_at": "2012-10-26T15:10:23.145266Z",
      "transaction_number": "CR736-397-7818",
      "state": "cleared",
      "meta": {},
      "id": "CR7iYa2JNTJ0tATP9XI2dmLi",
      "available_at": "2012-10-26T22:10:23.126222Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:10:24.346540Z",
            "updated_at": "2012-10-26T15:10:24.346543Z",
            "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA",
            "refunds_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC7kkFTJzYkrUcGQ9Uoq57WA",
            "credits_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:10:24.416465Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:10:24.342254Z",
            "updated_at": "2012-10-26T15:10:24.342257Z",
            "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/bank_accounts/BA7kkmSPVyHuTsEMrTxx8xjS",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA7kkmSPVyHuTsEMrTxx8xjS"
          },
          "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/credits/CR7koGlpgDqQqCeGRw67rHlG",
          "updated_at": "2012-10-26T15:10:24.416467Z",
          "transaction_number": "CR648-821-7449",
          "state": "cleared",
          "meta": {},
          "id": "CR7koGlpgDqQqCeGRw67rHlG",
          "available_at": "2012-10-26T22:10:24.398171Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:10:24.346540Z",
            "updated_at": "2012-10-26T15:10:24.346543Z",
            "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA",
            "refunds_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC7kkFTJzYkrUcGQ9Uoq57WA",
            "credits_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:10:24.417084Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:10:24.342254Z",
            "updated_at": "2012-10-26T15:10:24.342257Z",
            "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/accounts/AC7kkFTJzYkrUcGQ9Uoq57WA/bank_accounts/BA7kkmSPVyHuTsEMrTxx8xjS",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA7kkmSPVyHuTsEMrTxx8xjS"
          },
          "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/credits/CR7koLGZkIiFCzfMfpIcm4AI",
          "updated_at": "2012-10-26T15:10:24.417085Z",
          "transaction_number": "CR722-125-5793",
          "state": "cleared",
          "meta": {},
          "id": "CR7koLGZkIiFCzfMfpIcm4AI",
          "available_at": "2012-10-26T22:10:24.404417Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP7kdatOERkQGP6xYSjSNYGM/credits?limit=10&offset=0"
    }



Update a Credit
---------------

.. code::

    PUT /v1/marketplaces/:marketplace_id/accounts/:account_id/credits/:credit_id
    PUT /v1/marketplaces/:marketplace_id/credits/:credit_id

Request
~~~~~~~

``description``: **optional** *string*. Sequence of characters.


``meta``: **optional** *object*. Single level mapping from string keys to string values.


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
        "holds_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:10:27.070462Z",
        "updated_at": "2012-10-26T15:10:27.070465Z",
        "uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI",
        "refunds_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC7noCEsYffmGIKgPiqmJykI",
        "credits_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:10:27.135606Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:10:27.066116Z",
        "updated_at": "2012-10-26T15:10:27.066119Z",
        "uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/accounts/AC7noCEsYffmGIKgPiqmJykI/bank_accounts/BA7nojkxlHCx0QpEzGoFMPL6",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA7nojkxlHCx0QpEzGoFMPL6"
      },
      "uri": "/v1/marketplaces/TEST-MP7nhgsj0bSZY1x3k7xRpgMY/credits/CR7ns4TzqHF3EB8FcE8aZHbS",
      "updated_at": "2012-10-26T15:10:27.182262Z",
      "transaction_number": "CR296-611-3323",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR7ns4TzqHF3EB8FcE8aZHbS",
      "available_at": "2012-10-26T22:10:27.113319Z"
    }




