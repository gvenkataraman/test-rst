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
            "holds_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:54:23.706295Z",  
            "uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1z2wogjD2UhjgBRDNsvfBG",  
            "credits_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T14:54:23.828382Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:54:23.701583Z",  
            "uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/accounts/AC1z2wogjD2UhjgBRDNsvfBG/bank_accounts/BA1z2cgK7NcpsVHHdlV9PF8o",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1z2cgK7NcpsVHHdlV9PF8o" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1yV9WhOcrNg9khulBuIUWU/credits/CR1zamqg1K6MMrlyy2q6aJhy",  
        "transaction_number": "CR271-275-1730",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR1zamqg1K6MMrlyy2q6aJhy",  
        "available_at": "2012-10-29T21:54:23.817712Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:54:25.241418Z",  
            "uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1ALAcmeK1OPqgDFlLRa912",  
            "credits_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T14:54:25.320335Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:54:25.237049Z",  
            "uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/accounts/AC1ALAcmeK1OPqgDFlLRa912/bank_accounts/BA1ALgKEEI44LL8wIk54Dzq4",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1ALgKEEI44LL8wIk54Dzq4" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1AEfUFZNFAzKWGYpKEA4hS/credits/CR1AQn3GLRyXzcu6xTfoWb8o",  
        "transaction_number": "CR166-076-5621",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR1AQn3GLRyXzcu6xTfoWb8o",  
        "available_at": "2012-10-29T21:54:25.302078Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:54:26.871420Z",  
                    "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1CBfpK8pLfleynWfIaSqb2",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T14:54:26.965553Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T14:54:26.867132Z",  
                    "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/bank_accounts/BA1CAWneLCKJ99JBouVC9N8o",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1CAWneLCKJ99JBouVC9N8o" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/credits/CR1CGE5t0ynTA2hWCjtxKE3G",  
                "transaction_number": "CR041-233-8764",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR1CGE5t0ynTA2hWCjtxKE3G",  
                "available_at": "2012-10-29T21:54:26.939827Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:54:26.871420Z",  
                    "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1CBfpK8pLfleynWfIaSqb2",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T14:54:26.966349Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T14:54:26.867132Z",  
                    "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/accounts/AC1CBfpK8pLfleynWfIaSqb2/bank_accounts/BA1CAWneLCKJ99JBouVC9N8o",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1CAWneLCKJ99JBouVC9N8o" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/credits/CR1CGLFTRR4nyB9sIv47T3pO",  
                "transaction_number": "CR583-539-5419",  
                "amount": 431,  
                "meta": {},  
                "id": "CR1CGLFTRR4nyB9sIv47T3pO",  
                "available_at": "2012-10-29T21:54:26.949627Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1CtSGBZD6Knaelkogmal3C/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:54:29.986817Z",  
            "uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1G6uOSyKUOKAvGwKPYzpWc",  
            "credits_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T14:54:30.082685Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T14:54:29.983066Z",  
            "uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/accounts/AC1G6uOSyKUOKAvGwKPYzpWc/bank_accounts/BA1G6efqObA8sftIJFpHKPHK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1G6efqObA8sftIJFpHKPHK" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1G0NsD6jtJOCHe2JkVeqJm/credits/CR1GbJqj6bumwqcxW5GDwary",  
        "transaction_number": "CR795-043-5410",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR1GbJqj6bumwqcxW5GDwary",  
        "available_at": "2012-10-29T21:54:30.053722Z" 
    } 
 

