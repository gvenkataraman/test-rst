Marketplaces
============

- `Create a Marketplace`_
- `Retrieve a Hold`_
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
        "holds_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T14:56:22.114317Z",  
            "uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC3IdsRxmPEOIdMJ7WmLavc0",  
            "credits_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/accounts/AC3IdsRxmPEOIdMJ7WmLavc0/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/bank_accounts",  
        "id": "TEST-MP3Id9Hg2yjo8marSLV6S180",  
        "credits_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3Id9Hg2yjo8marSLV6S180/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T14:56:23.644511Z",  
            "uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC3JWbfa4sF0fseeUuXuVJm4",  
            "credits_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/accounts/AC3JWbfa4sF0fseeUuXuVJm4/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/bank_accounts",  
        "id": "TEST-MP3JVUxWmoZpzkoMpZS8xi6g",  
        "credits_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3JVUxWmoZpzkoMpZS8xi6g/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta",  
                "holds_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T14:56:24.915681Z",  
                    "uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC3LmLCBwNBRqZCjxorgR1w8",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts/AC3LmLCBwNBRqZCjxorgR1w8/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/accounts",  
                "id": "TEST-MP3LkN6MC9REtt93wPZfF8Ta",  
                "credits_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3LkN6MC9REtt93wPZfF8Ta/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu",  
        "accounts_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T14:56:27.740325Z",  
            "uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC3OxJPUL22SNzyyXfen6HZi",  
            "credits_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/accounts/AC3OxJPUL22SNzyyXfen6HZi/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/bank_accounts",  
        "id": "TEST-MP3OvKAwz2wVESOODmKVD3vu",  
        "credits_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3OvKAwz2wVESOODmKVD3vu/cards" 
    } 
 

