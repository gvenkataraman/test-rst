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
            "holds_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:15.103883Z",  
            "uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5eI9hYYWWmdB13LV0brWIs",  
            "credits_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-30T10:10:15.247816Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:15.099587Z",  
            "uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/accounts/AC5eI9hYYWWmdB13LV0brWIs/bank_accounts/BA5eHQep8zG7TXFNl0gvxXow",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5eHQep8zG7TXFNl0gvxXow" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5eC86aPdoX0PpLi2Qwg8HW/credits/CR5eRoZPlgfl90a5GXMWIVdW",  
        "transaction_number": "CR172-339-2137",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR5eRoZPlgfl90a5GXMWIVdW",  
        "available_at": "2012-10-30T17:10:15.235805Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:16.571605Z",  
            "uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5gmuRz0RaZDtgYUAiTgG7W",  
            "credits_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-30T10:10:16.640905Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:16.567350Z",  
            "uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/accounts/AC5gmuRz0RaZDtgYUAiTgG7W/bank_accounts/BA5gmbUXgMyT6XkQLdgt3wCo",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5gmbUXgMyT6XkQLdgt3wCo" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5gf7SCkHhKmWdPqBxC6xTu/credits/CR5gqJVwx0YEGiEjS8GLKefG",  
        "transaction_number": "CR766-777-1957",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR5gqJVwx0YEGiEjS8GLKefG",  
        "available_at": "2012-10-30T17:10:16.623225Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:17.947470Z",  
                    "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5hUrduR2KTuijctdgP89ec",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T10:10:18.020744Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T10:10:17.943033Z",  
                    "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/bank_accounts/BA5hU7CpB94FRvARZ1ZhfGbW",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5hU7CpB94FRvARZ1ZhfGbW" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/credits/CR5hYv1YYkI8foSWbPUPVrWA",  
                "transaction_number": "CR714-068-3242",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR5hYv1YYkI8foSWbPUPVrWA",  
                "available_at": "2012-10-30T17:10:17.998738Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:17.947470Z",  
                    "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5hUrduR2KTuijctdgP89ec",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T10:10:18.021473Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T10:10:17.943033Z",  
                    "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/accounts/AC5hUrduR2KTuijctdgP89ec/bank_accounts/BA5hU7CpB94FRvARZ1ZhfGbW",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5hU7CpB94FRvARZ1ZhfGbW" 
                },  
                "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/credits/CR5hYBuIOCVmiLH7sAwT9vaQ",  
                "transaction_number": "CR516-917-1986",  
                "amount": 431,  
                "meta": {},  
                "id": "CR5hYBuIOCVmiLH7sAwT9vaQ",  
                "available_at": "2012-10-30T17:10:18.006323Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5hN5G51d1zoL0iM8CILwhu/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:20.955614Z",  
            "uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5licMyoSxyiJwd1XAEwN9i",  
            "credits_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-30T10:10:21.054981Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:20.951347Z",  
            "uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/accounts/AC5licMyoSxyiJwd1XAEwN9i/bank_accounts/BA5lhTRhKMK5qFeGf2uCNkZm",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5lhTRhKMK5qFeGf2uCNkZm" 
        },  
        "uri": "/v1/marketplaces/TEST-MP5laQsT5JpcJ8DCiF2kUZEw/credits/CR5lnyCHDwaq56sPgYYiEqmE",  
        "transaction_number": "CR765-478-2761",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR5lnyCHDwaq56sPgYYiEqmE",  
        "available_at": "2012-10-30T17:10:21.023446Z" 
    } 
 

