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

    USD cents. Must be **>=** the minimum credit amount allowed for your
    marketplace and **<=** the maximum credit amount allowed for your
    marketplace.

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
        "holds_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T16:07:21.862631Z",
        "updated_at": "2012-10-26T16:07:21.862633Z",
        "uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY",
        "refunds_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC6ZzzN1tYgJUjWdU74QWyoY",
        "credits_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T16:07:21.917790Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T16:07:21.859897Z",
        "updated_at": "2012-10-26T16:07:21.859900Z",
        "uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/accounts/AC6ZzzN1tYgJUjWdU74QWyoY/bank_accounts/BA6ZznuGde5LfprskY9tG47y",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA6ZznuGde5LfprskY9tG47y"
      },
      "uri": "/v1/marketplaces/TEST-MP6ZtYmxH5KKMlP7A9CxrOQI/credits/CR6ZCM7XyS6EgNtdf3zlWrLm",
      "updated_at": "2012-10-26T16:07:21.917792Z",
      "transaction_number": "CR469-870-8512",
      "state": "cleared",
      "meta": {},
      "id": "CR6ZCM7XyS6EgNtdf3zlWrLm",
      "available_at": "2012-10-26T23:07:21.902069Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T16:07:23.086446Z",
        "updated_at": "2012-10-26T16:07:23.086448Z",
        "uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM",
        "refunds_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC70WU6t1TLPsOtPdICTt5AM",
        "credits_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T16:07:23.145439Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T16:07:23.082292Z",
        "updated_at": "2012-10-26T16:07:23.082295Z",
        "uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/accounts/AC70WU6t1TLPsOtPdICTt5AM/bank_accounts/BA70WBFdKb4i0kRNlie6RHeY",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA70WBFdKb4i0kRNlie6RHeY"
      },
      "uri": "/v1/marketplaces/TEST-MP70PXLgr1gmXAvkNycB30Y4/credits/CR710oFfqI8SLj4OOA6ehnOQ",
      "updated_at": "2012-10-26T16:07:23.145441Z",
      "transaction_number": "CR992-871-2506",
      "state": "cleared",
      "meta": {},
      "id": "CR710oFfqI8SLj4OOA6ehnOQ",
      "available_at": "2012-10-26T23:07:23.129820Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T16:07:24.304473Z",
            "updated_at": "2012-10-26T16:07:24.304475Z",
            "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs",
            "refunds_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC72jQpWSC65ngDsoXh0MkAs",
            "credits_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T16:07:24.377585Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T16:07:24.300989Z",
            "updated_at": "2012-10-26T16:07:24.300991Z",
            "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/bank_accounts/BA72jAZNRqCebsryh2KWE8TO",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA72jAZNRqCebsryh2KWE8TO"
          },
          "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/credits/CR72nJ5osxJazZyudBTQZxze",
          "updated_at": "2012-10-26T16:07:24.377588Z",
          "transaction_number": "CR598-662-9825",
          "state": "cleared",
          "meta": {},
          "id": "CR72nJ5osxJazZyudBTQZxze",
          "available_at": "2012-10-26T23:07:24.351798Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T16:07:24.304473Z",
            "updated_at": "2012-10-26T16:07:24.304475Z",
            "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs",
            "refunds_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC72jQpWSC65ngDsoXh0MkAs",
            "credits_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T16:07:24.378319Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T16:07:24.300989Z",
            "updated_at": "2012-10-26T16:07:24.300991Z",
            "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/accounts/AC72jQpWSC65ngDsoXh0MkAs/bank_accounts/BA72jAZNRqCebsryh2KWE8TO",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA72jAZNRqCebsryh2KWE8TO"
          },
          "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/credits/CR72nQIM8cBRokRkvZmvnGGU",
          "updated_at": "2012-10-26T16:07:24.378321Z",
          "transaction_number": "CR288-206-5036",
          "state": "cleared",
          "meta": {},
          "id": "CR72nQIM8cBRokRkvZmvnGGU",
          "available_at": "2012-10-26T23:07:24.361057Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP72eNzmcphwXc4ivuNR7AEc/credits?limit=10&offset=0"
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
        "holds_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T16:07:26.935339Z",
        "updated_at": "2012-10-26T16:07:26.935342Z",
        "uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA",
        "refunds_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC75hitprcABue9gOsRhm3mA",
        "credits_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/cards"
      },
      "fee": 25,
      "description": "my new description",
      "amount": 1254,
      "created_at": "2012-10-26T16:07:27.019340Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T16:07:26.930920Z",
        "updated_at": "2012-10-26T16:07:26.930923Z",
        "uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/accounts/AC75hitprcABue9gOsRhm3mA/bank_accounts/BA75gYUt8tpO6ytU6BtXQiSU",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA75gYUt8tpO6ytU6BtXQiSU"
      },
      "uri": "/v1/marketplaces/TEST-MP759Za2xoZ9ADirpOdQkrk0/credits/CR75lMy38UlYkoh41mRIRvyk",
      "updated_at": "2012-10-26T16:07:27.074387Z",
      "transaction_number": "CR235-056-4076",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR75lMy38UlYkoh41mRIRvyk",
      "available_at": "2012-10-26T23:07:26.991355Z"
    }




