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
            "holds_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:09:29.613234Z",  
            "uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1hpWnzAly4OJe4bTxza09m",  
            "credits_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T12:09:29.741326Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:09:29.608694Z",  
            "uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/accounts/AC1hpWnzAly4OJe4bTxza09m/bank_accounts/BA1hpCdUrlc9LeCbLhL27H7u",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1hpCdUrlc9LeCbLhL27H7u" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1hiAJZvoRpwJUoD9a2ZyBe/credits/CR1hyhuS117Dph1zAmxXET6A",  
        "transaction_number": "CR149-779-8092",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR1hyhuS117Dph1zAmxXET6A",  
        "available_at": "2012-10-29T19:09:29.732103Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:09:31.253726Z",  
            "uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1jgkS0IQIAqlNNMN2Z5aXG",  
            "credits_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:09:31.311387Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:09:31.249370Z",  
            "uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/accounts/AC1jgkS0IQIAqlNNMN2Z5aXG/bank_accounts/BA1jg1zXr52fsHo1QcWfcPSk",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1jg1zXr52fsHo1QcWfcPSk" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1j9NUhnz5XMMEMtImd1VAw/credits/CR1jjO048wCv8w2U0CmYYZ6Y",  
        "transaction_number": "CR577-100-4566",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR1jjO048wCv8w2U0CmYYZ6Y",  
        "available_at": "2012-10-29T19:09:31.297638Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:09:32.774171Z",  
                    "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1kYmoXBUkfsyXJubKRzwmU",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:09:32.845605Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:09:32.770505Z",  
                    "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/bank_accounts/BA1kY6z58GLjlocg0qm12HZi",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1kY6z58GLjlocg0qm12HZi" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/credits/CR1l2cRHlME67N5imSjqVpNa",  
                "transaction_number": "CR486-416-0455",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR1l2cRHlME67N5imSjqVpNa",  
                "available_at": "2012-10-29T19:09:32.821714Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:09:32.774171Z",  
                    "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1kYmoXBUkfsyXJubKRzwmU",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:09:32.846477Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:09:32.770505Z",  
                    "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/accounts/AC1kYmoXBUkfsyXJubKRzwmU/bank_accounts/BA1kY6z58GLjlocg0qm12HZi",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1kY6z58GLjlocg0qm12HZi" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/credits/CR1l2kNj8nPT0BikMYZ3qFEM",  
                "transaction_number": "CR305-555-7218",  
                "amount": 431,  
                "meta": {},  
                "id": "CR1l2kNj8nPT0BikMYZ3qFEM",  
                "available_at": "2012-10-29T19:09:32.830250Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1kS4qzmbQGXSUz40Kg4tI8/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:09:36.048438Z",  
            "uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1oEBQ0MVBBKuC5SmmWCOGw",  
            "credits_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:09:36.114554Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:09:36.044136Z",  
            "uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/accounts/AC1oEBQ0MVBBKuC5SmmWCOGw/bank_accounts/BA1oEoeZ6VRkpVH36SWBk2q0",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1oEoeZ6VRkpVH36SWBk2q0" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1oxO1WG79Qozbw0UZk7zGA/credits/CR1oIaE1kNbRYbPro8qdUPnm",  
        "transaction_number": "CR719-437-7588",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR1oIaE1kNbRYbPro8qdUPnm",  
        "available_at": "2012-10-29T19:09:36.091610Z" 
    } 
 

