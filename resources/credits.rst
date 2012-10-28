Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_
- `Update a Credit`_

Fields
------

``id`` 
    *string*. The resource identifier. 
 
``uri`` 
    *string*. A URI for a Balanced entity 
 
``amount`` 
    *integer*. Amount of the credit. 
 
``created_at`` 
    *string*. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit was created. 
 
``description`` 
    *string*. A description of the credit, used for display purposes. 
 
``account`` 
    *object*. The account to which the credit is associated. 
 
``meta`` 
    *object*. A single-level dictionary of string-type key/value pairs. 
 
``transaction_number`` 
    *string*. An identifier for this transaction. 
 
``available_at`` 
    *string*. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit will be available to the merchant. 
 
``fee`` 
    *integer*. The fee charged by Balanced for this credit. 
 
``destination`` 
    *object*. The funding destination for this credit (i.e., a bank account).  
 
``state`` 
    *string*. One of ``pending``, ``cleared``, ``rejected``.  
 

Credit an Account
-----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    POST /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``amount``: *required* **integer**. USD cents. Must be **>=** your minimum credit amount  but **<=** your maximum credit amount. 
 
``description``: *optional* **string**.  
 
``meta``: *optional* **object**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as``: *optional* **string**.  
 
    Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``account_uri``: *optional* **string**.  
 
Exactly one of 
 
    ``destination_uri``: *required* **string**.  
 
    ``bank_account_uri``: *required* **string**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MP7I5wuRxkSPEjUTTdqKHWm0/accounts/AC7IcSfpIAdCJqDHJvvwzdIw" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:47:58.633816Z", 
        "updated_at": "2012-10-28T11:47:58.633818Z", 
        "uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI", 
        "refunds_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC7JEoipVBJSS53NRNAeSSoI", 
        "credits_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T11:47:58.764472Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:47:58.629581Z", 
        "updated_at": "2012-10-28T11:47:58.629584Z", 
        "uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/accounts/AC7JEoipVBJSS53NRNAeSSoI/bank_accounts/BA7JE5odL6c87ziKY2rkkMw4", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA7JE5odL6c87ziKY2rkkMw4" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP7Jx5j9two1Lb20TU4J2KAk/credits/CR7JMLQmoVUVAmt2Lk3pCKxe", 
      "updated_at": "2012-10-28T11:47:58.764475Z", 
      "transaction_number": "CR252-154-8474", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR7JMLQmoVUVAmt2Lk3pCKxe", 
      "available_at": "2012-10-28T18:47:58.753213Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:47:59.958713Z", 
        "updated_at": "2012-10-28T11:47:59.958716Z", 
        "uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM", 
        "refunds_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC7L8MfxraGKmNHjNdLM5kWM", 
        "credits_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:48:00.014961Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:47:59.954357Z", 
        "updated_at": "2012-10-28T11:47:59.954360Z", 
        "uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/accounts/AC7L8MfxraGKmNHjNdLM5kWM/bank_accounts/BA7L8sY1oc8gsVxMNdDANG04", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA7L8sY1oc8gsVxMNdDANG04" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP7L1pZmbaSsGLwicH45jXmc/credits/CR7Lc7YXeYH0rwQcHCZsRGO8", 
      "updated_at": "2012-10-28T11:48:00.014963Z", 
      "transaction_number": "CR771-816-2758", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR7Lc7YXeYH0rwQcHCZsRGO8", 
      "available_at": "2012-10-28T18:48:00.000540Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:48:01.189318Z", 
            "updated_at": "2012-10-28T11:48:01.189321Z", 
            "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i", 
            "refunds_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC7MwALRZel9kcR7CtZnxs3i", 
            "credits_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T11:48:01.272262Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:48:01.184941Z", 
            "updated_at": "2012-10-28T11:48:01.184944Z", 
            "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/bank_accounts/BA7MwhqBgHTFZSRU0q1i7284", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA7MwhqBgHTFZSRU0q1i7284" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/credits/CR7MB5aSL2V2tWW4Jr71wJxy", 
          "updated_at": "2012-10-28T11:48:01.272264Z", 
          "transaction_number": "CR522-752-8144", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR7MB5aSL2V2tWW4Jr71wJxy", 
          "available_at": "2012-10-28T18:48:01.245356Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:48:01.189318Z", 
            "updated_at": "2012-10-28T11:48:01.189321Z", 
            "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i", 
            "refunds_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC7MwALRZel9kcR7CtZnxs3i", 
            "credits_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T11:48:01.273019Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:48:01.184941Z", 
            "updated_at": "2012-10-28T11:48:01.184944Z", 
            "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/accounts/AC7MwALRZel9kcR7CtZnxs3i/bank_accounts/BA7MwhqBgHTFZSRU0q1i7284", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA7MwhqBgHTFZSRU0q1i7284" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/credits/CR7MBcPS95bitD1DRyvlGV5a", 
          "updated_at": "2012-10-28T11:48:01.273022Z", 
          "transaction_number": "CR210-029-3793", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR7MBcPS95bitD1DRyvlGV5a", 
          "available_at": "2012-10-28T18:48:01.254571Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP7MpgFYZILKpFitIjsrYkok/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description``: *optional* **string**.  
 
``meta``: *optional* **object**. Single level mapping from string keys to string values. 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:48:03.839489Z", 
        "updated_at": "2012-10-28T11:48:03.839492Z", 
        "uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw", 
        "refunds_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC2rmte06fNoJv1I9xMphYw", 
        "credits_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:48:03.923607Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:48:03.835273Z", 
        "updated_at": "2012-10-28T11:48:03.835276Z", 
        "uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/accounts/AC2rmte06fNoJv1I9xMphYw/bank_accounts/BA2r3L5Hq3NweDp4rSqaueo", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA2r3L5Hq3NweDp4rSqaueo" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP2k2UjbjYwJz3cUFAadXTe/credits/CR2vQKcc1VQDNEmEp13wnn6", 
      "updated_at": "2012-10-28T11:48:03.979124Z", 
      "transaction_number": "CR686-285-1908", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR2vQKcc1VQDNEmEp13wnn6", 
      "available_at": "2012-10-28T18:48:03.895442Z" 
    } 
 

