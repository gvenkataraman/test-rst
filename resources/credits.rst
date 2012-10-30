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
            "holds_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:09:59.459134Z",  
            "uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6mxcz9cd7LXRTBom8eF4NZ",  
            "credits_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-30T00:09:59.589697Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:09:59.454733Z",  
            "uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/accounts/AC6mxcz9cd7LXRTBom8eF4NZ/bank_accounts/BA6mwSPKK1YMTw7xgbd2C4BJ",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6mwSPKK1YMTw7xgbd2C4BJ" 
        },  
        "uri": "/v1/marketplaces/TEST-MP6mqnqwlnade47U1ykH3akH/credits/CR6mFA9eCHOeVglO4cvDLFv5",  
        "transaction_number": "CR653-560-2087",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR6mFA9eCHOeVglO4cvDLFv5",  
        "available_at": "2012-10-30T07:09:59.578507Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:01.284343Z",  
            "uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6oAtvDpOoQYIB4K1dz6YvN",  
            "credits_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-30T00:10:01.375777Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:10:01.279900Z",  
            "uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/accounts/AC6oAtvDpOoQYIB4K1dz6YvN/bank_accounts/BA6oAa23v0uCcPy7tXBPw1qz",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6oAa23v0uCcPy7tXBPw1qz" 
        },  
        "uri": "/v1/marketplaces/TEST-MP6otLLnyrM1lsNtdlx3kbg7/credits/CR6oG4WnP5tLDzQixgF9U38n",  
        "transaction_number": "CR500-002-0115",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR6oG4WnP5tLDzQixgF9U38n",  
        "available_at": "2012-10-30T07:10:01.357179Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:03.021121Z",  
                    "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6qxzSUemdTc3SAb3pvGyB5",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T00:10:03.120499Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T00:10:03.017032Z",  
                    "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/bank_accounts/BA6qxiBuUOv1TTmQUnTumeVJ",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA6qxiBuUOv1TTmQUnTumeVJ" 
                },  
                "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/credits/CR6qDmif1xELICFOrXkowteH",  
                "transaction_number": "CR515-297-7061",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR6qDmif1xELICFOrXkowteH",  
                "available_at": "2012-10-30T07:10:03.094246Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:03.021121Z",  
                    "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC6qxzSUemdTc3SAb3pvGyB5",  
                    "credits_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-30T00:10:03.121236Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T00:10:03.017032Z",  
                    "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/accounts/AC6qxzSUemdTc3SAb3pvGyB5/bank_accounts/BA6qxiBuUOv1TTmQUnTumeVJ",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA6qxiBuUOv1TTmQUnTumeVJ" 
                },  
                "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/credits/CR6qDu3oEGSmUKM9rKs8utnJ",  
                "transaction_number": "CR537-372-0027",  
                "amount": 431,  
                "meta": {},  
                "id": "CR6qDu3oEGSmUKM9rKs8utnJ",  
                "available_at": "2012-10-30T07:10:03.104787Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP6qqi1BpFUdxf2fvSRO37YT/credits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:10:07.336123Z",  
            "uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6voua2Zy5m6CJx4AbFa0mf",  
            "credits_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-30T00:10:07.443046Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T00:10:07.331543Z",  
            "uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/accounts/AC6voua2Zy5m6CJx4AbFa0mf/bank_accounts/BA6vo9sBOCKwd5Ct7pRYQSxJ",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA6vo9sBOCKwd5Ct7pRYQSxJ" 
        },  
        "uri": "/v1/marketplaces/TEST-MP6vgk1BzbqGUFC9D3DQ0iun/credits/CR6vunGB8QNzMP78X2XIThKP",  
        "transaction_number": "CR559-667-5057",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR6vunGB8QNzMP78X2XIThKP",  
        "available_at": "2012-10-30T07:10:07.410040Z" 
    } 
 

