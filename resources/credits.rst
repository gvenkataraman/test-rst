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

    USD cents. ``amount`` must be **>=** the minimum credit amount allowed for your
    marketplace. ``amount`` must be **<=** the maximum credit amount allowed for your
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
        "holds_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:59:31.844945Z",
        "updated_at": "2012-10-26T15:59:31.844947Z",
        "uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2",
        "refunds_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC6fZVPLqnY8N29teEqKCcf2",
        "credits_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:59:31.904075Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:59:31.841856Z",
        "updated_at": "2012-10-26T15:59:31.841858Z",
        "uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/accounts/AC6fZVPLqnY8N29teEqKCcf2/bank_accounts/BA6fZHZsrO6YdMLyxDFvs308",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA6fZHZsrO6YdMLyxDFvs308"
      },
      "uri": "/v1/marketplaces/TEST-MP6fUPUAquBQcJsCrUefDPJq/credits/CR6g3rizg057Xn7Ez9tofw2w",
      "updated_at": "2012-10-26T15:59:31.904077Z",
      "transaction_number": "CR637-493-2687",
      "state": "cleared",
      "meta": {},
      "id": "CR6g3rizg057Xn7Ez9tofw2w",
      "available_at": "2012-10-26T22:59:31.887576Z"
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
        "holds_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:59:33.068906Z",
        "updated_at": "2012-10-26T15:59:33.068909Z",
        "uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4",
        "refunds_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC6hngOulke82oT0B4p8Zws4",
        "credits_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/cards"
      },
      "fee": 25,
      "description": "hiya",
      "amount": 1254,
      "created_at": "2012-10-26T15:59:33.145630Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:59:33.064709Z",
        "updated_at": "2012-10-26T15:59:33.064712Z",
        "uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/accounts/AC6hngOulke82oT0B4p8Zws4/bank_accounts/BA6hmY6m2E289U1nXmJMKIHW",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA6hmY6m2E289U1nXmJMKIHW"
      },
      "uri": "/v1/marketplaces/TEST-MP6hfT72RoOQIg5QGVzyIYE4/credits/CR6hrPCnysiDdmiEDnGM6KUI",
      "updated_at": "2012-10-26T15:59:33.145633Z",
      "transaction_number": "CR397-307-5992",
      "state": "cleared",
      "meta": {},
      "id": "CR6hrPCnysiDdmiEDnGM6KUI",
      "available_at": "2012-10-26T22:59:33.125867Z"
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
      "first_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/credits?limit=10&offset=0",
      "items": [
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:59:34.339303Z",
            "updated_at": "2012-10-26T15:59:34.339305Z",
            "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32",
            "refunds_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC6iNRl2R8kxga8KGi1kdk32",
            "credits_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 1254,
          "created_at": "2012-10-26T15:59:34.421545Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:59:34.334942Z",
            "updated_at": "2012-10-26T15:59:34.334946Z",
            "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/bank_accounts/BA6iNxWPkfGR63IcS2baxamg",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA6iNxWPkfGR63IcS2baxamg"
          },
          "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/credits/CR6iSouO7jLvkkEtJ3JFD4WM",
          "updated_at": "2012-10-26T15:59:34.421548Z",
          "transaction_number": "CR375-432-5911",
          "state": "cleared",
          "meta": {},
          "id": "CR6iSouO7jLvkkEtJ3JFD4WM",
          "available_at": "2012-10-26T22:59:34.395939Z"
        },
        {
          "account": {
            "balance": 0,
            "holds_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/holds",
            "name": null,
            "roles": [
              "merchant",
              "buyer"
            ],
            "created_at": "2012-10-26T15:59:34.339303Z",
            "updated_at": "2012-10-26T15:59:34.339305Z",
            "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32",
            "refunds_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/refunds",
            "meta": {},
            "debits_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/debits",
            "transactions_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/transactions",
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/bank_accounts",
            "email_address": "email.7@y.com",
            "id": "AC6iNRl2R8kxga8KGi1kdk32",
            "credits_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/credits",
            "cards_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/cards"
          },
          "fee": 25,
          "description": "hiya",
          "amount": 431,
          "created_at": "2012-10-26T15:59:34.422268Z",
          "destination": {
            "bank_name": null,
            "name": "Fit Finlay",
            "bank_code": "325182797",
            "created_at": "2012-10-26T15:59:34.334942Z",
            "updated_at": "2012-10-26T15:59:34.334946Z",
            "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/accounts/AC6iNRl2R8kxga8KGi1kdk32/bank_accounts/BA6iNxWPkfGR63IcS2baxamg",
            "is_valid": true,
            "meta": {},
            "last_four": "x234",
            "id": "BA6iNxWPkfGR63IcS2baxamg"
          },
          "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/credits/CR6iSvXt1874V6Iv7PFabDhy",
          "updated_at": "2012-10-26T15:59:34.422270Z",
          "transaction_number": "CR931-249-2693",
          "state": "cleared",
          "meta": {},
          "id": "CR6iSvXt1874V6Iv7PFabDhy",
          "available_at": "2012-10-26T22:59:34.405156Z"
        }
      ],
      "previous_uri": null,
      "uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/credits?limit=10&offset=0",
      "limit": 10,
      "offset": 0,
      "total": 2,
      "next_uri": null,
      "last_uri": "/v1/marketplaces/TEST-MP6iGpGBl6195hDqYXOLAawc/credits?limit=10&offset=0"
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
        "holds_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/holds",
        "name": null,
        "roles": [
          "merchant",
          "buyer"
        ],
        "created_at": "2012-10-26T15:59:36.908822Z",
        "updated_at": "2012-10-26T15:59:36.908825Z",
        "uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji",
        "refunds_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/refunds",
        "meta": {},
        "debits_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/debits",
        "transactions_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/transactions",
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/bank_accounts",
        "email_address": "email.7@y.com",
        "id": "AC6lH2vqynhOsXGZddB0ncji",
        "credits_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/credits",
        "cards_uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/cards"
      },
      "fee": 25,
      "description": "my new description",
      "amount": 1254,
      "created_at": "2012-10-26T15:59:36.992618Z",
      "destination": {
        "bank_name": null,
        "name": "Fit Finlay",
        "bank_code": "325182797",
        "created_at": "2012-10-26T15:59:36.904506Z",
        "updated_at": "2012-10-26T15:59:36.904509Z",
        "uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/accounts/AC6lH2vqynhOsXGZddB0ncji/bank_accounts/BA6lGJeb7Nig5YFzGvs6nSqU",
        "is_valid": true,
        "meta": {},
        "last_four": "x234",
        "id": "BA6lGJeb7Nig5YFzGvs6nSqU"
      },
      "uri": "/v1/marketplaces/TEST-MP6lzGGR5bv6qw0nhzH34OTW/credits/CR6lLv0uPRZqds8UsvPUcX7C",
      "updated_at": "2012-10-26T15:59:37.036018Z",
      "transaction_number": "CR092-772-1145",
      "state": "cleared",
      "meta": {
        "my-id": "0987654321"
      },
      "id": "CR6lLv0uPRZqds8UsvPUcX7C",
      "available_at": "2012-10-26T22:59:36.964448Z"
    }




