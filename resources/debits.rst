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
            "holds_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:26.010199Z",  
            "uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5qYFZqCvzfQ1uJGeOAeB6I",  
            "credits_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/cards" 
        },  
        "fee": 43,  
        "description": null,  
        "refunds_uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/debits/WD5r802oKAtRmc8LUzVquLC4/refunds",  
        "created_at": "2012-10-30T10:10:26.155068Z",  
        "transaction_number": "W371-712-9319",  
        "uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/debits/WD5r802oKAtRmc8LUzVquLC4",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:26.006009Z",  
            "uri": "/v1/marketplaces/TEST-MP5qRgH4CohzLLn6s2h3OEzG/accounts/AC5qYFZqCvzfQ1uJGeOAeB6I/bank_accounts/BA5qYnmVk9cK6cnDXCU5cVPm",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5qYnmVk9cK6cnDXCU5cVPm" 
        },  
        "amount": 1234,  
        "meta": {},  
        "appears_on_statement_as": "hiya.bom",  
        "hold": null,  
        "id": "WD5r802oKAtRmc8LUzVquLC4",  
        "available_at": "2012-10-30T17:10:26.143128Z" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:27.475461Z",  
            "uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5sCQQM2FOwKpFsm9CqK668",  
            "credits_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/cards" 
        },  
        "fee": 43,  
        "description": "abc123",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/debits/WD5sHK5dpLJpoSWzAlXax2YY/refunds",  
        "created_at": "2012-10-30T10:10:27.553839Z",  
        "transaction_number": "W458-222-9488",  
        "uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/debits/WD5sHK5dpLJpoSWzAlXax2YY",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:27.470927Z",  
            "uri": "/v1/marketplaces/TEST-MP5svqvhyhDmM4IxkrU7rzCI/accounts/AC5sCQQM2FOwKpFsm9CqK668/bank_accounts/BA5sCwWocfzuVBwrR5aNza2E",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5sCwWocfzuVBwrR5aNza2E" 
        },  
        "amount": 1254,  
        "meta": {},  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD5sHK5dpLJpoSWzAlXax2YY",  
        "available_at": "2012-10-30T17:10:27.545846Z" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/holds",  
                    "name": null,  
                    "roles": [ 
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:28.845170Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/transactions",  
                    "email_address": "email.8@y.com",  
                    "id": "AC5uanBz33MgGbEeZK81BSv2",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/cards" 
                },  
                "fee": 349999,  
                "description": null,  
                "source": { 
                    "expiration_month": 1,  
                    "hash": null,  
                    "last_four": "1111",  
                    "expiration_year": 2015,  
                    "created_at": "2012-10-30T10:10:28.857253Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/cards/CCb446049622b411e28ea080ee7316ae44",  
                    "id": "CCb446049622b411e28ea080ee7316ae44",  
                    "card_type": "visa",  
                    "is_valid": true,  
                    "meta": {},  
                    "country_code": "USA",  
                    "postal_code": "94110",  
                    "brand": "Visa",  
                    "street_address": "Somewhere over the rainbow",  
                    "name": "Jet Li" 
                },  
                "created_at": "2012-10-30T10:10:28.887261Z",  
                "transaction_number": "W615-866-7231",  
                "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ubXNjOM63d1fra00ABQTa",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ubXNjOM63d1fra00ABQTa/refunds",  
                "amount": 9999999,  
                "meta": {},  
                "appears_on_statement_as": "hiya.bom",  
                "hold": { 
                    "fee": 30,  
                    "description": null,  
                    "created_at": "2012-10-30T10:10:28.894153Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/holds/HL5udGFAKqc0sgYLq8wASylm",  
                    "expires_at": "2012-11-06T17:10:28.866525Z",  
                    "transaction_number": "HL325-959-9387",  
                    "amount": 9999999,  
                    "meta": {},  
                    "is_void": false,  
                    "account_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2",  
                    "source_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uanBz33MgGbEeZK81BSv2/cards/CCb446049622b411e28ea080ee7316ae44",  
                    "id": "HL5udGFAKqc0sgYLq8wASylm" 
                },  
                "id": "WD5ubXNjOM63d1fra00ABQTa",  
                "available_at": "2012-10-30T17:10:28.867199Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:28.844302Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5uajxRx2MXzdF4oj34QM28",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/cards" 
                },  
                "fee": 43,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T10:10:28.840979Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/bank_accounts/BA5ua4PWHegcU853dgC2wEQI",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5ua4PWHegcU853dgC2wEQI" 
                },  
                "created_at": "2012-10-30T10:10:28.933073Z",  
                "transaction_number": "W257-404-0020",  
                "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ufjevvDNddhu7WG1jh60A",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ufjevvDNddhu7WG1jh60A/refunds",  
                "amount": 1254,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD5ufjevvDNddhu7WG1jh60A",  
                "available_at": "2012-10-30T17:10:28.916831Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-30T10:10:28.844302Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC5uajxRx2MXzdF4oj34QM28",  
                    "credits_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/cards" 
                },  
                "fee": 15,  
                "description": "abc123",  
                "source": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-30T10:10:28.840979Z",  
                    "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/accounts/AC5uajxRx2MXzdF4oj34QM28/bank_accounts/BA5ua4PWHegcU853dgC2wEQI",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA5ua4PWHegcU853dgC2wEQI" 
                },  
                "created_at": "2012-10-30T10:10:28.933818Z",  
                "transaction_number": "W557-731-0944",  
                "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ufqUiKRKfNCY3uFntkiLa",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits/WD5ufqUiKRKfNCY3uFntkiLa/refunds",  
                "amount": 431,  
                "meta": {},  
                "appears_on_statement_as": "PND*TESTS",  
                "hold": null,  
                "id": "WD5ufqUiKRKfNCY3uFntkiLa",  
                "available_at": "2012-10-30T17:10:28.918479Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 3,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5u3KIkEBNtLvVYZTnN0IxC/debits?limit=10&offset=0" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:10:31.994894Z",  
            "uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5xI0tZzcUSspHSh0ZifHcE",  
            "credits_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/cards" 
        },  
        "fee": 43,  
        "description": "my new description",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/debits/WD5xNF49riGePvqXsLXfGvEo/refunds",  
        "created_at": "2012-10-30T10:10:32.091837Z",  
        "transaction_number": "W131-119-2335",  
        "uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/debits/WD5xNF49riGePvqXsLXfGvEo",  
        "source": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-30T10:10:31.990552Z",  
            "uri": "/v1/marketplaces/TEST-MP5xAEccAPJ1B2K7QKlVIhc8/accounts/AC5xI0tZzcUSspHSh0ZifHcE/bank_accounts/BA5xHH8sehUtBcAxbF1VwWd6",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA5xHH8sehUtBcAxbF1VwWd6" 
        },  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "appears_on_statement_as": "PND*TESTS",  
        "hold": null,  
        "id": "WD5xNF49riGePvqXsLXfGvEo",  
        "available_at": "2012-10-30T17:10:32.076772Z" 
    } 
 

