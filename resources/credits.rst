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
            "holds_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:59:51.717096Z",  
            "uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2HnDUWACtP9ISPekUfA4yE",  
            "credits_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T15:59:51.860756Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:59:51.712682Z",  
            "uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/accounts/AC2HnDUWACtP9ISPekUfA4yE/bank_accounts/BA2HnkpKXrc1cv398xmQd53u",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2HnkpKXrc1cv398xmQd53u" 
        },  
        "uri": "/v1/marketplaces/TEST-MP2HgiSCAK68BkLUkUUvwRHm/credits/CR2HwSjiGuwIOOddxbecVJS4",  
        "transaction_number": "CR184-073-6274",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR2HwSjiGuwIOOddxbecVJS4",  
        "available_at": "2012-10-29T22:59:51.848678Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:59:53.187153Z",  
            "uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2J29GAUJ6tqiDcmioK3MlC",  
            "credits_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:59:53.274388Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:59:53.183053Z",  
            "uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/accounts/AC2J29GAUJ6tqiDcmioK3MlC/bank_accounts/BA2J1RqSg2CPM3ElNluXaZZG",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2J1RqSg2CPM3ElNluXaZZG" 
        },  
        "uri": "/v1/marketplaces/TEST-MP2IUKgJzw2Ov8QbTYbpmjRy/credits/CR2J7uxmkDIQJ2AdpSrvrAB6",  
        "transaction_number": "CR228-569-6642",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR2J7uxmkDIQJ2AdpSrvrAB6",  
        "available_at": "2012-10-29T22:59:53.254916Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:59:54.781886Z",  
                    "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2KPmoWtPFHD0v6HPw4XFgo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:59:54.876149Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:59:54.777524Z",  
                    "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/bank_accounts/BA2KP33WnHN9PzE0z3xgPApu",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2KP33WnHN9PzE0z3xgPApu" 
                },  
                "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/credits/CR2KUJEKe1vZS9h8qJ5WOqhe",  
                "transaction_number": "CR640-360-4095",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR2KUJEKe1vZS9h8qJ5WOqhe",  
                "available_at": "2012-10-29T22:59:54.850544Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:59:54.781886Z",  
                    "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC2KPmoWtPFHD0v6HPw4XFgo",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T15:59:54.876906Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T15:59:54.777524Z",  
                    "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/accounts/AC2KPmoWtPFHD0v6HPw4XFgo/bank_accounts/BA2KP33WnHN9PzE0z3xgPApu",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA2KP33WnHN9PzE0z3xgPApu" 
                },  
                "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/credits/CR2KUR6kEfBRlmOFWl4kbCkI",  
                "transaction_number": "CR913-631-6425",  
                "amount": 431,  
                "meta": {},  
                "id": "CR2KUR6kEfBRlmOFWl4kbCkI",  
                "available_at": "2012-10-29T22:59:54.859792Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP2KI2KoEJyWPaiKZfNBzcIk/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:59:57.899239Z",  
            "uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2OkK4AZFXrixVMBEokmubi",  
            "credits_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T15:59:57.995597Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T15:59:57.895004Z",  
            "uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/accounts/AC2OkK4AZFXrixVMBEokmubi/bank_accounts/BA2OkrkAmdOWHP9jEUO13iWU",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA2OkrkAmdOWHP9jEUO13iWU" 
        },  
        "uri": "/v1/marketplaces/TEST-MP2OdpPRz5NpSF3a6Ufc29dG/credits/CR2Oq6eQG1PTRBHrhqTTFBCQ",  
        "transaction_number": "CR453-836-7884",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR2Oq6eQG1PTRBHrhqTTFBCQ",  
        "available_at": "2012-10-29T22:59:57.967706Z" 
    } 
 

