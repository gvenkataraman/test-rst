Mechants
========

- `List all Mechants`_.
- `Retrieve a Mechant`_.
- `Update a Mechant`_.

Fields
------

``id`` 
    **string**. The resource identifier.  
 
``uri`` 
    **string**. The URI of this merchant.  
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    merchant was underwritten. 
 
``type`` 
    **string**. Merchant type. It will be one of: ``person`` or ``business`` 
 
``name`` 
    **string**. The name of the business, for a business-type merchant. 
    The name of the person, for a person-type merchant. 
 
``email_address`` 
    **string**. Email address of the business, for a business-type merchant. 
    Email address of the person, for a person-type merchant. 
 
``phone_number`` 
    **string**. The merchant's phone number. 
 
``balance`` 
    **integer**. Merchant's account balance. 
 
``marketplace`` 
    **object**.  
``accounts_uri`` 
    **string**. Accounts belonging to this merchant. 
 
``api_keys_uri`` 
    **string**. URI for this merchant's API keys. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``street_address`` 
    **string**.  
``city`` 
    **string**.  
``postal_code`` 
    **string**.  
``country_code`` 
    **string**.  

List all Mechants
-----------------

.. code:: 
 
    HEAD /v1/merchants 
    GET /v1/merchants 
 

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
        "first_uri": "/v1/merchants?limit=10&offset=0",  
        "items": [ 
            { 
                "phone_number": "+19046281796",  
                "city": "San Francisco",  
                "marketplace": { 
                    "in_escrow": 9999999,  
                    "domain_url": "hiya.bom",  
                    "name": "Some",  
                    "owner_account_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/accounts/AC2N8NlU1yCYntOAuzMyuVLe",  
                    "support_email_address": "email.0@y.com",  
                    "uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/bank_accounts",  
                    "support_phone_number": "1234321234",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/debits",  
                    "holds_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/holds",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/transactions",  
                    "accounts_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/accounts",  
                    "id": "TEST-MP2N7hWCc1nsy74GPd2wEOtS",  
                    "credits_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP2N7hWCc1nsy74GPd2wEOtS/cards" 
                },  
                "name": "Merchants, Inc.",  
                "email_address": "email.1@y.com",  
                "created_at": "2012-10-29T16:50:03.313064Z",  
                "uri": "/v1/merchants/TEST-MR2N8vFiuLWTdIZwODmjmFxy",  
                "accounts_uri": "/v1/merchants/TEST-MR2N8vFiuLWTdIZwODmjmFxy/accounts",  
                "meta": {},  
                "postal_code": "94110",  
                "country_code": "USA",  
                "balance": 0,  
                "type": "business",  
                "id": "TEST-MR2N8vFiuLWTdIZwODmjmFxy",  
                "street_address": "Somewhere over the rainbow",  
                "api_keys_uri": "/v1/merchants/TEST-MR2N8vFiuLWTdIZwODmjmFxy/api_keys" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/merchants?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 1,  
        "next_uri": null,  
        "last_uri": "/v1/merchants?limit=10&offset=0" 
    } 
 

Retrieve a Mechant
------------------

.. code:: 
 
    GET /v1/merchants/(merchant:merchant) 
 

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
        "phone_number": "+19046281796",  
        "city": "San Francisco",  
        "marketplace": { 
            "in_escrow": 9999999,  
            "domain_url": "hiya.bom",  
            "name": "Some",  
            "owner_account_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/accounts/AC2OUNr7lKABAGIfOs6M5wvG",  
            "support_email_address": "email.0@y.com",  
            "uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/bank_accounts",  
            "support_phone_number": "1234321234",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/debits",  
            "holds_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/holds",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/transactions",  
            "accounts_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/accounts",  
            "id": "TEST-MP2OTfe8duhO176g14TYzc3i",  
            "credits_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2OTfe8duhO176g14TYzc3i/cards" 
        },  
        "name": "Merchants, Inc.",  
        "api_keys_uri": "/v1/merchants/TEST-MR2OUoUs6cGzecGwLw5cZDZG/api_keys",  
        "created_at": "2012-10-29T16:50:04.890011Z",  
        "uri": "/v1/merchants/TEST-MR2OUoUs6cGzecGwLw5cZDZG",  
        "accounts_uri": "/v1/merchants/TEST-MR2OUoUs6cGzecGwLw5cZDZG/accounts",  
        "meta": {},  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "email.1@y.com",  
        "id": "TEST-MR2OUoUs6cGzecGwLw5cZDZG",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

Update a Mechant
----------------

.. code:: 
 
    PUT /v1/merchants/(merchant:merchant) 
 

Request
~~~~~~~
   
``name`` 
    *optional* **string** or **null**. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string** or **null**. RFC-2822 formatted email address. 
 
``phone_number`` 
    *optional* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``bank_account`` 
    *optional* **object** or **null**.  
        ``name`` 
            *required* **string** or **null**. Name on the bank account. Length must be **>=** ``2``. 
 
        ``account_number`` 
            *required* **string** or **null**. Bank account number. Length must be **>=** ``1``. 
 
        ``bank_code`` 
            #. If not a *production* bank account then `bank_code` is a: 
 
               ``bank_code`` 
                   *required* **string** or **null**. Length must be **>=** ``1``. 
 
 
        ``account_type`` 
            *optional* **string** or **null**. Bank account type. It should be one of: ``checking``, ``savings`` 
 
        ``meta`` 
            *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "phone_number": "+16501112222",  
        "meta": { 
            "location": "121.121" 
        },  
        "email_address": "will@ie.com",  
        "name": "Willie",  
        "bank_account": { 
            "account_type": "savings",  
            "account_number": "345345345",  
            "name": "Willie",  
            "bank_code": "325182797" 
        } 
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
        "phone_number": "+16501112222",  
        "city": "San Francisco",  
        "marketplace": null,  
        "name": "Willie",  
        "api_keys_uri": "/v1/merchants/TEST-MR2TPaTwXn77A66A1FyOKRCc/api_keys",  
        "created_at": "2012-10-29T16:50:09.258789Z",  
        "uri": "/v1/merchants/TEST-MR2TPaTwXn77A66A1FyOKRCc",  
        "accounts_uri": "/v1/merchants/TEST-MR2TPaTwXn77A66A1FyOKRCc/accounts",  
        "meta": { 
            "location": "121.121" 
        },  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "will@ie.com",  
        "id": "TEST-MR2TPaTwXn77A66A1FyOKRCc",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

