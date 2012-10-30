Merchants
========

- `List all Merchants`_.
- `Retrieve a Merchant`_.
- `Update a Merchant`_.

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
    **object**. See `Marketplaces <./marketplaces.rst#marketplace-view>`_. 
 
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

List all Merchants
------------------

.. code:: 
 
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
                    "owner_account_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/accounts/AC1JLkGvXl4lvMGLx7MTlyvO",  
                    "support_email_address": "email.0@y.com",  
                    "uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/bank_accounts",  
                    "support_phone_number": "1234321234",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/debits",  
                    "holds_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/holds",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/transactions",  
                    "accounts_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/accounts",  
                    "id": "TEST-MP1JJmgk319CGVY2rF5JmOlC",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1JJmgk319CGVY2rF5JmOlC/cards" 
                },  
                "name": "Merchants, Inc.",  
                "email_address": "email.1@y.com",  
                "created_at": "2012-10-30T09:59:52.712952Z",  
                "uri": "/v1/merchants/TEST-MR1JKV3Lpa4CproquuIt7mhS",  
                "accounts_uri": "/v1/merchants/TEST-MR1JKV3Lpa4CproquuIt7mhS/accounts",  
                "meta": {},  
                "postal_code": "94110",  
                "country_code": "USA",  
                "balance": 0,  
                "type": "business",  
                "id": "TEST-MR1JKV3Lpa4CproquuIt7mhS",  
                "street_address": "Somewhere over the rainbow",  
                "api_keys_uri": "/v1/merchants/TEST-MR1JKV3Lpa4CproquuIt7mhS/api_keys" 
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
 

Retrieve a Merchant
-------------------

.. code:: 
 
    GET /v1/merchants/(merchant-id) 
 

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
            "owner_account_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/accounts/AC1LoYnCMnPCaYG2fImUwWWg",  
            "support_email_address": "email.0@y.com",  
            "uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/bank_accounts",  
            "support_phone_number": "1234321234",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/debits",  
            "holds_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/holds",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/transactions",  
            "accounts_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/accounts",  
            "id": "TEST-MP1Ln09e7uHIHfIBX1a1z9Qg",  
            "credits_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1Ln09e7uHIHfIBX1a1z9Qg/cards" 
        },  
        "name": "Merchants, Inc.",  
        "api_keys_uri": "/v1/merchants/TEST-MR1LoyC1N8fgzi3ICvGhxxpG/api_keys",  
        "created_at": "2012-10-30T09:59:54.170439Z",  
        "uri": "/v1/merchants/TEST-MR1LoyC1N8fgzi3ICvGhxxpG",  
        "accounts_uri": "/v1/merchants/TEST-MR1LoyC1N8fgzi3ICvGhxxpG/accounts",  
        "meta": {},  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "email.1@y.com",  
        "id": "TEST-MR1LoyC1N8fgzi3ICvGhxxpG",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

Update a Merchant
-----------------

.. code:: 
 
    PUT /v1/merchants/(merchant-id) 
 

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
        "api_keys_uri": "/v1/merchants/TEST-MR1Q5PjFH55Gm2eZgOwaX9Va/api_keys",  
        "created_at": "2012-10-30T09:59:58.345545Z",  
        "uri": "/v1/merchants/TEST-MR1Q5PjFH55Gm2eZgOwaX9Va",  
        "accounts_uri": "/v1/merchants/TEST-MR1Q5PjFH55Gm2eZgOwaX9Va/accounts",  
        "meta": { 
            "location": "121.121" 
        },  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "will@ie.com",  
        "id": "TEST-MR1Q5PjFH55Gm2eZgOwaX9Va",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

