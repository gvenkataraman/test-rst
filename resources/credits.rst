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
 
One of: 
 
    ``destination_uri`` 
        *required* **string**.  
 
    ``bank_account_uri`` 
        *required* **string**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MP1It57kWY7bOrmj7YiVqQio/accounts/AC1Iz6UWqz5qOAqBdKOVkz8o" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:27:06.616722Z", 
        "updated_at": "2012-10-28T14:27:06.616725Z", 
        "uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg", 
        "refunds_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC1JZJFxSpjIecrj7a6BmJMg", 
        "credits_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:27:06.710817Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:27:06.613117Z", 
        "updated_at": "2012-10-28T14:27:06.613119Z", 
        "uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/accounts/AC1JZJFxSpjIecrj7a6BmJMg/bank_accounts/BA1JZtZjHs2bd2oaDQhNu9Ug", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA1JZtZjHs2bd2oaDQhNu9Ug" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP1JTRql2nm9zcPn4zT7c31a/credits/CR1K5HJyhHyeU4lt2gFzGQny", 
      "updated_at": "2012-10-28T14:27:06.710819Z", 
      "transaction_number": "CR712-239-0280", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR1K5HJyhHyeU4lt2gFzGQny", 
      "available_at": "2012-10-28T21:27:06.701611Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:27:07.912435Z", 
        "updated_at": "2012-10-28T14:27:07.912438Z", 
        "uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm", 
        "refunds_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC1Ls5rxjmNuVkynjHqLpvrm", 
        "credits_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:27:07.969723Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:27:07.908138Z", 
        "updated_at": "2012-10-28T14:27:07.908141Z", 
        "uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/accounts/AC1Ls5rxjmNuVkynjHqLpvrm/bank_accounts/BA1LrMjoWfXuAzZ3QQTltJVW", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA1LrMjoWfXuAzZ3QQTltJVW" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP1LkuMJO51gMee0z1s7CtGA/credits/CR1LvAhcJ8F0DQoXFQaFRd3K", 
      "updated_at": "2012-10-28T14:27:07.969725Z", 
      "transaction_number": "CR740-885-7822", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR1LvAhcJ8F0DQoXFQaFRd3K", 
      "available_at": "2012-10-28T21:27:07.956236Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:27:09.144789Z", 
            "updated_at": "2012-10-28T14:27:09.144791Z", 
            "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2", 
            "refunds_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC1MQ1RRVEg7AfQ0bQgKhUr2", 
            "credits_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:27:09.204972Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:27:09.141596Z", 
            "updated_at": "2012-10-28T14:27:09.141599Z", 
            "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/bank_accounts/BA1MPMDfxv0acGhhnpfFSkKg", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA1MPMDfxv0acGhhnpfFSkKg" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/credits/CR1MTcfnt4TGDV2owm1ShRdi", 
          "updated_at": "2012-10-28T14:27:09.204974Z", 
          "transaction_number": "CR161-837-5526", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR1MTcfnt4TGDV2owm1ShRdi", 
          "available_at": "2012-10-28T21:27:09.182993Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:27:09.144789Z", 
            "updated_at": "2012-10-28T14:27:09.144791Z", 
            "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2", 
            "refunds_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC1MQ1RRVEg7AfQ0bQgKhUr2", 
            "credits_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:27:09.205555Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:27:09.141596Z", 
            "updated_at": "2012-10-28T14:27:09.141599Z", 
            "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/accounts/AC1MQ1RRVEg7AfQ0bQgKhUr2/bank_accounts/BA1MPMDfxv0acGhhnpfFSkKg", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA1MPMDfxv0acGhhnpfFSkKg" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/credits/CR1MTiZxz7Jeb5mpuXT3JZYw", 
          "updated_at": "2012-10-28T14:27:09.205557Z", 
          "transaction_number": "CR227-224-5695", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR1MTiZxz7Jeb5mpuXT3JZYw", 
          "available_at": "2012-10-28T21:27:09.190977Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP1MKPl6Eo5Yrf0ZxLPZkhow/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:27:11.764820Z", 
        "updated_at": "2012-10-28T14:27:11.764822Z", 
        "uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2", 
        "refunds_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC1PMJJbl1jUBVg3Icp3Z1l2", 
        "credits_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:27:11.820789Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:27:11.761645Z", 
        "updated_at": "2012-10-28T14:27:11.761647Z", 
        "uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/accounts/AC1PMJJbl1jUBVg3Icp3Z1l2/bank_accounts/BA1PMvk1QWe754QtBt9ymH2c", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA1PMvk1QWe754QtBt9ymH2c" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP1PFfS1YVHhTxXh4U8euyfG/credits/CR1PPIjrrF88xP9FhdTb1TVi", 
      "updated_at": "2012-10-28T14:27:11.857480Z", 
      "transaction_number": "CR410-887-7439", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR1PPIjrrF88xP9FhdTb1TVi", 
      "available_at": "2012-10-28T21:27:11.801901Z" 
    } 
 

