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
        "holds_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS",  
        "accounts_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:11:49.683635Z",  
            "uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC4Xls4RsG7MSq0uDZ0L8pa4",  
            "credits_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/accounts/AC4Xls4RsG7MSq0uDZ0L8pa4/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/bank_accounts",  
        "id": "TEST-MP4Xl1SZMBkvhAymIlsN9GNS",  
        "credits_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4Xl1SZMBkvhAymIlsN9GNS/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG",  
        "accounts_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T15:11:51.268485Z",  
            "uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC4Z7YWIT7ZLEwL5Pn42dypS",  
            "credits_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/accounts/AC4Z7YWIT7ZLEwL5Pn42dypS/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/bank_accounts",  
        "id": "TEST-MP4Z7IgQh38OCQAeHjV4iOvG",  
        "credits_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4Z7IgQh38OCQAeHjV4iOvG/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8",  
                "holds_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T15:11:52.803188Z",  
                    "uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC50QYwVLaA6VTdH9eOm0wrq",  
                    "credits_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts/AC50QYwVLaA6VTdH9eOm0wrq/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/accounts",  
                "id": "TEST-MP50PqX52KwMO8JikdUhFOa8",  
                "credits_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP50PqX52KwMO8JikdUhFOa8/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG",  
        "accounts_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:11:56.206748Z",  
            "uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC54GhLBLpGZegDLU1V4feSg",  
            "credits_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/accounts/AC54GhLBLpGZegDLU1V4feSg/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/bank_accounts",  
        "id": "TEST-MP54EiPw9WJQhBkHB2BI43pG",  
        "credits_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP54EiPw9WJQhBkHB2BI43pG/cards" 
    } 
 

