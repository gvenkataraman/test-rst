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
    *required* **integer** or *null*. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description`` 
    *optional* **string** or *null*.  
 
``meta`` 
    *optional* **object** or *null*. Single level mapping from string keys to string values. 
 
``appears_on_statement_as`` 
    *optional* **string** or *null*. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``destination_uri`` 
    *optional* **string** or *null*.  
 
``bank_account_uri`` 
    *optional* **string** or *null*.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 1234,  
        "account_uri": "/v1/marketplaces/TEST-MP7tHC9HOMRnZmy9TKkoSafG/accounts/AC7tOwFN4tDgDlfMXtEYsPsg" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:31:21.662451Z",  
            "uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7veNZo42KXYi9ODncqRwoY",  
            "credits_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-28T17:31:21.763617Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:31:21.658053Z",  
            "uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/accounts/AC7veNZo42KXYi9ODncqRwoY/bank_accounts/BA7veurfCvgXbhSOlnMXeN8g",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA7veurfCvgXbhSOlnMXeN8g" 
        },  
        "uri": "/v1/marketplaces/TEST-MP7v7nZ4uX56UcypVAz9VQr2/credits/CR7vlkSigceT3QWFre6bAEwk",  
        "transaction_number": "CR197-524-5032",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR7vlkSigceT3QWFre6bAEwk",  
        "available_at": "2012-10-29T00:31:21.755352Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:31:22.930541Z",  
            "uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7wFe8STpnjALAtSbvS2K5C",  
            "credits_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-28T17:31:22.982346Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:31:22.926059Z",  
            "uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/accounts/AC7wFe8STpnjALAtSbvS2K5C/bank_accounts/BA7wEUvo3WCKbYH48okOvdqs",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA7wEUvo3WCKbYH48okOvdqs" 
        },  
        "uri": "/v1/marketplaces/TEST-MP7wyOmocbtX4aZEg1vsjXwg/credits/CR7wIe7J219fRSN11Vf5Doc4",  
        "transaction_number": "CR233-783-9800",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR7wIe7J219fRSN11Vf5Doc4",  
        "available_at": "2012-10-29T00:31:22.966783Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T17:31:24.154766Z",  
                    "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7y2BdSMTqgEn5xtmwVO2Gg",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T17:31:24.237000Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T17:31:24.150356Z",  
                    "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/bank_accounts/BA7y2hBZFO3gqUYQzjhy2yr2",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "x234",  
                    "id": "BA7y2hBZFO3gqUYQzjhy2yr2" 
                },  
                "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/credits/CR7y77kvyNXKOsLYID4uldDC",  
                "transaction_number": "CR038-809-4729",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR7y77kvyNXKOsLYID4uldDC",  
                "available_at": "2012-10-29T00:31:24.211197Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T17:31:24.154766Z",  
                    "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7y2BdSMTqgEn5xtmwVO2Gg",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T17:31:24.237724Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T17:31:24.150356Z",  
                    "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/accounts/AC7y2BdSMTqgEn5xtmwVO2Gg/bank_accounts/BA7y2hBZFO3gqUYQzjhy2yr2",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "x234",  
                    "id": "BA7y2hBZFO3gqUYQzjhy2yr2" 
                },  
                "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/credits/CR7y7eLyKeVLdU3hhF4j7Jys",  
                "transaction_number": "CR798-098-8350",  
                "amount": 431,  
                "meta": {},  
                "id": "CR7y7eLyKeVLdU3hhF4j7Jys",  
                "available_at": "2012-10-29T00:31:24.220338Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP7xV7DT49R1SUat4DvXfk3y/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description`` 
    *optional* **string** or *null*.  
 
``meta`` 
    *optional* **object** or *null*. Single level mapping from string keys to string values. 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:31:26.761383Z",  
            "uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7AYnHkjJ5TJAIvxxXZBSXq",  
            "credits_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-28T17:31:26.822016Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:31:26.758482Z",  
            "uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/accounts/AC7AYnHkjJ5TJAIvxxXZBSXq/bank_accounts/BA7AYaCckSo2wQnNZB9QvxZi",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA7AYaCckSo2wQnNZB9QvxZi" 
        },  
        "uri": "/v1/marketplaces/TEST-MP7ASY9slyFOlawBqSygZ0ZC/credits/CR7B1urp1XX5FqLxz3vvQ26o",  
        "transaction_number": "CR522-527-1967",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR7B1urp1XX5FqLxz3vvQ26o",  
        "available_at": "2012-10-29T00:31:26.799956Z" 
    } 
 

