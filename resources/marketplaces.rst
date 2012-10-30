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
        "holds_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW",  
        "accounts_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T10:10:52.991020Z",  
            "uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC5Vk8zLm7wvw0dhf86jzipm",  
            "credits_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/accounts/AC5Vk8zLm7wvw0dhf86jzipm/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/bank_accounts",  
        "id": "TEST-MP5VjRRcy52hbqJdob4yH9NW",  
        "credits_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5VjRRcy52hbqJdob4yH9NW/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe",  
        "accounts_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-30T10:10:54.412765Z",  
            "uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC5WVh42aAsHNruWyjMuwbyY",  
            "credits_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/accounts/AC5WVh42aAsHNruWyjMuwbyY/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/bank_accounts",  
        "id": "TEST-MP5WUWIQoxSSVIfSOeuXLgxe",  
        "credits_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5WUWIQoxSSVIfSOeuXLgxe/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u",  
                "holds_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:55.769817Z",  
                    "uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC5YrSDyp3vTIABSNYNHUcAc",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts/AC5YrSDyp3vTIABSNYNHUcAc/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/accounts",  
                "id": "TEST-MP5Yqh4yHm32uZmmpsCqQa1u",  
                "credits_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5Yqh4yHm32uZmmpsCqQa1u/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q",  
        "accounts_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:58.652655Z",  
            "uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC61GSKS1sU1ni0gqidBEbWs",  
            "credits_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/accounts/AC61GSKS1sU1ni0gqidBEbWs/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/bank_accounts",  
        "id": "TEST-MP61EUxhdLsUuercxsYyzq3q",  
        "credits_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP61EUxhdLsUuercxsYyzq3q/cards" 
    } 
 

