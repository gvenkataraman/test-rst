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
            "holds_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:05:52.315807Z",  
            "uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC585cGvtEHzM6e2vrzj0CUc",  
            "credits_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T12:05:52.435656Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:05:52.311518Z",  
            "uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/accounts/AC585cGvtEHzM6e2vrzj0CUc/bank_accounts/BA584TIPfZPL81LqsUzLC77m",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA584TIPfZPL81LqsUzLC77m" 
        },  
        "uri": "/v1/marketplaces/TEST-MP57XCQUg2wzWPUGZbmWIvt2/credits/CR58cU5JHnSgZg0xI1opy8uw",  
        "transaction_number": "CR310-837-0829",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR58cU5JHnSgZg0xI1opy8uw",  
        "available_at": "2012-10-29T19:05:52.425481Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:05:54.001482Z",  
            "uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC59YKXsGULBeC25wYkMsOfW",  
            "credits_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:05:54.073966Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:05:53.997550Z",  
            "uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/accounts/AC59YKXsGULBeC25wYkMsOfW/bank_accounts/BA59YtpYdBf475F7UTw1o6pe",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA59YtpYdBf475F7UTw1o6pe" 
        },  
        "uri": "/v1/marketplaces/TEST-MP59REMHP7c4rkdwP2m7nX5G/credits/CR5a2ZLl3iLAs5yc97pVbYck",  
        "transaction_number": "CR289-115-7819",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR5a2ZLl3iLAs5yc97pVbYck",  
        "available_at": "2012-10-29T19:05:54.054350Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:05:55.669171Z",  
                    "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5bR3415boZMi9qOmXmU5H6",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:05:55.738598Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:05:55.665415Z",  
                    "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/bank_accounts/BA5bQMacgvfNanaj7epTBGa8",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5bQMacgvfNanaj7epTBGa8" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/credits/CR5bUONvjDpI6IZ8REeKEcQs",  
                "transaction_number": "CR290-538-7674",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR5bUONvjDpI6IZ8REeKEcQs",  
                "available_at": "2012-10-29T19:05:55.716460Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:05:55.669171Z",  
                    "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5bR3415boZMi9qOmXmU5H6",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:05:55.739479Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:05:55.665415Z",  
                    "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/accounts/AC5bR3415boZMi9qOmXmU5H6/bank_accounts/BA5bQMacgvfNanaj7epTBGa8",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5bQMacgvfNanaj7epTBGa8" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/credits/CR5bUUz5s8VxKVHV4GITfxQM",  
                "transaction_number": "CR207-969-1326",  
                "amount": 431,  
                "meta": {},  
                "id": "CR5bUUz5s8VxKVHV4GITfxQM",  
                "available_at": "2012-10-29T19:05:55.723786Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5bKtVZtpxuneo1OW5PEAok/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:05:59.274815Z",  
            "uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5fUt1cvcaMZtD01TX38SeU",  
            "credits_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:05:59.353641Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:05:59.271330Z",  
            "uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/accounts/AC5fUt1cvcaMZtD01TX38SeU/bank_accounts/BA5fUeMLMXC6GcseOMeHm8IY",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5fUeMLMXC6GcseOMeHm8IY" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5fO4s1PiAawKQ2agG1xAgc/credits/CR5fYGIsk9XepjCfHM0M92kI",  
        "transaction_number": "CR091-353-6462",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR5fYGIsk9XepjCfHM0M92kI",  
        "available_at": "2012-10-29T19:05:59.327395Z" 
    } 
 

