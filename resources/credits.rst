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
        "holds_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:20:34.535750Z",
        "updated_at": "2012-10-26T15:20:34.535752Z",
        "uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG",
        "refunds_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC2OuQrYduuKuzELPJGS8HVG",
        "credits_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:20:34.594188Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:20:34.531749Z",
        "updated_at": "2012-10-26T15:20:34.531752Z",
        "uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/accounts/AC2OuQrYduuKuzELPJGS8HVG/bank_accounts/BA2OuyQbPPXmSPbSF13EkyXO",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA2OuyQbPPXmSPbSF13EkyXO"
      },
      "uri": "/v1/marketplaces/TEST-MP2OprmvTjN1kplDNP2IRRm4/credits/CR2Oyj3RjCNjy2bpmKpoxJIg",
      "updated_at": "2012-10-26T15:20:34.594190Z",
      "transaction_number": "CR674-780-7938",
      "state": "cleared",
      "meta": {},
      "id": "CR2Oyj3RjCNjy2bpmKpoxJIg",
      "available_at": "2012-10-26T22:20:34.578639Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:20:35.752230Z",
        "updated_at": "2012-10-26T15:20:35.752232Z",
        "uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500",
        "refunds_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC2PRG1yAyyooOCh7y7iy500",
        "credits_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:20:35.819060Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:20:35.748767Z",
        "updated_at": "2012-10-26T15:20:35.748770Z",
        "uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/accounts/AC2PRG1yAyyooOCh7y7iy500/bank_accounts/BA2PRqHQqSANWlzgkBjVw2Z6",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA2PRqHQqSANWlzgkBjVw2Z6"
      },
      "uri": "/v1/marketplaces/TEST-MP2PMm5T51VF5tyVGLAXaEBe/credits/CR2PVxE8iBQVelQ8BZyDb36I",
      "updated_at": "2012-10-26T15:20:35.819063Z",
      "transaction_number": "CR852-456-4799",
      "state": "cleared",
      "meta": {},
      "id": "CR2PVxE8iBQVelQ8BZyDb36I",
      "available_at": "2012-10-26T22:20:35.799412Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:20:37.009214Z",
            "updated_at": "2012-10-26T15:20:37.009217Z",
            "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4",
            "refunds_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC2Rhk8bd8CRTzf0XElglFe4",
            "credits_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:20:37.070591Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:20:37.004744Z",
            "updated_at": "2012-10-26T15:20:37.004747Z",
            "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/bank_accounts/BA2Rh0iCvQwxCLsaXNGEuQqo",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA2Rh0iCvQwxCLsaXNGEuQqo"
          },
          "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/credits/CR2RkJDShd07BsReLDoLF21m",
          "updated_at": "2012-10-26T15:20:37.070592Z",
          "transaction_number": "CR745-293-3969",
          "state": "cleared",
          "meta": {},
          "id": "CR2RkJDShd07BsReLDoLF21m",
          "available_at": "2012-10-26T22:20:37.051892Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:20:37.009214Z",
            "updated_at": "2012-10-26T15:20:37.009217Z",
            "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4",
            "refunds_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC2Rhk8bd8CRTzf0XElglFe4",
            "credits_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:20:37.071121Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:20:37.004744Z",
            "updated_at": "2012-10-26T15:20:37.004747Z",
            "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/accounts/AC2Rhk8bd8CRTzf0XElglFe4/bank_accounts/BA2Rh0iCvQwxCLsaXNGEuQqo",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA2Rh0iCvQwxCLsaXNGEuQqo"
          },
          "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/credits/CR2RkP4OJd8vpcuJBkMqucEQ",
          "updated_at": "2012-10-26T15:20:37.071123Z",
          "transaction_number": "CR259-382-8574",
          "state": "cleared",
          "meta": {},
          "id": "CR2RkP4OJd8vpcuJBkMqucEQ",
          "available_at": "2012-10-26T22:20:37.058548Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP2Ra0jZ5MeHZIkkeD2KiYao/credits?limit=10&offset=0"
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
        "holds_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:20:39.634714Z",
        "updated_at": "2012-10-26T15:20:39.634716Z",
        "uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8",
        "refunds_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC2Uephe8lUo2AJNilv7aVk8",
        "credits_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:20:39.718678Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:20:39.630346Z",
        "updated_at": "2012-10-26T15:20:39.630349Z",
        "uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/accounts/AC2Uephe8lUo2AJNilv7aVk8/bank_accounts/BA2Ue5WuECALM30OCRvAlbxy",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA2Ue5WuECALM30OCRvAlbxy"
      },
      "uri": "/v1/marketplaces/TEST-MP2U8ujWZUJ1M40i2QzIx9QM/credits/CR2UiRVWI6ToT5U3y5k3EUE4",
      "updated_at": "2012-10-26T15:20:39.773687Z",
      "transaction_number": "CR916-743-9636",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR2UiRVWI6ToT5U3y5k3EUE4",
      "available_at": "2012-10-26T22:20:39.690360Z"
    }




