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
        "account_uri": "/v1/marketplaces/TEST-MP22rgR76lq39N27h8R8gq8c/accounts/AC22wYJNuJ1phlH9VgWWowM4" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:33:31.252270Z",  
            "uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC23Vs40VXBqP4kVtso7s8NS",  
            "credits_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-28T17:33:31.347604Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:33:31.249275Z",  
            "uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/accounts/AC23Vs40VXBqP4kVtso7s8NS/bank_accounts/BA23VerE9Z2vQ3Lhlx1nFFbK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA23VerE9Z2vQ3Lhlx1nFFbK" 
        },  
        "uri": "/v1/marketplaces/TEST-MP23QC8DjWEoYQg0Ed9MXafO/credits/CR241z3ONLJ1s2Q5pYVqUlrC",  
        "transaction_number": "CR954-359-0162",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR241z3ONLJ1s2Q5pYVqUlrC",  
        "available_at": "2012-10-29T00:33:31.339374Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:33:32.526345Z",  
            "uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC25mhAIowxGMkabNW3r2SK8",  
            "credits_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-28T17:33:32.601825Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:33:32.522167Z",  
            "uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/accounts/AC25mhAIowxGMkabNW3r2SK8/bank_accounts/BA25lZ5rORoemvAlQ9Pt0olu",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA25lZ5rORoemvAlQ9Pt0olu" 
        },  
        "uri": "/v1/marketplaces/TEST-MP25eRa88BETJ5IYNIyP7TWA/credits/CR25qLJE0zjU6InUztSlhM32",  
        "transaction_number": "CR071-046-6928",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR25qLJE0zjU6InUztSlhM32",  
        "available_at": "2012-10-29T00:33:32.581905Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T17:33:33.773234Z",  
                    "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC26LeyHHZtteywVdaQpzegQ",  
                    "credits_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T17:33:33.833813Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T17:33:33.768893Z",  
                    "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/bank_accounts/BA26KVjRQYygDzGAW4B1eY1m",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "x234",  
                    "id": "BA26KVjRQYygDzGAW4B1eY1m" 
                },  
                "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/credits/CR26OFrUkryJa6VAIIbUf0j2",  
                "transaction_number": "CR686-836-8243",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR26OFrUkryJa6VAIIbUf0j2",  
                "available_at": "2012-10-29T00:33:33.816358Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-28T17:33:33.773234Z",  
                    "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC26LeyHHZtteywVdaQpzegQ",  
                    "credits_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-28T17:33:33.834335Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-28T17:33:33.768893Z",  
                    "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/accounts/AC26LeyHHZtteywVdaQpzegQ/bank_accounts/BA26KVjRQYygDzGAW4B1eY1m",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "x234",  
                    "id": "BA26KVjRQYygDzGAW4B1eY1m" 
                },  
                "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/credits/CR26OKmGsU5Lj8QCRAY5zozO",  
                "transaction_number": "CR237-564-2163",  
                "amount": 431,  
                "meta": {},  
                "id": "CR26OKmGsU5Lj8QCRAY5zozO",  
                "available_at": "2012-10-29T00:33:33.822817Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP26EYWWcZ9tUh7GcHtoS4Kw/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-28T17:33:36.371166Z",  
            "uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC29Gp3zmKEkEZ34sMnD7Kde",  
            "credits_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-28T17:33:36.435060Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-28T17:33:36.367831Z",  
            "uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/accounts/AC29Gp3zmKEkEZ34sMnD7Kde/bank_accounts/BA29GaepOeUwFSVNwUg3Os96",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "x234",  
            "id": "BA29GaepOeUwFSVNwUg3Os96" 
        },  
        "uri": "/v1/marketplaces/TEST-MP29BcAyL2naWq3KqLMMiS9e/credits/CR29JK6DjXDYVduUJlrfap3C",  
        "transaction_number": "CR611-896-1760",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR29JK6DjXDYVduUJlrfap3C",  
        "available_at": "2012-10-29T00:33:36.412307Z" 
    } 
 

