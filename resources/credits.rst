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
    *required* **integer**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description`` 
    *optional* **string**.  
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as`` 
    *optional* **string**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``account_uri`` 
    *optional* **string**.  
 
Exactly one of 
    ``destination_uri`` 
        *required* **string**.  
 
    ``bank_account_uri`` 
        *required* **string**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MP3hX8SlvoNWMuhhlQkcJTta/accounts/AC3i2Gli1nhXZWpYW2qZhl9W" 
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
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:21:23.802914Z", 
        "updated_at": "2012-10-28T14:21:23.802916Z", 
        "uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3junLgYmqDhaVDp90VSzFG", 
        "credits_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:21:23.901032Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:21:23.799902Z", 
        "updated_at": "2012-10-28T14:21:23.799904Z", 
        "uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/accounts/AC3junLgYmqDhaVDp90VSzFG/bank_accounts/BA3juaU5c711EFpcqhBi9Ukk", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3juaU5c711EFpcqhBi9Ukk" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3joo1ghlC4MicIbsXIMC1e/credits/CR3jALvfmAq1q3HA2mvFYXkM", 
      "updated_at": "2012-10-28T14:21:23.901034Z", 
      "transaction_number": "CR097-694-2990", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR3jALvfmAq1q3HA2mvFYXkM", 
      "available_at": "2012-10-28T21:21:23.893749Z" 
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
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:21:25.079217Z", 
        "updated_at": "2012-10-28T14:21:25.079220Z", 
        "uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3kVnu2J7KU5dwqbw9gLeh6", 
        "credits_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:21:25.132443Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:21:25.075650Z", 
        "updated_at": "2012-10-28T14:21:25.075652Z", 
        "uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/accounts/AC3kVnu2J7KU5dwqbw9gLeh6/bank_accounts/BA3kV88ZtsYFYiOO27pvfuUA", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3kV88ZtsYFYiOO27pvfuUA" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3kQ5KxORjyfB0iK7IDEric/credits/CR3kYB8JGRpPeU0aBX5QYLTS", 
      "updated_at": "2012-10-28T14:21:25.132445Z", 
      "transaction_number": "CR286-737-8714", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR3kYB8JGRpPeU0aBX5QYLTS", 
      "available_at": "2012-10-28T21:21:25.119330Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:21:26.293196Z", 
            "updated_at": "2012-10-28T14:21:26.293198Z", 
            "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY", 
            "refunds_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC3mi2PX5C2XXj7CUFYb7NWY", 
            "credits_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:21:26.353634Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:21:26.290095Z", 
            "updated_at": "2012-10-28T14:21:26.290097Z", 
            "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/bank_accounts/BA3mhOPZOLUoi31nddCTjqcs", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA3mhOPZOLUoi31nddCTjqcs" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/credits/CR3mluQ2RSUHdobgPMkmOUU4", 
          "updated_at": "2012-10-28T14:21:26.353636Z", 
          "transaction_number": "CR446-415-8385", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR3mluQ2RSUHdobgPMkmOUU4", 
          "available_at": "2012-10-28T21:21:26.336692Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:21:26.293196Z", 
            "updated_at": "2012-10-28T14:21:26.293198Z", 
            "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY", 
            "refunds_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC3mi2PX5C2XXj7CUFYb7NWY", 
            "credits_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:21:26.354104Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:21:26.290095Z", 
            "updated_at": "2012-10-28T14:21:26.290097Z", 
            "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/accounts/AC3mi2PX5C2XXj7CUFYb7NWY/bank_accounts/BA3mhOPZOLUoi31nddCTjqcs", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA3mhOPZOLUoi31nddCTjqcs" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/credits/CR3mlzrN2drQHhNKr3VK9bdW", 
          "updated_at": "2012-10-28T14:21:26.354105Z", 
          "transaction_number": "CR578-460-4298", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR3mlzrN2drQHhNKr3VK9bdW", 
          "available_at": "2012-10-28T21:21:26.343100Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP3mciBbbjpTJ84TNqdkMuji/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description`` 
    *optional* **string**.  
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 

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
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:21:28.841243Z", 
        "updated_at": "2012-10-28T14:21:28.841245Z", 
        "uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3p9Jl9tsEkzK20PQTkcPsM", 
        "credits_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:21:28.903702Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:21:28.838351Z", 
        "updated_at": "2012-10-28T14:21:28.838354Z", 
        "uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/accounts/AC3p9Jl9tsEkzK20PQTkcPsM/bank_accounts/BA3p9vqPcWlf39Gi3uiTBAb2", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3p9vqPcWlf39Gi3uiTBAb2" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3p4ezcMj8oQguozpxkX6cY/credits/CR3pd34sxPOY2Lx60VuR1Q2M", 
      "updated_at": "2012-10-28T14:21:28.944509Z", 
      "transaction_number": "CR045-089-2760", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR3pd34sxPOY2Lx60VuR1Q2M", 
      "available_at": "2012-10-28T21:21:28.882374Z" 
    } 
 

