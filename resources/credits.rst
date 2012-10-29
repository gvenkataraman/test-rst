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
            "holds_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:45.465155Z",  
            "uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC76XNejuoHij5AfBCWrhJf6",  
            "credits_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T15:56:45.610712Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:56:45.460619Z",  
            "uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/accounts/AC76XNejuoHij5AfBCWrhJf6/bank_accounts/BA76Xswl4GeBlMcWHSEcnVhW",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA76Xswl4GeBlMcWHSEcnVhW" 
        },  
        "uri": "/v1/marketplaces/TEST-MP76QC8vRK1NPSIxhwcjA8JK/credits/CR7777MUHe5oqbGvAcGcrZYw",  
        "transaction_number": "CR108-235-8109",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR7777MUHe5oqbGvAcGcrZYw",  
        "available_at": "2012-10-29T22:56:45.598072Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:47.272861Z",  
            "uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC78ZR2zD818NdeIp4hLZl2c",  
            "credits_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:56:47.352466Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:56:47.268353Z",  
            "uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/accounts/AC78ZR2zD818NdeIp4hLZl2c/bank_accounts/BA78Zx7nVw5knJHlu7SiVnLK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA78Zx7nVw5knJHlu7SiVnLK" 
        },  
        "uri": "/v1/marketplaces/TEST-MP78U0fqSdlmmZDh5Ya1cPHu/credits/CR794E5HpGl6S7du4nfAMkdK",  
        "transaction_number": "CR880-735-9717",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR794E5HpGl6S7du4nfAMkdK",  
        "available_at": "2012-10-29T22:56:47.332564Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:56:48.858476Z",  
                    "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7aMqdj8K9HjdSiNimv0IPa",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:56:48.951689Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:56:48.854174Z",  
                    "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/bank_accounts/BA7aM746i33YQUMvrhRXTB2s",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA7aM746i33YQUMvrhRXTB2s" 
                },  
                "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/credits/CR7aRFj1EWo61xmMApTGnScY",  
                "transaction_number": "CR894-543-3567",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR7aRFj1EWo61xmMApTGnScY",  
                "available_at": "2012-10-29T22:56:48.924643Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:56:48.858476Z",  
                    "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC7aMqdj8K9HjdSiNimv0IPa",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:56:48.952362Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:56:48.854174Z",  
                    "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/accounts/AC7aMqdj8K9HjdSiNimv0IPa/bank_accounts/BA7aM746i33YQUMvrhRXTB2s",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA7aM746i33YQUMvrhRXTB2s" 
                },  
                "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/credits/CR7aRMLXb9iB9cyVstOseLC4",  
                "transaction_number": "CR308-532-6737",  
                "amount": 431,  
                "meta": {},  
                "id": "CR7aRMLXb9iB9cyVstOseLC4",  
                "available_at": "2012-10-29T22:56:48.934408Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP7aFrnaAS1Uc2c9jqEXCdU0/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:52.246106Z",  
            "uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC7eAEnpqBoXSqLF9Ibnau2g",  
            "credits_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:56:52.329978Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:56:52.241382Z",  
            "uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/accounts/AC7eAEnpqBoXSqLF9Ibnau2g/bank_accounts/BA7eAjwAzOlEpM4nFogVvsMs",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA7eAjwAzOlEpM4nFogVvsMs" 
        },  
        "uri": "/v1/marketplaces/TEST-MP7esRjiygNDhixoylA6q8bG/credits/CR7eFix9kcUdMekw3d4muqOg",  
        "transaction_number": "CR926-137-2095",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR7eFix9kcUdMekw3d4muqOg",  
        "available_at": "2012-10-29T22:56:52.306564Z" 
    } 
 

