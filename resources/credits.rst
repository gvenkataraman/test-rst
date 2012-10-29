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
        "account_uri": "/v1/marketplaces/TEST-MP5voO74fmGme83OYp6IBv2Q/accounts/AC5vw3JfEqCrzrVBrZGDIytC" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:44:46.327438Z",  
            "uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5xok09sIopc4iy6YUE3GC0",  
            "credits_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T11:44:46.433428Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:44:46.323007Z",  
            "uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/accounts/AC5xok09sIopc4iy6YUE3GC0/bank_accounts/BA5xo0kMitHl53ui49ODrMsA",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5xo0kMitHl53ui49ODrMsA" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5xgyV4QemZ55bBlMYq5jLu/credits/CR5xvb9XwzriF8ex6hhsOiDW",  
        "transaction_number": "CR291-437-0809",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR5xvb9XwzriF8ex6hhsOiDW",  
        "available_at": "2012-10-29T18:44:46.425038Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:44:47.825510Z",  
            "uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5z4MAOyyus0soDM7BxJk8Y",  
            "credits_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T11:44:47.882526Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:44:47.821207Z",  
            "uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/accounts/AC5z4MAOyyus0soDM7BxJk8Y/bank_accounts/BA5z4tKDFZoCdhBoXIhOCkja",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5z4tKDFZoCdhBoXIhOCkja" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5yYW6HLLOyfn5L0CEAWWLa/credits/CR5z8cpxAKRAnujq7HPR2OTa",  
        "transaction_number": "CR916-697-9240",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR5z8cpxAKRAnujq7HPR2OTa",  
        "available_at": "2012-10-29T18:44:47.868204Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T11:44:49.270868Z",  
                    "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5AHzdQaQExFyvuO6qG0VqQ",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T11:44:49.341076Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T11:44:49.267070Z",  
                    "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/bank_accounts/BA5AHjEQIAA3YoZC5Cip7wry",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5AHjEQIAA3YoZC5Cip7wry" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/credits/CR5ALutQI5JrCUSIBy5CpHaQ",  
                "transaction_number": "CR705-200-6734",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR5ALutQI5JrCUSIBy5CpHaQ",  
                "available_at": "2012-10-29T18:44:49.320848Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T11:44:49.270868Z",  
                    "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5AHzdQaQExFyvuO6qG0VqQ",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T11:44:49.341672Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T11:44:49.267070Z",  
                    "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/accounts/AC5AHzdQaQExFyvuO6qG0VqQ/bank_accounts/BA5AHjEQIAA3YoZC5Cip7wry",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5AHjEQIAA3YoZC5Cip7wry" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/credits/CR5ALBp0cnF1UxzFX3teZLNi",  
                "transaction_number": "CR632-516-9667",  
                "amount": 431,  
                "meta": {},  
                "id": "CR5ALBp0cnF1UxzFX3teZLNi",  
                "available_at": "2012-10-29T18:44:49.327614Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5ABj1CrXImclhRyaDJ5yqE/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T11:44:52.646082Z",  
            "uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5EuWsHH1TfJX9P42kXlyjq",  
            "credits_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T11:44:52.719073Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T11:44:52.641817Z",  
            "uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/accounts/AC5EuWsHH1TfJX9P42kXlyjq/bank_accounts/BA5EuD1xlN3mK4hX3ACJpER6",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5EuD1xlN3mK4hX3ACJpER6" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5En48DKWfA5xEZZRSsTXGA/credits/CR5EyG15NNYiIdYN15tK0okc",  
        "transaction_number": "CR210-542-9744",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR5EyG15NNYiIdYN15tK0okc",  
        "available_at": "2012-10-29T18:44:52.691878Z" 
    } 
 

