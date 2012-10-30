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
    **object**. The account owning this marketplace. See `Accounts <./accounts.rst>`_. 
 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S",  
        "accounts_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T09:59:43.475226Z",  
            "uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC1zmU1KSHjYq7LZWkO3oYle",  
            "credits_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/accounts/AC1zmU1KSHjYq7LZWkO3oYle/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/bank_accounts",  
        "id": "TEST-MP1zmt63iSc17eVge5fnQ93S",  
        "credits_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1zmt63iSc17eVge5fnQ93S/cards" 
    } 
 

Retrieve a Marketplace
----------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id) 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8",  
        "accounts_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T09:59:45.047260Z",  
            "uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC1B8wSbvpg5lQHtORyZDguE",  
            "credits_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/accounts/AC1B8wSbvpg5lQHtORyZDguE/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/bank_accounts",  
        "id": "TEST-MP1B86WFBuPp7geHHVj2Hho8",  
        "credits_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1B86WFBuPp7geHHVj2Hho8/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY",  
                "holds_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:46.474854Z",  
                    "uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC1CK2rAJ5WoOOxqzhaPIr6k",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts/AC1CK2rAJ5WoOOxqzhaPIr6k/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/accounts",  
                "id": "TEST-MP1CI2Kk7TPWvEb97dUntrmY",  
                "credits_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1CI2Kk7TPWvEb97dUntrmY/cards" 
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
 
    PUT /v1/marketplaces/(marketplace-id) 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi",  
        "accounts_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:49.701174Z",  
            "uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC1Gn0WLw4xtQWmlXu6rmibi",  
            "credits_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/accounts/AC1Gn0WLw4xtQWmlXu6rmibi/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/bank_accounts",  
        "id": "TEST-MP1Gl0iNi73On2jG2TnTkSbi",  
        "credits_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1Gl0iNi73On2jG2TnTkSbi/cards" 
    } 
 

