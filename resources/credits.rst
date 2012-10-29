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
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 1234,  
        "account_uri": "/v1/marketplaces/TEST-MP5EyUkvDpjoMbFAlPb9hHb6/accounts/AC5EFfw41umopy2iMzy1zeDy" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:37:44.901539Z",  
            "uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5Gt7aSirSWb80H0oIpT7jS",  
            "credits_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T11:37:45.008730Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:37:44.896786Z",  
            "uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/accounts/AC5Gt7aSirSWb80H0oIpT7jS/bank_accounts/BA5GsMApdPce4IiLkM5ZgPjK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5GsMApdPce4IiLkM5ZgPjK" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5Glrc6rsCs1prXHz3mXKK0/credits/CR5GA17zNQikNJqpHPAaqVjS",  
        "transaction_number": "CR855-082-5464",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR5GA17zNQikNJqpHPAaqVjS",  
        "available_at": "2012-10-29T18:37:44.999643Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    GET /v1/marketplaces/(marketplace:marketplace)/credits/(credit:credit) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:37:46.390752Z",  
            "uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5I8YTjrf8PBq9AA4zj7bak",  
            "credits_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T11:37:46.455927Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:37:46.386841Z",  
            "uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/accounts/AC5I8YTjrf8PBq9AA4zj7bak/bank_accounts/BA5I8HgZONtAVTqssLXwIm3O",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5I8HgZONtAVTqssLXwIm3O" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5I2qu3fDmhMRgju5Lmgqvq/credits/CR5IcS0DqnmpYCH9wTZa5JoE",  
        "transaction_number": "CR784-649-9208",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR5IcS0DqnmpYCH9wTZa5JoE",  
        "available_at": "2012-10-29T18:37:46.439228Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T11:37:47.818282Z",  
                    "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5JKvXcjCbh5bY1GzvBG35y",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T11:37:47.889382Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T11:37:47.814189Z",  
                    "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/bank_accounts/BA5JKe1jufoiGKG655KsGpTu",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5JKe1jufoiGKG655KsGpTu" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/credits/CR5JOxa300qYY6z5xfap6qLq",  
                "transaction_number": "CR257-562-2256",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR5JOxa300qYY6z5xfap6qLq",  
                "available_at": "2012-10-29T18:37:47.869403Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T11:37:47.818282Z",  
                    "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5JKvXcjCbh5bY1GzvBG35y",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T11:37:47.889949Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T11:37:47.814189Z",  
                    "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/accounts/AC5JKvXcjCbh5bY1GzvBG35y/bank_accounts/BA5JKe1jufoiGKG655KsGpTu",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5JKe1jufoiGKG655KsGpTu" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/credits/CR5JOCGT4IXMrp5eLkicr4W0",  
                "transaction_number": "CR595-439-8614",  
                "amount": 431,  
                "meta": {},  
                "id": "CR5JOCGT4IXMrp5eLkicr4W0",  
                "available_at": "2012-10-29T18:37:47.876333Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5JEFH1JqNCUltpu9Xahlkw/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:37:51.113004Z",  
            "uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5NsgA8mmxKFZz9EusDAyLa",  
            "credits_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T11:37:51.181747Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:37:51.108830Z",  
            "uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/accounts/AC5NsgA8mmxKFZz9EusDAyLa/bank_accounts/BA5NrY0QuKWniQ1vBmpu6YjG",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5NrY0QuKWniQ1vBmpu6YjG" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5Nl6MdhLKMhLJm6QfE2f1W/credits/CR5NvXQZtXaRyLeualK83XXC",  
        "transaction_number": "CR513-623-5162",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR5NvXQZtXaRyLeualK83XXC",  
        "available_at": "2012-10-29T18:37:51.159617Z" 
    } 
 

