Marketplaces
============

- `Create a Marketplace`_
- `Retrieve a Marketplace`_
- `List my Marketplaces`_
- `Update a Marketplace`_

Fields
------

``id`` 
    **string**. The resource identifier.  
 
``uri`` 
    **string**. The URI of this marketplace  
 
``name`` 
    **string**. Name of this marketplace. 
 
``support_email_address`` 
    **string**. Email address on file for support for this marketplace. 
 
``support_phone_number`` 
    **string**. Phone number on file for support for this marketplace. 
 
``domain_url`` 
    **string**.  
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``in_escrow`` 
    **integer**. Amount (in cents) in the escrow account for this marketplace. 
 
``owner_account`` 
    **object**. The account owning this marketplace.  
 
``debits_uri`` 
    **string**. URI for all debits for this marketplace. 
 
``credits_uri`` 
    **string**. URI for all credits for this marketplace. 
 
``refunds_uri`` 
    **string**. URI for all refunds for this marketplace. 
 
``holds_uri`` 
    **string**. URI for all holds for this marketplace. 
 
``accounts_uri`` 
    **string**. URI for all accounts on this marketplace. 
 
``transactions_uri`` 
    **string**. URI for all transactions for this marketplace. 
 
``bank_accounts_uri`` 
    **string**. A URI for a Balanced entity 
 
``cards_uri`` 
    **string**. A URI for a Balanced entity 
 

Create a Marketplace
--------------------

.. code:: 
 
    POST /v1/marketplaces 
 

Request
~~~~~~~

``support_email_address`` 
    *optional* **string** or **null**. RFC-2822 formatted email address. 
 
``name`` 
    *optional* **string** or **null**. Length must be **<=** ``128``. 
 
``domain_url`` 
    *optional* **string** or **null**.  
 
``support_phone_number`` 
    *optional* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``owner_account`` 
    *optional* **object** or **null**.  
        ``name`` 
            *optional* **string** or **null**. Length must be **<=** ``128``. 
 
        ``email_address`` 
            *optional* **string** or **null**. RFC-2822 formatted email address. 
 
    Defaults to: 
 
    .. code:: javascript 
 
        { 
            "email_address": null, 
            "name": null 
        } 
 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "support_phone_number": "+12125551212",  
        "domain_url": "example.com",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "support_email_address": "support@example.com",  
        "name": "Seller of things" 
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
        "in_escrow": 0,  
        "support_phone_number": "+12125551212",  
        "holds_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0",  
        "accounts_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:57:27.773162Z",  
            "uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC5u1Ti0Wt32FszynQFnJXK",  
            "credits_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/accounts/AC5u1Ti0Wt32FszynQFnJXK/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/bank_accounts",  
        "id": "TEST-MP5tKmBoODivOtYmaZKc3k0",  
        "credits_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5tKmBoODivOtYmaZKc3k0/cards" 
    } 
 

Retrieve a Marketplace
----------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace) 
 

Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 201 CREATED 
 
Body 
~~~~ 
 
.. code:: javascript 
 
    { 
        "in_escrow": 0,  
        "support_phone_number": "+12125551212",  
        "holds_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0",  
        "accounts_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:57:29.611480Z",  
            "uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC7ydJTn6Bi79hRIZDDzHso",  
            "credits_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/accounts/AC7ydJTn6Bi79hRIZDDzHso/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/bank_accounts",  
        "id": "TEST-MP7xQrm04GMpcsmQsjiukK0",  
        "credits_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7xQrm04GMpcsmQsjiukK0/cards" 
    } 
 

List my Marketplaces
--------------------

.. code:: 
 
    GET /v1/marketplaces 
 

Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
~~~~ 
 
.. code:: javascript 
 
    { 
        "first_uri": "/v1/marketplaces?limit=10&offset=0",  
        "items": [ 
            { 
                "in_escrow": 9999999,  
                "support_phone_number": "1234321234",  
                "domain_url": "hiya.bom",  
                "name": "Some",  
                "support_email_address": "email.0@y.com",  
                "uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo",  
                "holds_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:57:30.982183Z",  
                    "uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC95Kp3naJxUjJ6XtOWaPM8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts/AC95Kp3naJxUjJ6XtOWaPM8/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/accounts",  
                "id": "TEST-MP93LNBsd9QO7vk1PC3LOGo",  
                "credits_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP93LNBsd9QO7vk1PC3LOGo/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 1,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces?limit=10&offset=0" 
    } 
 

Update a Marketplace
--------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace) 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. Length must be **<=** ``128``. 
 
``support_email_address`` 
    *optional* **string** or **null**. RFC-2822 formatted email address. 
 
``support_phone_number`` 
    *optional* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
``domain_url`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "support_phone_number": "+18185551212",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "support_email_address": "faster-support@example.com",  
        "name": "Seller of thingz" 
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
        "in_escrow": 9999999,  
        "support_phone_number": "+18185551212",  
        "holds_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI",  
        "accounts_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:57:34.686082Z",  
            "uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/transactions",  
            "email_address": "email.2@y.com",  
            "id": "ACdg1jb81vH7UNna61pG3U8",  
            "credits_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/accounts/ACdg1jb81vH7UNna61pG3U8/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/bank_accounts",  
        "id": "TEST-MPde4s1p7wSkXuh5F7eMkYI",  
        "credits_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPde4s1p7wSkXuh5F7eMkYI/cards" 
    } 
 

