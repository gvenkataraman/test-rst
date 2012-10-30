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
 
    POST /v1/marketplaces/(marketplace-id)/accounts/(account-id)/credits 
    POST /v1/marketplaces/(marketplace-id)/credits 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:00.453542Z",  
            "uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/transactions",  
            "email_address": "email.7@y.com",  
            "id": "ACMYSWZZHSHvzdqPQUNnBbK",  
            "credits_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-30T09:59:00.565392Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:00.449267Z",  
            "uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/accounts/ACMYSWZZHSHvzdqPQUNnBbK/bank_accounts/BAMYzGhNV10cmsgfIKrYXs0",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BAMYzGhNV10cmsgfIKrYXs0" 
        },  
        "uri": "/v1/marketplaces/TEST-MPMRe8BlGIKzW1f5m74jZqY/credits/CRN63kzqZB5s3tgd5zTh7bS",  
        "transaction_number": "CR933-295-5512",  
        "amount": 1234,  
        "meta": {},  
        "id": "CRN63kzqZB5s3tgd5zTh7bS",  
        "available_at": "2012-10-30T16:59:00.555584Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/credits/(credit-id) 
    GET /v1/marketplaces/(marketplace-id)/credits/(credit-id) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:01.997984Z",  
            "uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/transactions",  
            "email_address": "email.7@y.com",  
            "id": "ACOIA7ZcsLawUVXLGtY3zvK",  
            "credits_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-30T09:59:02.086734Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:01.993663Z",  
            "uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/accounts/ACOIA7ZcsLawUVXLGtY3zvK/bank_accounts/BAOIh6yjg0msoDF75EwwiKo",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BAOIh6yjg0msoDF75EwwiKo" 
        },  
        "uri": "/v1/marketplaces/TEST-MPOB7yIor13TwF5UQKgIncw/credits/CROO2osHPwUAEvG1QA9Kcks",  
        "transaction_number": "CR715-931-0883",  
        "amount": 1254,  
        "meta": {},  
        "id": "CROO2osHPwUAEvG1QA9Kcks",  
        "available_at": "2012-10-30T16:59:02.067267Z" 
    } 
 

List All Credits
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/credits 
    GET /v1/marketplaces/(marketplace-id)/credits 
 

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
        "first_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:03.524663Z",  
                    "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "ACQr2zzbLf4Ks9mWqh0kDEU",  
                    "credits_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T09:59:03.618781Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T09:59:03.520446Z",  
                    "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/bank_accounts/BAQqK0xWycCUbJQmAd89ohK",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BAQqK0xWycCUbJQmAd89ohK" 
                },  
                "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/credits/CRQwrjjlQjDWAQJHPRyDXAo",  
                "transaction_number": "CR884-659-2335",  
                "amount": 1254,  
                "meta": {},  
                "id": "CRQwrjjlQjDWAQJHPRyDXAo",  
                "available_at": "2012-10-30T16:59:03.593099Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:03.524663Z",  
                    "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "ACQr2zzbLf4Ks9mWqh0kDEU",  
                    "credits_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T09:59:03.619507Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T09:59:03.520446Z",  
                    "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/accounts/ACQr2zzbLf4Ks9mWqh0kDEU/bank_accounts/BAQqK0xWycCUbJQmAd89ohK",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BAQqK0xWycCUbJQmAd89ohK" 
                },  
                "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/credits/CRQwyUOGJfQ2IeJHbpfXJdO",  
                "transaction_number": "CR710-544-9791",  
                "amount": 431,  
                "meta": {},  
                "id": "CRQwyUOGJfQ2IeJHbpfXJdO",  
                "available_at": "2012-10-30T16:59:03.602890Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MPQjDTh7TXa0sCQNq55UX1G/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/credits 
    GET /v1/marketplaces/(marketplace-id)/credits 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:06.776956Z",  
            "uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/transactions",  
            "email_address": "email.7@y.com",  
            "id": "ACU5Q2HuBHxsLz7jNMeru4c",  
            "credits_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-30T09:59:06.857568Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:06.773333Z",  
            "uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/accounts/ACU5Q2HuBHxsLz7jNMeru4c/bank_accounts/BAU5zByWjPCBZATaHZBNqZK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BAU5zByWjPCBZATaHZBNqZK" 
        },  
        "uri": "/v1/marketplaces/TEST-MPTZ33z34i4TN1rdubC8Ojy/credits/CRU9TpQruc87aMyQPBN47FG",  
        "transaction_number": "CR328-226-6766",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CRU9TpQruc87aMyQPBN47FG",  
        "available_at": "2012-10-30T16:59:06.827767Z" 
    } 
 

