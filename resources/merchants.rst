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
                    "owner_account_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/accounts/AC3oreHzuOXooXtHzvhbanCQ",  
                    "support_email_address": "email.0@y.com",  
                    "uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/bank_accounts",  
                    "support_phone_number": "1234321234",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/debits",  
                    "holds_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/holds",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/transactions",  
                    "accounts_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/accounts",  
                    "id": "TEST-MP3opSCttQRnNCfLUXrSnhJi",  
                    "credits_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP3opSCttQRnNCfLUXrSnhJi/cards" 
                },  
                "name": "Merchants, Inc.",  
                "email_address": "email.1@y.com",  
                "created_at": "2012-10-29T16:00:29.997105Z",  
                "uri": "/v1/merchants/TEST-MR3oqVLen8UdpkFGTqe2fzbC",  
                "accounts_uri": "/v1/merchants/TEST-MR3oqVLen8UdpkFGTqe2fzbC/accounts",  
                "meta": {},  
                "postal_code": "94110",  
                "country_code": "USA",  
                "balance": 0,  
                "type": "business",  
                "id": "TEST-MR3oqVLen8UdpkFGTqe2fzbC",  
                "street_address": "Somewhere over the rainbow",  
                "api_keys_uri": "/v1/merchants/TEST-MR3oqVLen8UdpkFGTqe2fzbC/api_keys" 
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
            "owner_account_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/accounts/AC3qabKqQiR3imbSfbM3O8OE",  
            "support_email_address": "email.0@y.com",  
            "uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/bank_accounts",  
            "support_phone_number": "1234321234",  
            "refunds_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/debits",  
            "holds_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/holds",  
            "transactions_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/transactions",  
            "accounts_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/accounts",  
            "id": "TEST-MP3q8cIaZIWz9eS24wJhP8KE",  
            "credits_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP3q8cIaZIWz9eS24wJhP8KE/cards" 
        },  
        "name": "Merchants, Inc.",  
        "api_keys_uri": "/v1/merchants/TEST-MR3q9M6BOxBC4sn3joKwoAjq/api_keys",  
        "created_at": "2012-10-29T16:00:31.530311Z",  
        "uri": "/v1/merchants/TEST-MR3q9M6BOxBC4sn3joKwoAjq",  
        "accounts_uri": "/v1/merchants/TEST-MR3q9M6BOxBC4sn3joKwoAjq/accounts",  
        "meta": {},  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "email.1@y.com",  
        "id": "TEST-MR3q9M6BOxBC4sn3joKwoAjq",  
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
        "api_keys_uri": "/v1/merchants/TEST-MR3uTHSMX9QAM6kckCTJnz48/api_keys",  
        "created_at": "2012-10-29T16:00:35.743594Z",  
        "uri": "/v1/merchants/TEST-MR3uTHSMX9QAM6kckCTJnz48",  
        "accounts_uri": "/v1/merchants/TEST-MR3uTHSMX9QAM6kckCTJnz48/accounts",  
        "meta": { 
            "location": "121.121" 
        },  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "will@ie.com",  
        "id": "TEST-MR3uTHSMX9QAM6kckCTJnz48",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

