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
        "holds_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:43:48.702360Z",
        "updated_at": "2012-10-26T14:43:48.702363Z",
        "uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly",
        "refunds_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC1KRWLfTi1dqxOdEgjkJBly",
        "credits_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:43:48.778518Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:43:48.697965Z",
        "updated_at": "2012-10-26T14:43:48.697968Z",
        "uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/accounts/AC1KRWLfTi1dqxOdEgjkJBly/bank_accounts/BA1KRDn2mpnxgrnFQ0tb3rEM",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA1KRDn2mpnxgrnFQ0tb3rEM"
      },
      "uri": "/v1/marketplaces/TEST-MP1KKCKZU6hiEG06FbxgnC9m/credits/CR1KWte845jICrmF6BT2OZ5G",
      "updated_at": "2012-10-26T14:43:48.778521Z",
      "transaction_number": "CR156-795-4527",
      "state": "cleared",
      "meta": {},
      "id": "CR1KWte845jICrmF6BT2OZ5G",
      "available_at": "2012-10-26T21:43:48.758822Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:43:49.973037Z",
        "updated_at": "2012-10-26T14:43:49.973040Z",
        "uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0",
        "refunds_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC1Miypvq6ASzuvQMUIANlA0",
        "credits_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:43:50.049481Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:43:49.968661Z",
        "updated_at": "2012-10-26T14:43:49.968664Z",
        "uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/accounts/AC1Miypvq6ASzuvQMUIANlA0/bank_accounts/BA1MifaoWH6KrCxp2wtVaKgc",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA1MifaoWH6KrCxp2wtVaKgc"
      },
      "uri": "/v1/marketplaces/TEST-MP1Mbc4v0YDTlrYEHadSHQJC/credits/CR1Mn6osXXD4Xv2B46ddI0Nm",
      "updated_at": "2012-10-26T14:43:50.049484Z",
      "transaction_number": "CR490-355-9860",
      "state": "cleared",
      "meta": {},
      "id": "CR1Mn6osXXD4Xv2B46ddI0Nm",
      "available_at": "2012-10-26T21:43:50.029819Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:43:51.224078Z",
            "updated_at": "2012-10-26T14:43:51.224080Z",
            "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII",
            "refunds_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC1NHO0gEks6iom4ebZE4YII",
            "credits_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T14:43:51.282507Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:43:51.221083Z",
            "updated_at": "2012-10-26T14:43:51.221086Z",
            "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/bank_accounts/BA1NHADbaW04y4fi1NXO9S4Y",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA1NHADbaW04y4fi1NXO9S4Y"
          },
          "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/credits/CR1NKUyhuJXxmdvFZE3BZPJa",
          "updated_at": "2012-10-26T14:43:51.282509Z",
          "transaction_number": "CR150-994-3893",
          "state": "cleared",
          "meta": {},
          "id": "CR1NKUyhuJXxmdvFZE3BZPJa",
          "available_at": "2012-10-26T21:43:51.262456Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:43:51.224078Z",
            "updated_at": "2012-10-26T14:43:51.224080Z",
            "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII",
            "refunds_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC1NHO0gEks6iom4ebZE4YII",
            "credits_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T14:43:51.283146Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:43:51.221083Z",
            "updated_at": "2012-10-26T14:43:51.221086Z",
            "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/accounts/AC1NHO0gEks6iom4ebZE4YII/bank_accounts/BA1NHADbaW04y4fi1NXO9S4Y",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA1NHADbaW04y4fi1NXO9S4Y"
          },
          "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/credits/CR1NL0puDziR95YZ7MiBOjcg",
          "updated_at": "2012-10-26T14:43:51.283148Z",
          "transaction_number": "CR939-575-5989",
          "state": "cleared",
          "meta": {},
          "id": "CR1NL0puDziR95YZ7MiBOjcg",
          "available_at": "2012-10-26T21:43:51.269276Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP1NAy4fpWPlHgNmN8h54M84/credits?limit=10&offset=0"
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
        "holds_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:43:53.796100Z",
        "updated_at": "2012-10-26T14:43:53.796102Z",
        "uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o",
        "refunds_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC1QB9iqJqMxRJtNELsZRk6o",
        "credits_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:43:53.859457Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:43:53.791670Z",
        "updated_at": "2012-10-26T14:43:53.791673Z",
        "uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/accounts/AC1QB9iqJqMxRJtNELsZRk6o/bank_accounts/BA1QAPGOeJYtbavee0cToaVu",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA1QAPGOeJYtbavee0cToaVu"
      },
      "uri": "/v1/marketplaces/TEST-MP1Qu2EbK3eWIDfYYULEf5gE/credits/CR1QEwQHg1XsgOLqsjN8aKjy",
      "updated_at": "2012-10-26T14:43:53.902965Z",
      "transaction_number": "CR296-933-5442",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR1QEwQHg1XsgOLqsjN8aKjy",
      "available_at": "2012-10-26T21:43:53.838325Z"
    }




