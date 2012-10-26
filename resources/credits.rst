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
        "holds_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:07:53.277388Z",
        "updated_at": "2012-10-26T15:07:53.277391Z",
        "uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU",
        "refunds_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC4Aqci4lJndoKaNReN2JHsU",
        "credits_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:07:53.348230Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:07:53.273946Z",
        "updated_at": "2012-10-26T15:07:53.273948Z",
        "uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/accounts/AC4Aqci4lJndoKaNReN2JHsU/bank_accounts/BA4ApWV8LiEuzByloO8k9AC8",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA4ApWV8LiEuzByloO8k9AC8"
      },
      "uri": "/v1/marketplaces/TEST-MP4AkmFzqbmTJv41zLvT7i1C/credits/CR4AujJIFOxTKMLMpzFo0sKg",
      "updated_at": "2012-10-26T15:07:53.348232Z",
      "transaction_number": "CR849-856-8157",
      "state": "cleared",
      "meta": {},
      "id": "CR4AujJIFOxTKMLMpzFo0sKg",
      "available_at": "2012-10-26T22:07:53.327900Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:07:54.545192Z",
        "updated_at": "2012-10-26T15:07:54.545195Z",
        "uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6",
        "refunds_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC4BQB6tchlUzDWwYnQIK1b6",
        "credits_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:07:54.623453Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:07:54.540956Z",
        "updated_at": "2012-10-26T15:07:54.540959Z",
        "uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/accounts/AC4BQB6tchlUzDWwYnQIK1b6/bank_accounts/BA4BQihmNivMU1FM38u6OnCA",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA4BQihmNivMU1FM38u6OnCA"
      },
      "uri": "/v1/marketplaces/TEST-MP4BJCebHeIHdldpIceWYNHm/credits/CR4BVe3Xy8O8x8e00vXr7PDK",
      "updated_at": "2012-10-26T15:07:54.623456Z",
      "transaction_number": "CR063-305-6949",
      "state": "cleared",
      "meta": {},
      "id": "CR4BVe3Xy8O8x8e00vXr7PDK",
      "available_at": "2012-10-26T22:07:54.603006Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:07:55.800254Z",
            "updated_at": "2012-10-26T15:07:55.800257Z",
            "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q",
            "refunds_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC4Dg75qaqSQjxM242p5xX2Q",
            "credits_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:07:55.867176Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:07:55.795864Z",
            "updated_at": "2012-10-26T15:07:55.795867Z",
            "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/bank_accounts/BA4DfNNU7skmpFCv42gUgi68",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA4DfNNU7skmpFCv42gUgi68"
          },
          "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/credits/CR4DjGWzczmArjOFnjD9IxG4",
          "updated_at": "2012-10-26T15:07:55.867178Z",
          "transaction_number": "CR176-525-3815",
          "state": "cleared",
          "meta": {},
          "id": "CR4DjGWzczmArjOFnjD9IxG4",
          "available_at": "2012-10-26T22:07:55.844768Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:07:55.800254Z",
            "updated_at": "2012-10-26T15:07:55.800257Z",
            "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q",
            "refunds_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC4Dg75qaqSQjxM242p5xX2Q",
            "credits_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:07:55.867840Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:07:55.795864Z",
            "updated_at": "2012-10-26T15:07:55.795867Z",
            "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/accounts/AC4Dg75qaqSQjxM242p5xX2Q/bank_accounts/BA4DfNNU7skmpFCv42gUgi68",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA4DfNNU7skmpFCv42gUgi68"
          },
          "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/credits/CR4DjN5JPWs4LM439T5QlMOM",
          "updated_at": "2012-10-26T15:07:55.867842Z",
          "transaction_number": "CR935-635-0802",
          "state": "cleared",
          "meta": {},
          "id": "CR4DjN5JPWs4LM439T5QlMOM",
          "available_at": "2012-10-26T22:07:55.852014Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP4D8EhpiC9Hvfixefj2W3TS/credits?limit=10&offset=0"
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
        "holds_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:07:58.440425Z",
        "updated_at": "2012-10-26T15:07:58.440428Z",
        "uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic",
        "refunds_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC4Geeesulue1ropNcUdAHic",
        "credits_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:07:58.518012Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:07:58.436989Z",
        "updated_at": "2012-10-26T15:07:58.436992Z",
        "uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/accounts/AC4Geeesulue1ropNcUdAHic/bank_accounts/BA4GdZ2MUyqttEh1aXLdqRmY",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA4GdZ2MUyqttEh1aXLdqRmY"
      },
      "uri": "/v1/marketplaces/TEST-MP4G8Nsc1gvGrASa2QNZEYss/credits/CR4GiejlxkHKsgO1l9BcOnLS",
      "updated_at": "2012-10-26T15:07:58.574298Z",
      "transaction_number": "CR998-026-8880",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR4GiejlxkHKsgO1l9BcOnLS",
      "available_at": "2012-10-26T22:07:58.489563Z"
    }




