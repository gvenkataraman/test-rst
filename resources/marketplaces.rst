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
        "holds_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T16:00:41.376746Z",  
            "uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC3Bez05DrRZBczvEoafAO7W",  
            "credits_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/accounts/AC3Bez05DrRZBczvEoafAO7W/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/bank_accounts",  
        "id": "TEST-MP3BecfRx84fN4vreZlCmWkQ",  
        "credits_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3BecfRx84fN4vreZlCmWkQ/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T16:00:42.973992Z",  
            "uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC3D1Wrd35yrn8D3FJB8vdL6",  
            "credits_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/accounts/AC3D1Wrd35yrn8D3FJB8vdL6/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/bank_accounts",  
        "id": "TEST-MP3D1EIbWJO0rnCUKbhnHTUw",  
        "credits_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3D1EIbWJO0rnCUKbhnHTUw/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4",  
                "holds_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:00:44.269522Z",  
                    "uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC3EuekKYFHTeDjXMy5aMAUA",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts/AC3EuekKYFHTeDjXMy5aMAUA/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/accounts",  
                "id": "TEST-MP3EsfeKsxUpF4aqZPcuEPS4",  
                "credits_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3EsfeKsxUpF4aqZPcuEPS4/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:00:47.451686Z",  
            "uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC3I48c81XeK97p6SAk3PjVi",  
            "credits_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/accounts/AC3I48c81XeK97p6SAk3PjVi/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/bank_accounts",  
        "id": "TEST-MP3I29eXWU1T4TzyGr3AsMbq",  
        "credits_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3I29eXWU1T4TzyGr3AsMbq/cards" 
    } 
 

