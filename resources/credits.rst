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

``amount``
    *required* **integer**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description``
    *optional* **string**
 
``meta``
    *optional* **object**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as``
    *optional* **string**. Text that will appear on the buyer's statement. Characters that can be 
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
      "account_uri": "/v1/marketplaces/TEST-MP6DAc804xfspZwanTgUh8EY/accounts/AC6DFHh01LdbLWk9hhCSY5Uw" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:55:50.411867Z", 
        "updated_at": "2012-10-28T13:55:50.411869Z", 
        "uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6F6Nay8h0w5Ku9LtcJIWYA", 
        "credits_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T13:55:50.508777Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:55:50.408975Z", 
        "updated_at": "2012-10-28T13:55:50.408977Z", 
        "uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/accounts/AC6F6Nay8h0w5Ku9LtcJIWYA/bank_accounts/BA6F6A2tl46s3dI81kwwmSeU", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6F6A2tl46s3dI81kwwmSeU" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6F1aYm6Sdmxv3BlROLzJ0U/credits/CR6FcUqaxsmR1bIqA73vDcJm", 
      "updated_at": "2012-10-28T13:55:50.508778Z", 
      "transaction_number": "CR431-059-7217", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR6FcUqaxsmR1bIqA73vDcJm", 
      "available_at": "2012-10-28T20:55:50.499035Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:55:51.713553Z", 
        "updated_at": "2012-10-28T13:55:51.713555Z", 
        "uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6Gzy7pIcTwIIsJ8jj1LGja", 
        "credits_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T13:55:51.770846Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:55:51.709240Z", 
        "updated_at": "2012-10-28T13:55:51.709243Z", 
        "uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/accounts/AC6Gzy7pIcTwIIsJ8jj1LGja/bank_accounts/BA6GzeJsNIOM5vaiNls9nRGI", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6GzeJsNIOM5vaiNls9nRGI" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6Gs6dGTAtfj9uxvrLzh9NW/credits/CR6GCYjc0tIsIdDS6Qxkwp36", 
      "updated_at": "2012-10-28T13:55:51.770848Z", 
      "transaction_number": "CR877-232-0068", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR6GCYjc0tIsIdDS6Qxkwp36", 
      "available_at": "2012-10-28T20:55:51.756458Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T13:55:52.946369Z", 
            "updated_at": "2012-10-28T13:55:52.946372Z", 
            "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm", 
            "refunds_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC6HXvT6VHyJmb6lbfuvkTvm", 
            "credits_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T13:55:53.031585Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T13:55:52.941874Z", 
            "updated_at": "2012-10-28T13:55:52.941877Z", 
            "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/bank_accounts/BA6HXccFhSBX7BLBfgrnxD4E", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA6HXccFhSBX7BLBfgrnxD4E" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/credits/CR6I2fpLZmKs6nkSP5VY2US0", 
          "updated_at": "2012-10-28T13:55:53.031588Z", 
          "transaction_number": "CR564-341-6863", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR6I2fpLZmKs6nkSP5VY2US0", 
          "available_at": "2012-10-28T20:55:53.005876Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T13:55:52.946369Z", 
            "updated_at": "2012-10-28T13:55:52.946372Z", 
            "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm", 
            "refunds_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC6HXvT6VHyJmb6lbfuvkTvm", 
            "credits_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T13:55:53.032302Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T13:55:52.941874Z", 
            "updated_at": "2012-10-28T13:55:52.941877Z", 
            "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/accounts/AC6HXvT6VHyJmb6lbfuvkTvm/bank_accounts/BA6HXccFhSBX7BLBfgrnxD4E", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA6HXccFhSBX7BLBfgrnxD4E" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/credits/CR6I2n2T2D4dnPvBEbpl8IVm", 
          "updated_at": "2012-10-28T13:55:53.032304Z", 
          "transaction_number": "CR802-740-1700", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR6I2n2T2D4dnPvBEbpl8IVm", 
          "available_at": "2012-10-28T20:55:53.015079Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP6HQ5HgJzEYtQRL9ZmeGBxy/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description``: *optional* **string**.  
 
``meta``: *optional* **object**.  
    Single level mapping from string keys to string values. 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:55:55.611704Z", 
        "updated_at": "2012-10-28T13:55:55.611706Z", 
        "uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6KXo63xJjAJiMPnK76dlVa", 
        "credits_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T13:55:55.668785Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:55:55.608153Z", 
        "updated_at": "2012-10-28T13:55:55.608155Z", 
        "uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/accounts/AC6KXo63xJjAJiMPnK76dlVa/bank_accounts/BA6KX7NuO7tmQZ0slVXp2b52", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6KX7NuO7tmQZ0slVXp2b52" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6KRZcosZoGUgf08AXdXspK/credits/CR6L0qgNFcHYXfot3zWKMina", 
      "updated_at": "2012-10-28T13:55:55.710955Z", 
      "transaction_number": "CR614-006-0869", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR6L0qgNFcHYXfot3zWKMina", 
      "available_at": "2012-10-28T20:55:55.649792Z" 
    } 
 

