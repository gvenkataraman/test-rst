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

.. pilo: balanced_service.forms.CreateCreditForm

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MP3QoPU0qe7f22YcSjiwlv3S/accounts/AC3QwdGh3hFdUc7xhFV7Wa7G" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:44:25.578224Z", 
        "updated_at": "2012-10-28T11:44:25.578227Z", 
        "uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3S1pFQggRJ4zZffW2SU6IA", 
        "credits_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T11:44:25.680629Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:44:25.573980Z", 
        "updated_at": "2012-10-28T11:44:25.573983Z", 
        "uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/accounts/AC3S1pFQggRJ4zZffW2SU6IA/bank_accounts/BA3S16VPCOJetRcMjcszAVuc", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3S16VPCOJetRcMjcszAVuc" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3RTYVXpPq7Pk7mePobGETO/credits/CR3S7Y83geQtIVjQy6IU0B92", 
      "updated_at": "2012-10-28T11:44:25.680631Z", 
      "transaction_number": "CR737-707-5847", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR3S7Y83geQtIVjQy6IU0B92", 
      "available_at": "2012-10-28T18:44:25.671476Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    HEAD /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    HEAD /v1/marketplaces/(marketplace:marketplace)/credits/(credit:credit) 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:44:26.854061Z", 
        "updated_at": "2012-10-28T11:44:26.854064Z", 
        "uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3TsnMD1g3T0VZKsrqHJTYo", 
        "credits_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:44:26.930632Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:44:26.849840Z", 
        "updated_at": "2012-10-28T11:44:26.849843Z", 
        "uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/accounts/AC3TsnMD1g3T0VZKsrqHJTYo/bank_accounts/BA3Ts4XNeFMGScR70u3n6Buc", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3Ts4XNeFMGScR70u3n6Buc" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3TmvH4tunJrX69qiNgdrIU/credits/CR3TwRYePgtnEdwFWT8oWbYw", 
      "updated_at": "2012-10-28T11:44:26.930634Z", 
      "transaction_number": "CR261-741-5886", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR3TwRYePgtnEdwFWT8oWbYw", 
      "available_at": "2012-10-28T18:44:26.909913Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:44:28.141475Z", 
            "updated_at": "2012-10-28T11:44:28.141478Z", 
            "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru", 
            "refunds_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC3UU9OCKYiDiVHv16X7wzru", 
            "credits_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T11:44:28.226516Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:44:28.137077Z", 
            "updated_at": "2012-10-28T11:44:28.137080Z", 
            "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/bank_accounts/BA3UTQiTSZSYhVBzYJr9yTNG", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA3UTQiTSZSYhVBzYJr9yTNG" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/credits/CR3UYRvDeECV86oWlWkiOvfm", 
          "updated_at": "2012-10-28T11:44:28.226518Z", 
          "transaction_number": "CR911-377-6757", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR3UYRvDeECV86oWlWkiOvfm", 
          "available_at": "2012-10-28T18:44:28.200453Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:44:28.141475Z", 
            "updated_at": "2012-10-28T11:44:28.141478Z", 
            "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru", 
            "refunds_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC3UU9OCKYiDiVHv16X7wzru", 
            "credits_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T11:44:28.227265Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:44:28.137077Z", 
            "updated_at": "2012-10-28T11:44:28.137080Z", 
            "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/accounts/AC3UU9OCKYiDiVHv16X7wzru/bank_accounts/BA3UTQiTSZSYhVBzYJr9yTNG", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA3UTQiTSZSYhVBzYJr9yTNG" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/credits/CR3UYYYi8sYuISsXKIfNn3A8", 
          "updated_at": "2012-10-28T11:44:28.227267Z", 
          "transaction_number": "CR257-192-8030", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR3UYYYi8sYuISsXKIfNn3A8", 
          "available_at": "2012-10-28T18:44:28.209781Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP3UMM6UEEkqrTMdDG8fXGza/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:44:31.339186Z", 
        "updated_at": "2012-10-28T11:44:31.339189Z", 
        "uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8", 
        "refunds_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC3Yv8nfEaGmNiJmh89FFVE8", 
        "credits_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:44:31.409997Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:44:31.335299Z", 
        "updated_at": "2012-10-28T11:44:31.335302Z", 
        "uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/accounts/AC3Yv8nfEaGmNiJmh89FFVE8/bank_accounts/BA3YuRYg33jSbDO5UmhhoB8g", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA3YuRYg33jSbDO5UmhhoB8g" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP3YpLK351XGWcOGA0TYq6FK/credits/CR3Yz4FRqTwTAXFCVv0QmBbS", 
      "updated_at": "2012-10-28T11:44:31.455177Z", 
      "transaction_number": "CR833-366-3865", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR3Yz4FRqTwTAXFCVv0QmBbS", 
      "available_at": "2012-10-28T18:44:31.389490Z" 
    } 
 

