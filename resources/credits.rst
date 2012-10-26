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
        "holds_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:39:04.974033Z",
        "updated_at": "2012-10-26T14:39:04.974036Z",
        "uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW",
        "refunds_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC4oONnJLhu0bpKY7wEY93tW",
        "credits_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:39:05.050410Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:39:04.969927Z",
        "updated_at": "2012-10-26T14:39:04.969930Z",
        "uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/accounts/AC4oONnJLhu0bpKY7wEY93tW/bank_accounts/BA4oOvbv9KkqqJtGHlBO6H2c",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA4oOvbv9KkqqJtGHlBO6H2c"
      },
      "uri": "/v1/marketplaces/TEST-MP4oHss7fjbvTfV42mnculmI/credits/CR4oTlbaG6iiLbEx5eEBl6Hq",
      "updated_at": "2012-10-26T14:39:05.050412Z",
      "transaction_number": "CR878-680-1944",
      "state": "cleared",
      "meta": {},
      "id": "CR4oTlbaG6iiLbEx5eEBl6Hq",
      "available_at": "2012-10-26T21:39:05.030734Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T14:39:06.235981Z",
        "updated_at": "2012-10-26T14:39:06.235984Z",
        "uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK",
        "refunds_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC4qeNfcFslJ0CXz0jRZrrnK",
        "credits_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T14:39:06.312358Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T14:39:06.231837Z",
        "updated_at": "2012-10-26T14:39:06.231840Z",
        "uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/accounts/AC4qeNfcFslJ0CXz0jRZrrnK/bank_accounts/BA4qeuXl3BmF7gVKF33YbWte",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA4qeuXl3BmF7gVKF33YbWte"
      },
      "uri": "/v1/marketplaces/TEST-MP4q7nXEwwKPx2eibZiiUw3G/credits/CR4qjky4Z6Wf71Vo6XbOUKEs",
      "updated_at": "2012-10-26T14:39:06.312360Z",
      "transaction_number": "CR352-861-7316",
      "state": "cleared",
      "meta": {},
      "id": "CR4qjky4Z6Wf71Vo6XbOUKEs",
      "available_at": "2012-10-26T21:39:06.292659Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:39:07.503208Z",
            "updated_at": "2012-10-26T14:39:07.503210Z",
            "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg",
            "refunds_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC4rFa8jVHDv7KuOMwt2OFMg",
            "credits_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T14:39:07.585211Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:39:07.498848Z",
            "updated_at": "2012-10-26T14:39:07.498852Z",
            "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/bank_accounts/BA4rEQJPMqqTqKW9uYDBQb1a",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA4rEQJPMqqTqKW9uYDBQb1a"
          },
          "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/credits/CR4rJG24YB8rP9TtlRzd9xo8",
          "updated_at": "2012-10-26T14:39:07.585214Z",
          "transaction_number": "CR470-362-8874",
          "state": "cleared",
          "meta": {},
          "id": "CR4rJG24YB8rP9TtlRzd9xo8",
          "available_at": "2012-10-26T21:39:07.559529Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T14:39:07.503208Z",
            "updated_at": "2012-10-26T14:39:07.503210Z",
            "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg",
            "refunds_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC4rFa8jVHDv7KuOMwt2OFMg",
            "credits_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T14:39:07.585956Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T14:39:07.498848Z",
            "updated_at": "2012-10-26T14:39:07.498852Z",
            "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/accounts/AC4rFa8jVHDv7KuOMwt2OFMg/bank_accounts/BA4rEQJPMqqTqKW9uYDBQb1a",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA4rEQJPMqqTqKW9uYDBQb1a"
          },
          "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/credits/CR4rJNDQVSDzsapAOv6bLE5S",
          "updated_at": "2012-10-26T14:39:07.585958Z",
          "transaction_number": "CR740-886-0990",
          "state": "cleared",
          "meta": {},
          "id": "CR4rJNDQVSDzsapAOv6bLE5S",
          "available_at": "2012-10-26T21:39:07.568808Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP4rxPN9DBXcYwtiWOBdob8U/credits?limit=10&offset=0"
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




