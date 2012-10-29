Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_
- `Update a Credit`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``amount`` 
    **integer**. Amount of the credit. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit was created. 
 
``description`` 
    **string**. A description of the credit, used for display purposes. 
 
``account`` 
    **object**. The account to which the credit is associated. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``available_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit will be available to the merchant. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this credit. 
 
``destination`` 
    **object**. The funding destination for this credit (i.e., a bank account).  
 
``state`` 
    **string**. One of ``pending``, ``cleared``, ``rejected``.  
 

Credit an Account
-----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    POST /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``amount`` 
    *required* **integer** or **null**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``destination_uri`` 
    *optional* **string** or **null**.  
 
``bank_account_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 1234,  
        "account_uri": "/v1/marketplaces/TEST-MP1YDf60f4cGcnTjySC7Voeo/accounts/AC1YIqFg2niPzZDzkxCXdzNi" 
    } 
 

Response
~~~~~~~~

Headers 
^^^^^^^ 
 
.. code::  
 
    Status: 201 CREATED 
 
Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T18:23:34.352272Z",  
            "uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC207X0sppAMlI3L2a2fHwJ6",  
            "credits_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-28T18:23:34.441881Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T18:23:34.349324Z",  
            "uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/accounts/AC207X0sppAMlI3L2a2fHwJ6/bank_accounts/BA207KeD15rJkZ9Jv6obTEMc",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA207KeD15rJkZ9Jv6obTEMc" 
        },  
        "uri": "/v1/marketplaces/TEST-MP202ImSUOvOkLjVQvhmo3Fa/credits/CR20dHhUvFR7SMpGSjFT0f40",  
        "transaction_number": "CR208-151-4168",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR20dHhUvFR7SMpGSjFT0f40",  
        "available_at": "2012-10-29T01:23:34.434047Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    GET /v1/marketplaces/(marketplace:marketplace)/credits/(credit:credit) 
 

Request 
~~~~~~~ 
 
Body 
^^^^ 
 
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
            "holds_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T18:23:35.624713Z",  
            "uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC21yFQKrtAuceqxsUp1O53m",  
            "credits_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-28T18:23:35.689001Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T18:23:35.620482Z",  
            "uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/accounts/AC21yFQKrtAuceqxsUp1O53m/bank_accounts/BA21ymT4dOIFy9XVqnpupzgw",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA21ymT4dOIFy9XVqnpupzgw" 
        },  
        "uri": "/v1/marketplaces/TEST-MP21rbL7DZxKPQ3fjWL8lgcA/credits/CR21CzRPf0Z4UodaG5oUjjMM",  
        "transaction_number": "CR705-352-5389",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR21CzRPf0Z4UodaG5oUjjMM",  
        "available_at": "2012-10-29T01:23:35.674499Z" 
    } 
 

List All Credits
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T18:23:36.849915Z",  
                    "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC22W6stGfkC7upRvwCwxPUM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T18:23:36.912451Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T18:23:36.843483Z",  
                    "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/bank_accounts/BA22VEGeILMMQjTvcplb0oYc",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA22VEGeILMMQjTvcplb0oYc" 
                },  
                "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/credits/CR22ZACkudjn5hPEapaUQwEQ",  
                "transaction_number": "CR413-922-1074",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR22ZACkudjn5hPEapaUQwEQ",  
                "available_at": "2012-10-29T01:23:36.893550Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T18:23:36.849915Z",  
                    "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC22W6stGfkC7upRvwCwxPUM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T18:23:36.913054Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T18:23:36.843483Z",  
                    "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/accounts/AC22W6stGfkC7upRvwCwxPUM/bank_accounts/BA22VEGeILMMQjTvcplb0oYc",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA22VEGeILMMQjTvcplb0oYc" 
                },  
                "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/credits/CR22ZFPRYphmmyV7nB8CSHOc",  
                "transaction_number": "CR750-376-4844",  
                "amount": 431,  
                "meta": {},  
                "id": "CR22ZFPRYphmmyV7nB8CSHOc",  
                "available_at": "2012-10-29T01:23:36.900182Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP22PSOpl6LTCUtkYLYa8Y2U/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T18:23:39.423763Z",  
            "uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC25PANWyXk6uNwHE2aUG8fi",  
            "credits_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-28T18:23:39.514111Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T18:23:39.419536Z",  
            "uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/accounts/AC25PANWyXk6uNwHE2aUG8fi/bank_accounts/BA25Pi384juPjplShqCLtVNW",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA25Pi384juPjplShqCLtVNW" 
        },  
        "uri": "/v1/marketplaces/TEST-MP25IaJ4t84tpAHfUjJTIG5S/credits/CR25UFfb8Xs886idogmJbVQg",  
        "transaction_number": "CR930-594-9911",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR25UFfb8Xs886idogmJbVQg",  
        "available_at": "2012-10-29T01:23:39.480485Z" 
    } 
 

