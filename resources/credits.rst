Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_
- `Update a Credit`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``amount`` 
    **integer**. Amount of the credit. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit was created. 
 
``description`` 
    **string**. A description of the credit, used for display purposes. 
 
``account`` 
    **object**. The account to which the credit is associated. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``available_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit will be available to the merchant. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this credit. 
 
``destination`` 
    **object**. The funding destination for this credit (i.e., a bank account).  
 
``state`` 
    **string**. One of ``pending``, ``cleared``, ``rejected``.  
 

Credit an Account
-----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    POST /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``amount`` 
    *required* **integer** or **null**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as`` 
    *optional* **string** or **null**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``destination_uri`` 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:17:11.227806Z",  
            "uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1RxBYjVDCFtF2b3EEKnSnO",  
            "credits_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/cards" 
        },  
        "fee": 25,  
        "description": null,  
        "state": "cleared",  
        "created_at": "2012-10-29T12:17:11.345171Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:17:11.223809Z",  
            "uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/accounts/AC1RxBYjVDCFtF2b3EEKnSnO/bank_accounts/BA1Rxkj3uPLdYlRIKaaTJjvK",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1Rxkj3uPLdYlRIKaaTJjvK" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1RrvtlhohMQWASruMvWKLa/credits/CR1RF3nKLuo5WKcKiJvGs00A",  
        "transaction_number": "CR966-750-8014",  
        "amount": 1234,  
        "meta": {},  
        "id": "CR1RF3nKLuo5WKcKiJvGs00A",  
        "available_at": "2012-10-29T19:17:11.333733Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    GET /v1/marketplaces/(marketplace:marketplace)/credits/(credit:credit) 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:17:12.747202Z",  
            "uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1Tfz3aWCYA80xsRcju3lNG",  
            "credits_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/cards" 
        },  
        "fee": 25,  
        "description": "hiya",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:17:12.811649Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:17:12.743223Z",  
            "uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/accounts/AC1Tfz3aWCYA80xsRcju3lNG/bank_accounts/BA1Tfhn6EDqm21YE7PRNvLIE",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1Tfhn6EDqm21YE7PRNvLIE" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1Ta3InJYe1qVYbb2telrtW/credits/CR1TjznBUARVkpy3NYkEqKk4",  
        "transaction_number": "CR963-755-5799",  
        "amount": 1254,  
        "meta": {},  
        "id": "CR1TjznBUARVkpy3NYkEqKk4",  
        "available_at": "2012-10-29T19:17:12.799226Z" 
    } 
 

List All Credits
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/credits?limit=10&offset=0",  
        "items": [ 
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:17:14.115079Z",  
                    "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1UMWELwGSRAcJy8A5JWmPO",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:17:14.176679Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:17:14.110567Z",  
                    "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/bank_accounts/BA1UMCqOtlw62u1K9kuKaCGM",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1UMCqOtlw62u1K9kuKaCGM" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/credits/CR1UQlIAbyFC7CJeOomeuony",  
                "transaction_number": "CR374-818-3866",  
                "amount": 1254,  
                "meta": {},  
                "id": "CR1UQlIAbyFC7CJeOomeuony",  
                "available_at": "2012-10-29T19:17:14.156206Z" 
            },  
            { 
                "account": { 
                    "holds_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/holds",  
                    "name": null,  
                    "roles": [ 
                        "merchant",  
                        "buyer" 
                    ],  
                    "created_at": "2012-10-29T12:17:14.115079Z",  
                    "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO",  
                    "bank_accounts_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/bank_accounts",  
                    "refunds_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/refunds",  
                    "meta": {},  
                    "debits_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/debits",  
                    "transactions_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/transactions",  
                    "email_address": "email.7@y.com",  
                    "id": "AC1UMWELwGSRAcJy8A5JWmPO",  
                    "credits_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/credits",  
                    "cards_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/cards" 
                },  
                "fee": 25,  
                "description": "hiya",  
                "state": "cleared",  
                "created_at": "2012-10-29T12:17:14.177245Z",  
                "destination": { 
                    "bank_name": null,  
                    "name": "Fit Finlay",  
                    "bank_code": "325182797",  
                    "created_at": "2012-10-29T12:17:14.110567Z",  
                    "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/accounts/AC1UMWELwGSRAcJy8A5JWmPO/bank_accounts/BA1UMCqOtlw62u1K9kuKaCGM",  
                    "is_valid": true,  
                    "meta": {},  
                    "last_four": "1234",  
                    "id": "BA1UMCqOtlw62u1K9kuKaCGM" 
                },  
                "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/credits/CR1UQrnsQa6fvBb0db8oHeDO",  
                "transaction_number": "CR790-110-3177",  
                "amount": 431,  
                "meta": {},  
                "id": "CR1UQrnsQa6fvBb0db8oHeDO",  
                "available_at": "2012-10-29T19:17:14.164262Z" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/credits?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 2,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1UFqCfqwLDYMhTVLH24hxy/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description`` 
    *optional* **string** or **null**.  
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

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
            "holds_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T12:17:17.341848Z",  
            "uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1YpXESgF6heobFKCRkrKu0",  
            "credits_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/cards" 
        },  
        "fee": 25,  
        "description": "my new description",  
        "state": "cleared",  
        "created_at": "2012-10-29T12:17:17.408850Z",  
        "destination": { 
            "bank_name": null,  
            "name": "Fit Finlay",  
            "bank_code": "325182797",  
            "created_at": "2012-10-29T12:17:17.338148Z",  
            "uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/accounts/AC1YpXESgF6heobFKCRkrKu0/bank_accounts/BA1YpHkYr4rpHCKHmmLeMSig",  
            "is_valid": true,  
            "meta": {},  
            "last_four": "1234",  
            "id": "BA1YpHkYr4rpHCKHmmLeMSig" 
        },  
        "uri": "/v1/marketplaces/TEST-MP1YiWqeDiSqezWKy1BfaYW8/credits/CR1YtIVpCkgMgMSmMzoAfa6w",  
        "transaction_number": "CR920-338-2273",  
        "amount": 1254,  
        "meta": { 
            "my-id": "0987654321" 
        },  
        "id": "CR1YtIVpCkgMgMSmMzoAfa6w",  
        "available_at": "2012-10-29T19:17:17.390261Z" 
    } 
 

