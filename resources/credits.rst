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
        "amount": 1234 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:07.634272Z",  
            "uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4c3eAwqdmITs8p5jYJ0TVa",  
            "credits_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T15:11:07.771055Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:07.630122Z",  
            "uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/accounts/AC4c3eAwqdmITs8p5jYJ0TVa/bank_accounts/BA4c2VFwow8bygYZLGRYzMPy",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4c2VFwow8bygYZLGRYzMPy" 
        },  
        "uri": "/v1/marketplaces/TEST-MP4bVIquYXtwr81nEnUcRiFS/credits/CR4cc0aQajMX1JLKDZMWqfHe",  
        "transaction_number": "CR746-887-6902",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR4cc0aQajMX1JLKDZMWqfHe",  
        "available_at": "2012-10-29T22:11:07.759188Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:09.466968Z",  
            "uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4e71PU0619ApFC8W5Wp3TK",  
            "credits_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:11:09.538228Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:09.462548Z",  
            "uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/accounts/AC4e71PU0619ApFC8W5Wp3TK/bank_accounts/BA4e6IGqx0mvBdrHjDC7ZB2I",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4e6IGqx0mvBdrHjDC7ZB2I" 
        },  
        "uri": "/v1/marketplaces/TEST-MP4e0kteDAXYDpoCbNnYEaMs/credits/CR4ebxmBMV4iFlNU5kc7iHvS",  
        "transaction_number": "CR088-272-2194",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR4ebxmBMV4iFlNU5kc7iHvS",  
        "available_at": "2012-10-29T22:11:09.525324Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:11.072813Z",  
                    "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4fV0Qp4zf99AIdSYi4pKGE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:11:11.166533Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:11:11.068367Z",  
                    "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/bank_accounts/BA4fUGU8Tn3CCyEn4RVuar8U",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA4fUGU8Tn3CCyEn4RVuar8U" 
                },  
                "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/credits/CR4g0pa9adFHTtHTPf0z26QQ",  
                "transaction_number": "CR393-224-9858",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR4g0pa9adFHTtHTPf0z26QQ",  
                "available_at": "2012-10-29T22:11:11.141117Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:11.072813Z",  
                    "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC4fV0Qp4zf99AIdSYi4pKGE",  
                    "credits_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:11:11.167285Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:11:11.068367Z",  
                    "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/accounts/AC4fV0Qp4zf99AIdSYi4pKGE/bank_accounts/BA4fUGU8Tn3CCyEn4RVuar8U",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA4fUGU8Tn3CCyEn4RVuar8U" 
                },  
                "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/credits/CR4g0wFdDB5DgfX0tCPzfIOw",  
                "transaction_number": "CR177-670-4383",  
                "amount": 431,  
                "meta": {},  
                "id": "CR4g0wFdDB5DgfX0tCPzfIOw",  
                "available_at": "2012-10-29T22:11:11.150988Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4fNyWGfWORK1K2g6KBVebq/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:14.380321Z",  
            "uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC4jDEDqGdqQ1NzQWzORo4xC",  
            "credits_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:11:14.480188Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:11:14.375932Z",  
            "uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/accounts/AC4jDEDqGdqQ1NzQWzORo4xC/bank_accounts/BA4jDl7azrTjX1dGXCkkPILa",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA4jDl7azrTjX1dGXCkkPILa" 
        },  
        "uri": "/v1/marketplaces/TEST-MP4jwkOXWstKB3x2Kgx432pC/credits/CR4jIYzmO8CuS1LjQEku3Q0I",  
        "transaction_number": "CR415-189-6526",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR4jIYzmO8CuS1LjQEku3Q0I",  
        "available_at": "2012-10-29T22:11:14.447687Z" 
    } 
 

