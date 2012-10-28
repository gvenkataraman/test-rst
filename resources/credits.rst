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
      "account_uri": "/v1/marketplaces/TEST-MP2OmW6ZHoPXufi0Z7eqiBFO/accounts/AC2OtASyRNjsCPQA0SVJhfTe" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:28:07.006777Z", 
        "updated_at": "2012-10-28T14:28:07.006779Z", 
        "uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S", 
        "refunds_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC2PUUnWvuxQRS6XnFQfTT3S", 
        "credits_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:28:07.107079Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:28:07.003760Z", 
        "updated_at": "2012-10-28T14:28:07.003763Z", 
        "uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/accounts/AC2PUUnWvuxQRS6XnFQfTT3S/bank_accounts/BA2PUHdZnvHi77q5kvf5tqPW", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA2PUHdZnvHi77q5kvf5tqPW" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP2PPIMxL0Whf9jJPGVceYWo/credits/CR2Q1lUc9YUeDVmeUtaOxhEU", 
      "updated_at": "2012-10-28T14:28:07.107081Z", 
      "transaction_number": "CR751-496-5333", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR2Q1lUc9YUeDVmeUtaOxhEU", 
      "available_at": "2012-10-28T21:28:07.098455Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:28:08.304683Z", 
        "updated_at": "2012-10-28T14:28:08.304685Z", 
        "uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs", 
        "refunds_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC2RnpZdAYwMkcmk1ZEGfmcs", 
        "credits_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:28:08.355546Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:28:08.301389Z", 
        "updated_at": "2012-10-28T14:28:08.301391Z", 
        "uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/accounts/AC2RnpZdAYwMkcmk1ZEGfmcs/bank_accounts/BA2RnbruidphOTKSNYMfa9Fi", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA2RnbruidphOTKSNYMfa9Fi" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP2Rh6z1Sxkn7DqMlCxCEtbC/credits/CR2RqqoB2O4A7lwMXsew7EcQ", 
      "updated_at": "2012-10-28T14:28:08.355548Z", 
      "transaction_number": "CR876-900-3576", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR2RqqoB2O4A7lwMXsew7EcQ", 
      "available_at": "2012-10-28T21:28:08.342393Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:28:09.545164Z", 
            "updated_at": "2012-10-28T14:28:09.545167Z", 
            "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK", 
            "refunds_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC2SLUCEGfNXBomRPVXwcLPK", 
            "credits_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:28:09.611483Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:28:09.540644Z", 
            "updated_at": "2012-10-28T14:28:09.540647Z", 
            "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/bank_accounts/BA2SLAy5iM9FCNfhnPXhMV80", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA2SLAy5iM9FCNfhnPXhMV80" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/credits/CR2SPCFe2mIeUrlErraFkFrC", 
          "updated_at": "2012-10-28T14:28:09.611485Z", 
          "transaction_number": "CR723-310-1600", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR2SPCFe2mIeUrlErraFkFrC", 
          "available_at": "2012-10-28T21:28:09.591529Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:28:09.545164Z", 
            "updated_at": "2012-10-28T14:28:09.545167Z", 
            "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK", 
            "refunds_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC2SLUCEGfNXBomRPVXwcLPK", 
            "credits_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:28:09.612061Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:28:09.540644Z", 
            "updated_at": "2012-10-28T14:28:09.540647Z", 
            "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/accounts/AC2SLUCEGfNXBomRPVXwcLPK/bank_accounts/BA2SLAy5iM9FCNfhnPXhMV80", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA2SLAy5iM9FCNfhnPXhMV80" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/credits/CR2SPJLmUTJRWwpy9Q4J2FVi", 
          "updated_at": "2012-10-28T14:28:09.612063Z", 
          "transaction_number": "CR745-211-7261", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR2SPJLmUTJRWwpy9Q4J2FVi", 
          "available_at": "2012-10-28T21:28:09.599102Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP2SEdhYZgd2plOpFhW9H2qU/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:28:12.147164Z", 
        "updated_at": "2012-10-28T14:28:12.147167Z", 
        "uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG", 
        "refunds_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC2VHmzV2NNJ4sYWbSPfIgbG", 
        "credits_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:28:12.207216Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:28:12.143997Z", 
        "updated_at": "2012-10-28T14:28:12.144000Z", 
        "uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/accounts/AC2VHmzV2NNJ4sYWbSPfIgbG/bank_accounts/BA2VH8LdMBk7GynKkBZGk9mI", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA2VH8LdMBk7GynKkBZGk9mI" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP2VB5ZiXRB6kkQkWy5URXQ8/credits/CR2VKG6D0yuKBHkmajYFDiuw", 
      "updated_at": "2012-10-28T14:28:12.244290Z", 
      "transaction_number": "CR463-545-7580", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR2VKG6D0yuKBHkmajYFDiuw", 
      "available_at": "2012-10-28T21:28:12.189140Z" 
    } 
 

