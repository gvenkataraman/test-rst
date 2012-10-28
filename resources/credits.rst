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

``amount``: *required* **integer**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
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
      "account_uri": "/v1/marketplaces/TEST-MP4KPK6OWEnWPOUK9hBJuB6Y/accounts/AC4KV4Ax6uyww5BozUEvrbmI" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:54:06.679374Z", 
        "updated_at": "2012-10-28T13:54:06.679377Z", 
        "uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe", 
        "refunds_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC4Mrd9pSzvqYGW4hFs1TfLe", 
        "credits_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T13:54:06.773146Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:54:06.674479Z", 
        "updated_at": "2012-10-28T13:54:06.674482Z", 
        "uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/accounts/AC4Mrd9pSzvqYGW4hFs1TfLe/bank_accounts/BA4MqRDAhag9lZclvXjTYeQ4", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA4MqRDAhag9lZclvXjTYeQ4" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP4MjwrBZ1B3HAn5C5K7gNta/credits/CR4Mxi8j9L6Cpip44Zplv5UE", 
      "updated_at": "2012-10-28T13:54:06.773148Z", 
      "transaction_number": "CR675-236-0887", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR4Mxi8j9L6Cpip44Zplv5UE", 
      "available_at": "2012-10-28T20:54:06.765782Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:54:07.924468Z", 
        "updated_at": "2012-10-28T13:54:07.924471Z", 
        "uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw", 
        "refunds_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC4NQ25Daki5lygJaXYsAaOw", 
        "credits_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T13:54:07.984410Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:54:07.919868Z", 
        "updated_at": "2012-10-28T13:54:07.919871Z", 
        "uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/accounts/AC4NQ25Daki5lygJaXYsAaOw/bank_accounts/BA4NPH8E4qhqGryFOYkB7kXi", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA4NPH8E4qhqGryFOYkB7kXi" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP4NKe2r2AMBf5HHnOtzl7Gk/credits/CR4NTENXyl9b75T1L1vVhowY", 
      "updated_at": "2012-10-28T13:54:07.984412Z", 
      "transaction_number": "CR333-626-6671", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR4NTENXyl9b75T1L1vVhowY", 
      "available_at": "2012-10-28T20:54:07.969426Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T13:54:09.154060Z", 
            "updated_at": "2012-10-28T13:54:09.154064Z", 
            "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6", 
            "refunds_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC4PdKAiq6CYPqPAYxLiJRT6", 
            "credits_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T13:54:09.215202Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T13:54:09.149246Z", 
            "updated_at": "2012-10-28T13:54:09.149249Z", 
            "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/bank_accounts/BA4PdrfyWnjmyT6Cj3LLU86w", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA4PdrfyWnjmyT6Cj3LLU86w" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/credits/CR4Ph8qwrfy3M5Tiqxj7S3LS", 
          "updated_at": "2012-10-28T13:54:09.215204Z", 
          "transaction_number": "CR598-585-2988", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR4Ph8qwrfy3M5Tiqxj7S3LS", 
          "available_at": "2012-10-28T20:54:09.196385Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T13:54:09.154060Z", 
            "updated_at": "2012-10-28T13:54:09.154064Z", 
            "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6", 
            "refunds_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC4PdKAiq6CYPqPAYxLiJRT6", 
            "credits_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T13:54:09.215775Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T13:54:09.149246Z", 
            "updated_at": "2012-10-28T13:54:09.149249Z", 
            "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/accounts/AC4PdKAiq6CYPqPAYxLiJRT6/bank_accounts/BA4PdrfyWnjmyT6Cj3LLU86w", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA4PdrfyWnjmyT6Cj3LLU86w" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/credits/CR4PhdI5dnXY0HWzJ561lkY4", 
          "updated_at": "2012-10-28T13:54:09.215777Z", 
          "transaction_number": "CR468-607-9149", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR4PhdI5dnXY0HWzJ561lkY4", 
          "available_at": "2012-10-28T20:54:09.202528Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP4P6bIcGrvYLzB0kGYS7bVy/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T13:54:11.807267Z", 
        "updated_at": "2012-10-28T13:54:11.807270Z", 
        "uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY", 
        "refunds_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC4ScNvkmdk2dRdg4VTFhtGY", 
        "credits_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T13:54:11.893110Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T13:54:11.803025Z", 
        "updated_at": "2012-10-28T13:54:11.803029Z", 
        "uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/accounts/AC4ScNvkmdk2dRdg4VTFhtGY/bank_accounts/BA4ScuFXkPUZ1lOnGoxM3v48", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA4ScuFXkPUZ1lOnGoxM3v48" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP4S5hdwXt5VnKiJWAa3y1qk/credits/CR4ShlJPP323nrkZKWItlQX2", 
      "updated_at": "2012-10-28T13:54:11.948915Z", 
      "transaction_number": "CR942-829-0170", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR4ShlJPP323nrkZKWItlQX2", 
      "available_at": "2012-10-28T20:54:11.864196Z" 
    } 
 

