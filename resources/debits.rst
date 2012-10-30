Debits
=======

- `Debit an Account`_
- `Retrieve a Debit`_
- `List All Debits`_
- `Update a Debit`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the debit. 
 
``amount`` 
    **integer**. The amount of the debit. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this debit. 
 
``description`` 
    **string**. Free-text description of the debit. 
 
``hold`` 
    **object**. The original hold for this debit, if this debit was to a card. 
    If the debit was to a bank account, this field will be null.  
 
``refunds_uri`` 
    **string**. URI for any partial or complete refunds of this debit. 
 
``appears_on_statement_as`` 
    **string**. The text that will appear on the buyer's statement. 
 
``account`` 
    **object**. The account to which this debit is associated. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    debit was created. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``available_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    transaction is guaranteed to clear. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``source`` 
    **object**. The funding source (card or bank account) for this debit.  
 

Debit an Account
----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts/(account-id)/debits 
    POST /v1/marketplaces/(marketplace-id)/holds/(hold-id)/debits 
    POST /v1/marketplaces/(marketplace-id)/debits 
 

Request
~~~~~~~

``amount`` 
    *optional* **integer** or **null**. If the resolving URI references a hold then this is hold amount. You can 
    always capture less than the hold amount (e.g. a partial capture). 
    Otherwise its the maximum per debit amount for your marketplace. Value must be >= the minimum per debit ``amount`` for *your* 
    marketplace. Value must be <= the maximum per debit ``amount`` for *your* 
    marketplace. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``description`` 
    *optional* **string** or **null**.  
 
``merchant_uri`` 
    *optional* **string** or **null**. URI referencing the merchant account on behalf of whom the 
    debit is being done. This is different from marketplace. 
    In a peer-to-peer transaction, there are three parties: 
 
    1. Marketplace 
    2. Seller/Service provider 
    3. Buyer 
 
    This merchant account represents 2. 
 
``hold_uri`` 
    *optional* **string** or **null**. If no ``hold`` is provided one my be generated and captured if the 
    source is a card. 
 
``source_uri`` 
    *optional* **string** or **null**.  
 
``bank_account_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "amount": 1234 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:12.352017Z",  
            "uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC10mBgjyEerQaREzKEq0Tw8",  
            "credits_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/debits/WD10vVLa5VJywP8dWgyh2ph2/refunds",  
        "created_at": "2012-10-30T09:59:12.497432Z",  
        "transaction_number": "W240-552-6751",  
        "uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/debits/WD10vVLa5VJywP8dWgyh2ph2",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:12.347633Z",  
            "uri": "/v1/marketplaces/TEST-MP10fexbpRzWS6xBXTcBiOoI/accounts/AC10mBgjyEerQaREzKEq0Tw8/bank_accounts/BA10mhO4JP8QIJtiG8Z4TDMw",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA10mhO4JP8QIJtiG8Z4TDMw" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD10vVLa5VJywP8dWgyh2ph2",  
        "available_at": "2012-10-30T16:59:12.485056Z" 
    } 
 

Retrieve a Debit
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/debits/(debit-id) 
    GET /v1/marketplaces/(marketplace-id)/holds/(hold-id)/debits/(debit-id) 
    GET /v1/marketplaces/(marketplace-id)/debits/(debit-id) 
 

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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:13.860114Z",  
            "uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC123M3OVsCnIITetZqvjwos",  
            "credits_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/debits/WD128sHqitug6VDgy1DCqxbC/refunds",  
        "created_at": "2012-10-30T09:59:13.937996Z",  
        "transaction_number": "W239-507-1736",  
        "uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/debits/WD128sHqitug6VDgy1DCqxbC",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:13.855915Z",  
            "uri": "/v1/marketplaces/TEST-MP11XSqPUEnTjbmJgyVKu5k8/accounts/AC123M3OVsCnIITetZqvjwos/bank_accounts/BA123s6dEhCdxfaMjr7wAvv6",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA123s6dEhCdxfaMjr7wAvv6" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD128sHqitug6VDgy1DCqxbC",  
        "available_at": "2012-10-30T16:59:13.928103Z" 
    } 
 

