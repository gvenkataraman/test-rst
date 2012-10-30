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
                    "owner_account_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/accounts/AC7yVYQFnuDv37lxuhTvonXd",  
                    "support_email_address": "email.0@y.com",  
                    "uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/bank_accounts",  
                    "support_phone_number": "1234321234",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/debits",  
                    "holds_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/holds",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/transactions",  
                    "accounts_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/accounts",  
                    "id": "TEST-MP7yRPgRK5JmaHb91UKDi5iP",  
                    "credits_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP7yRPgRK5JmaHb91UKDi5iP/cards" 
                },  
                "name": "Merchants, Inc.",  
                "email_address": "email.1@y.com",  
                "created_at": "2012-10-30T00:11:05.604455Z",  
                "uri": "/v1/merchants/TEST-MR7yVyb2XrjdzAm27rDzzWRd",  
                "accounts_uri": "/v1/merchants/TEST-MR7yVyb2XrjdzAm27rDzzWRd/accounts",  
                "meta": {},  
                "postal_code": "94110",  
                "country_code": "USA",  
                "balance": 0,  
                "type": "business",  
                "id": "TEST-MR7yVyb2XrjdzAm27rDzzWRd",  
                "street_address": "Somewhere over the rainbow",  
                "api_keys_uri": "/v1/merchants/TEST-MR7yVyb2XrjdzAm27rDzzWRd/api_keys" 
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
            "owner_account_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/accounts/AC7BHDLFfyr1bPOLwUQGqG5l",  
            "support_email_address": "email.0@y.com",  
            "uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/bank_accounts",  
            "support_phone_number": "1234321234",  
            "refunds_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/debits",  
            "holds_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/holds",  
            "transactions_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/transactions",  
            "accounts_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/accounts",  
            "id": "TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x",  
            "credits_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP7BEd7JVGsEuXSXWUQ5Ch1x/cards" 
        },  
        "name": "Merchants, Inc.",  
        "api_keys_uri": "/v1/merchants/TEST-MR7BGZLmVFJ3JYTzdisqmbYv/api_keys",  
        "created_at": "2012-10-30T00:11:08.064583Z",  
        "uri": "/v1/merchants/TEST-MR7BGZLmVFJ3JYTzdisqmbYv",  
        "accounts_uri": "/v1/merchants/TEST-MR7BGZLmVFJ3JYTzdisqmbYv/accounts",  
        "meta": {},  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "email.1@y.com",  
        "id": "TEST-MR7BGZLmVFJ3JYTzdisqmbYv",  
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
        "api_keys_uri": "/v1/merchants/TEST-MR7HwWCPlHrbvdasPK0mJKYb/api_keys",  
        "created_at": "2012-10-30T00:11:13.251869Z",  
        "uri": "/v1/merchants/TEST-MR7HwWCPlHrbvdasPK0mJKYb",  
        "accounts_uri": "/v1/merchants/TEST-MR7HwWCPlHrbvdasPK0mJKYb/accounts",  
        "meta": { 
            "location": "121.121" 
        },  
        "postal_code": "94110",  
        "country_code": "USA",  
        "type": "business",  
        "balance": 0,  
        "email_address": "will@ie.com",  
        "id": "TEST-MR7HwWCPlHrbvdasPK0mJKYb",  
        "street_address": "Somewhere over the rainbow" 
    } 
 

