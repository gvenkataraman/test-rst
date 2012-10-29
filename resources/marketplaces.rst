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
        "holds_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0",  
        "accounts_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:04:46.023194Z",  
            "uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC53Ur2wxYV4KblDFeoEUqFK",  
            "credits_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/accounts/AC53Ur2wxYV4KblDFeoEUqFK/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/bank_accounts",  
        "id": "TEST-MP53U0FoRgsOS0orTpkYvro0",  
        "credits_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP53U0FoRgsOS0orTpkYvro0/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy",  
        "accounts_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:04:47.369027Z",  
            "uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC55qit73ZiFWP5RBk93Voxu",  
            "credits_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/accounts/AC55qit73ZiFWP5RBk93Voxu/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/bank_accounts",  
        "id": "TEST-MP55q1XpYXQZ4VTAqiyHfzhy",  
        "credits_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP55q1XpYXQZ4VTAqiyHfzhy/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K",  
                "holds_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:04:48.486510Z",  
                    "uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC56Gahj5PvzPcW6BtQmJtLS",  
                    "credits_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts/AC56Gahj5PvzPcW6BtQmJtLS/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/accounts",  
                "id": "TEST-MP56E9hCHMoKnhhFqo4dKx7K",  
                "credits_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP56E9hCHMoKnhhFqo4dKx7K/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru",  
        "accounts_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:04:50.992570Z",  
            "uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC59uWQ8uxlieK7yo44llZ8U",  
            "credits_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/accounts/AC59uWQ8uxlieK7yo44llZ8U/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/bank_accounts",  
        "id": "TEST-MP59tE3yZR5hnRPAbTmTgbru",  
        "credits_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP59tE3yZR5hnRPAbTmTgbru/cards" 
    } 
 