List All Debits
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/debits 
    GET /v1/marketplaces/(marketplace-id)/holds/(hold-id)/debits 
    GET /v1/marketplaces/(marketplace-id)/debits 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:15.556187Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC13Y2e3cLQywvZNGsBWyzfC",  
                    "credits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T09:59:15.570721Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/cards/CC22f66ca222b311e28dd780ee7316ae44",  
                    "id": "CC22f66ca222b311e28dd780ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-30T09:59:15.602711Z",  
                "transaction_number": "W926-458-8160",  
                "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD13ZVk08ZI5NRm2KtDq6Dwo",  
                "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD13ZVk08ZI5NRm2KtDq6Dwo/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-30T09:59:15.608738Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/holds/HL141ChNlwNUA5c6cni7D8a0",  
                    "expires_at": "2012-11-06T16:59:15.581628Z",  
                    "transaction_number": "HL442-391-7269",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC",  
                    "source_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13Y2e3cLQywvZNGsBWyzfC/cards/CC22f66ca222b311e28dd780ee7316ae44",  
                    "id": "HL141ChNlwNUA5c6cni7D8a0" 
                },  
                "id": "WD13ZVk08ZI5NRm2KtDq6Dwo",  
                "available_at": "2012-10-30T16:59:15.582431Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:15.554795Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC13XVRtBAAFFBcohnJj8kCM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T09:59:15.550822Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/bank_accounts/BA13XEx7tGFBxEfkOwldyhbS",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA13XEx7tGFBxEfkOwldyhbS" 
                },  
                "created_at": "2012-10-30T09:59:15.644166Z",  
                "transaction_number": "W284-217-6226",  
                "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD1439kFTdz6sszFUHCSA2RC",  
                "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD1439kFTdz6sszFUHCSA2RC/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD1439kFTdz6sszFUHCSA2RC",  
                "available_at": "2012-10-30T16:59:15.630049Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T09:59:15.554795Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC13XVRtBAAFFBcohnJj8kCM",  
                    "credits_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T09:59:15.550822Z",  
                    "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/accounts/AC13XVRtBAAFFBcohnJj8kCM/bank_accounts/BA13XEx7tGFBxEfkOwldyhbS",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA13XEx7tGFBxEfkOwldyhbS" 
                },  
                "created_at": "2012-10-30T09:59:15.644837Z",  
                "transaction_number": "W446-575-3490",  
                "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD143fJVGmsgCgGi2GoiXGbG",  
                "refunds_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits/WD143fJVGmsgCgGi2GoiXGbG/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD143fJVGmsgCgGi2GoiXGbG",  
                "available_at": "2012-10-30T16:59:15.631586Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP13R2SOOWn7Sb7FoWg2QEf2/debits?limit=10&offset=0" 
    } 
 

Update a Debit
--------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id)/debits 
    GET /v1/marketplaces/(marketplace-id)/holds/(hold-id)/debits 
    GET /v1/marketplaces/(marketplace-id)/debits 
 

Request
~~~~~~~

``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``description`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "meta": { 
            "my-id": "0987654321" 
        },  
        "description": "my new description" 
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
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T09:59:18.810560Z",  
            "uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC17CYrsl5YbnIrOV5SSuq5S",  
            "credits_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/debits/WD17HOluR86zzuS8nTaOvHik/refunds",  
        "created_at": "2012-10-30T09:59:18.894492Z",  
        "transaction_number": "W362-081-1302",  
        "uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/debits/WD17HOluR86zzuS8nTaOvHik",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T09:59:18.806105Z",  
            "uri": "/v1/marketplaces/TEST-MP17vu4phRj8xwyH4gZQNvI8/accounts/AC17CYrsl5YbnIrOV5SSuq5S/bank_accounts/BA17CEEjdmWcSUQ4aR7MiEV6",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA17CEEjdmWcSUQ4aR7MiEV6" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD17HOluR86zzuS8nTaOvHik",  
        "available_at": "2012-10-30T16:59:18.880504Z" 
    } 
 

