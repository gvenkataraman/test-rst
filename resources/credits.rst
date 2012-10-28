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
      "account_uri": "/v1/marketplaces/TEST-MP6kDubRkMDXLgCni0eK8kte/accounts/AC6kJTk98A28Itz82DZju8Ac" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:17:02.127661Z", 
        "updated_at": "2012-10-28T14:17:02.127663Z", 
        "uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6mf40e57YyCB5pbDrwxpcw", 
        "credits_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:17:02.217766Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:17:02.124632Z", 
        "updated_at": "2012-10-28T14:17:02.124635Z", 
        "uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/accounts/AC6mf40e57YyCB5pbDrwxpcw/bank_accounts/BA6meQooxWxuHmM00i3llBJ2", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6meQooxWxuHmM00i3llBJ2" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6m8jDgjhotZAMDTQOGckD2/credits/CR6mkSK2FR3A4rtB5V5LOuq0", 
      "updated_at": "2012-10-28T14:17:02.217768Z", 
      "transaction_number": "CR134-759-0551", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR6mkSK2FR3A4rtB5V5LOuq0", 
      "available_at": "2012-10-28T21:17:02.210539Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:17:03.382460Z", 
        "updated_at": "2012-10-28T14:17:03.382463Z", 
        "uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6nEyP4sHXSFi0jMCOcRLxO", 
        "credits_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:17:03.439983Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:17:03.378971Z", 
        "updated_at": "2012-10-28T14:17:03.378973Z", 
        "uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/accounts/AC6nEyP4sHXSFi0jMCOcRLxO/bank_accounts/BA6nEjqgxviF7Vt11aexdhcM", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6nEjqgxviF7Vt11aexdhcM" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6nztYUhRryHi3B6pHrQmsQ/credits/CR6nI3mMnW5dQe4PukkquHuA", 
      "updated_at": "2012-10-28T14:17:03.439985Z", 
      "transaction_number": "CR790-921-7960", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR6nI3mMnW5dQe4PukkquHuA", 
      "available_at": "2012-10-28T21:17:03.426233Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:17:04.607486Z", 
            "updated_at": "2012-10-28T14:17:04.607489Z", 
            "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc", 
            "refunds_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC6p1YvayiAvxlQdVn8txyIc", 
            "credits_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:17:04.692243Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:17:04.603338Z", 
            "updated_at": "2012-10-28T14:17:04.603341Z", 
            "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/bank_accounts/BA6p1GaCKtYal6vcRcrFkF6s", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA6p1GaCKtYal6vcRcrFkF6s" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/credits/CR6p6DP12tDn8lDuTUTvqVeY", 
          "updated_at": "2012-10-28T14:17:04.692247Z", 
          "transaction_number": "CR019-653-8265", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR6p6DP12tDn8lDuTUTvqVeY", 
          "available_at": "2012-10-28T21:17:04.665906Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:17:04.607486Z", 
            "updated_at": "2012-10-28T14:17:04.607489Z", 
            "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc", 
            "refunds_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC6p1YvayiAvxlQdVn8txyIc", 
            "credits_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:17:04.693210Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:17:04.603338Z", 
            "updated_at": "2012-10-28T14:17:04.603341Z", 
            "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/accounts/AC6p1YvayiAvxlQdVn8txyIc/bank_accounts/BA6p1GaCKtYal6vcRcrFkF6s", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA6p1GaCKtYal6vcRcrFkF6s" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/credits/CR6p6LxL63MCytyKE67JJRL6", 
          "updated_at": "2012-10-28T14:17:04.693212Z", 
          "transaction_number": "CR970-420-3143", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR6p6LxL63MCytyKE67JJRL6", 
          "available_at": "2012-10-28T21:17:04.675229Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP6oUsODeCFnqQ8sslMDVl8o/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:17:07.258377Z", 
        "updated_at": "2012-10-28T14:17:07.258380Z", 
        "uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU", 
        "refunds_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC6s0PfTNy0qbx8hfZLzjqGU", 
        "credits_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:17:07.328690Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:17:07.253846Z", 
        "updated_at": "2012-10-28T14:17:07.253849Z", 
        "uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/accounts/AC6s0PfTNy0qbx8hfZLzjqGU/bank_accounts/BA6s0vthUC6iKvMLskZ1IlEM", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA6s0vthUC6iKvMLskZ1IlEM" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP6rThnsv0sQ8c1pgSjiIULy/credits/CR6s4J5blECbyz9BGphaNIm8", 
      "updated_at": "2012-10-28T14:17:07.371864Z", 
      "transaction_number": "CR315-516-3699", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR6s4J5blECbyz9BGphaNIm8", 
      "available_at": "2012-10-28T21:17:07.308463Z" 
    } 
 

