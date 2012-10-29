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
            "holds_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:24.703979Z",  
            "uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC25Ih9IGD15FM3EZfYnACvq",  
            "credits_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T16:49:24.842310Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:24.699903Z",  
            "uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/accounts/AC25Ih9IGD15FM3EZfYnACvq/bank_accounts/BA25HYWWQiJERjw8CuWEXzV2",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA25HYWWQiJERjw8CuWEXzV2" 
        },  
        "uri": "/v1/marketplaces/TEST-MP25ASh68xOuwSvB6UjDziFm/credits/CR25Rd6ifZeAOBvMt5UZKdko",  
        "transaction_number": "CR275-323-4081",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR25Rd6ifZeAOBvMt5UZKdko",  
        "available_at": "2012-10-29T23:49:24.831294Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:26.362183Z",  
            "uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC27zTStcDewxXpw1AOiTqtK",  
            "credits_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T16:49:26.449236Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:26.357780Z",  
            "uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/accounts/AC27zTStcDewxXpw1AOiTqtK/bank_accounts/BA27zAMdail0VqL2RMbQ22sA",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA27zAMdail0VqL2RMbQ22sA" 
        },  
        "uri": "/v1/marketplaces/TEST-MP27szbRmQtZXAUmoFS9NKgA/credits/CR27FeW6lyTrjnEjL6isty4I",  
        "transaction_number": "CR650-163-7762",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR27FeW6lyTrjnEjL6isty4I",  
        "available_at": "2012-10-29T23:49:26.429655Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:27.852633Z",  
                    "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC29fQ59aFfABhWPbaDRJlc0",  
                    "credits_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T16:49:27.947708Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:49:27.848188Z",  
                    "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/bank_accounts/BA29fwuB9yHe2huJDzkSryio",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA29fwuB9yHe2huJDzkSryio" 
                },  
                "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/credits/CR29lf0GAb6Z8ypuJlIH3CbG",  
                "transaction_number": "CR025-785-4299",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR29lf0GAb6Z8ypuJlIH3CbG",  
                "available_at": "2012-10-29T23:49:27.921546Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:49:27.852633Z",  
                    "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC29fQ59aFfABhWPbaDRJlc0",  
                    "credits_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T16:49:27.948438Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T16:49:27.848188Z",  
                    "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/accounts/AC29fQ59aFfABhWPbaDRJlc0/bank_accounts/BA29fwuB9yHe2huJDzkSryio",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA29fwuB9yHe2huJDzkSryio" 
                },  
                "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/credits/CR29lmZMpVCPUVk6ieeWphXu",  
                "transaction_number": "CR861-135-4246",  
                "amount": 431,  
                "meta": {},  
                "id": "CR29lmZMpVCPUVk6ieeWphXu",  
                "available_at": "2012-10-29T23:49:27.931005Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP298wflkVtRw6fpCppFUBIo/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:31.198250Z",  
            "uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2d18Q0x4KE87nEq5uZGdgM",  
            "credits_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T16:49:31.273589Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T16:49:31.194811Z",  
            "uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/accounts/AC2d18Q0x4KE87nEq5uZGdgM/bank_accounts/BA2d0TF8OtnGaZECdIjPpoyw",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2d0TF8OtnGaZECdIjPpoyw" 
        },  
        "uri": "/v1/marketplaces/TEST-MP2cUhxm29789I7GQdvYanWc/credits/CR2d53cwSjdthpDVqtzbQDA0",  
        "transaction_number": "CR776-132-1962",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR2d53cwSjdthpDVqtzbQDA0",  
        "available_at": "2012-10-29T23:49:31.246958Z" 
    } 
 

