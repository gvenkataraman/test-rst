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
        "holds_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT",  
        "accounts_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T00:10:51.422413Z",  
            "uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC7iYKujOD9Qe5z3Q8rmJ7PR",  
            "credits_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/accounts/AC7iYKujOD9Qe5z3Q8rmJ7PR/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/bank_accounts",  
        "id": "TEST-MP7iYjFAl6G0Ik7spqzWR8mT",  
        "credits_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7iYjFAl6G0Ik7spqzWR8mT/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez",  
        "accounts_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T00:10:53.527085Z",  
            "uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC7llvxH0RXPnhJiwynfjIaL",  
            "credits_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/accounts/AC7llvxH0RXPnhJiwynfjIaL/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/bank_accounts",  
        "id": "TEST-MP7ll3cSahKiFpjoh0AUCrez",  
        "credits_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7ll3cSahKiFpjoh0AUCrez/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD",  
                "holds_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T00:10:55.787739Z",  
                    "uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC7nT7ujMfXZZe62ERlOoe4j",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts/AC7nT7ujMfXZZe62ERlOoe4j/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/accounts",  
                "id": "TEST-MP7nOJhH4zeJwBPUZXycAgyD",  
                "credits_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7nOJhH4zeJwBPUZXycAgyD/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH",  
        "accounts_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:11:01.191608Z",  
            "uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC7tXWecRCoH2PinIKk5HggH",  
            "credits_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/accounts/AC7tXWecRCoH2PinIKk5HggH/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/bank_accounts",  
        "id": "TEST-MP7tVnOcIG0bwq4bfCsgR3CH",  
        "credits_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7tVnOcIG0bwq4bfCsgR3CH/cards" 
    } 
 

