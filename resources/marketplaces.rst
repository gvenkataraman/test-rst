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
        "holds_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk",  
        "accounts_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T16:50:15.258808Z",  
            "uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC30zBFsoZveVJPfLBf6LZTS",  
            "credits_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/accounts/AC30zBFsoZveVJPfLBf6LZTS/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/bank_accounts",  
        "id": "TEST-MP30zgrAi807QBRBEkkFFKEk",  
        "credits_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP30zgrAi807QBRBEkkFFKEk/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/holds",  
        "name": "Seller of things",  
        "domain_url": "example.com",  
        "support_email_address": "support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs",  
        "accounts_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/holds",  
            "name": "Merchants, Inc.",  
            "roles": [ 
                "merchant" 
            ],  
            "created_at": "2012-10-29T16:50:16.755047Z",  
            "uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/transactions",  
            "email_address": "email.10@y.com",  
            "id": "AC32fXkY0xFHsyVminLZhbNi",  
            "credits_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/accounts/AC32fXkY0xFHsyVminLZhbNi/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/refunds",  
        "meta": { 
            "my-useful-data": "abc123" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/bank_accounts",  
        "id": "TEST-MP32fGEy9FGTn6ugdKEsLLKs",  
        "credits_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP32fGEy9FGTn6ugdKEsLLKs/cards" 
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
                "uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY",  
                "holds_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/holds",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/bank_accounts",  
                "owner_account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T16:50:18.116959Z",  
                    "uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/transactions",  
                    "email_address": "email.2@y.com",  
                    "id": "AC33MS4ekuWsTOYFhi5QHcs4",  
                    "credits_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts/AC33MS4ekuWsTOYFhi5QHcs4/cards" 
                },  
                "refunds_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/transactions",  
                "accounts_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/accounts",  
                "id": "TEST-MP33KQN7GHdjY5Oool4zuagY",  
                "credits_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP33KQN7GHdjY5Oool4zuagY/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/holds",  
        "name": "Seller of thingz",  
        "domain_url": "hiya.bom",  
        "support_email_address": "faster-support@example.com",  
        "uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU",  
        "accounts_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts",  
        "owner_account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:50:21.219524Z",  
            "uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/transactions",  
            "email_address": "email.2@y.com",  
            "id": "AC37hftV1iWhMCkaSF8dgj1G",  
            "credits_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/accounts/AC37hftV1iWhMCkaSF8dgj1G/cards" 
        },  
        "refunds_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/refunds",  
        "meta": { 
            "even-more-useful-data": "321cba" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/transactions",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/bank_accounts",  
        "id": "TEST-MP37fTL4pdBid4Yfrcl41pUU",  
        "credits_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP37fTL4pdBid4Yfrcl41pUU/cards" 
    } 
 

