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
      "account_uri": "/v1/marketplaces/TEST-MP5x260OyMa3KRdFF6G1C6zi/accounts/AC5x8iYx3jIaqWt9y1ajhhqc" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:45:58.534185Z", 
        "updated_at": "2012-10-28T11:45:58.534188Z", 
        "uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5yzv2ATbpCJAsMFhw4iqqw", 
        "credits_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T11:45:58.665411Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:45:58.529925Z", 
        "updated_at": "2012-10-28T11:45:58.529928Z", 
        "uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/accounts/AC5yzv2ATbpCJAsMFhw4iqqw/bank_accounts/BA5yzc5IwIeAGbox2CumMVQE", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5yzc5IwIeAGbox2CumMVQE" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5ytoKdlyym2Fb9fL5WLh52/credits/CR5yHUiXdNf32SRS6ZmZtdf6", 
      "updated_at": "2012-10-28T11:45:58.665413Z", 
      "transaction_number": "CR617-508-8245", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR5yHUiXdNf32SRS6ZmZtdf6", 
      "available_at": "2012-10-28T18:45:58.653971Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:45:59.869685Z", 
        "updated_at": "2012-10-28T11:45:59.869689Z", 
        "uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5A4AoafeJVzjKU2rr6eH1a", 
        "credits_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:45:59.936200Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:45:59.864805Z", 
        "updated_at": "2012-10-28T11:45:59.864808Z", 
        "uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/accounts/AC5A4AoafeJVzjKU2rr6eH1a/bank_accounts/BA5A4hmsJDqbXUktUyCnp5bu", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5A4hmsJDqbXUktUyCnp5bu" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5zX6cncDJR0tmQ1O3MY3yY/credits/CR5A8tEkFry8rRCrzQt9Ysy8", 
      "updated_at": "2012-10-28T11:45:59.936202Z", 
      "transaction_number": "CR797-956-0331", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR5A8tEkFry8rRCrzQt9Ysy8", 
      "available_at": "2012-10-28T18:45:59.918285Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:46:01.154535Z", 
            "updated_at": "2012-10-28T11:46:01.154538Z", 
            "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS", 
            "refunds_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC5BwdKb3OkmcKLVMUwZPMlS", 
            "credits_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T11:46:01.237254Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:46:01.150045Z", 
            "updated_at": "2012-10-28T11:46:01.150048Z", 
            "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/bank_accounts/BA5BvTXPNgZaiCyxsxJJx2o4", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA5BvTXPNgZaiCyxsxJJx2o4" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/credits/CR5BAM6ZIVv8NTXp6UZs4GLW", 
          "updated_at": "2012-10-28T11:46:01.237257Z", 
          "transaction_number": "CR917-019-6629", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR5BAM6ZIVv8NTXp6UZs4GLW", 
          "available_at": "2012-10-28T18:46:01.211428Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T11:46:01.154535Z", 
            "updated_at": "2012-10-28T11:46:01.154538Z", 
            "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS", 
            "refunds_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC5BwdKb3OkmcKLVMUwZPMlS", 
            "credits_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T11:46:01.238007Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T11:46:01.150045Z", 
            "updated_at": "2012-10-28T11:46:01.150048Z", 
            "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/accounts/AC5BwdKb3OkmcKLVMUwZPMlS/bank_accounts/BA5BvTXPNgZaiCyxsxJJx2o4", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA5BvTXPNgZaiCyxsxJJx2o4" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/credits/CR5BATwHOnEvyTA6jv2Snvla", 
          "updated_at": "2012-10-28T11:46:01.238009Z", 
          "transaction_number": "CR313-880-1417", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR5BATwHOnEvyTA6jv2Snvla", 
          "available_at": "2012-10-28T18:46:01.220624Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP5BoFDgjSmFvoAyi7HFgUF6/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T11:46:04.413740Z", 
        "updated_at": "2012-10-28T11:46:04.413743Z", 
        "uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5FbuQhnHrNePitxxxszcfG", 
        "credits_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T11:46:04.498704Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T11:46:04.409290Z", 
        "updated_at": "2012-10-28T11:46:04.409293Z", 
        "uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/accounts/AC5FbuQhnHrNePitxxxszcfG/bank_accounts/BA5FbbamYFCS42dYy8sTmBXC", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5FbbamYFCS42dYy8sTmBXC" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5F5isdfQP670t1udvhfdFG/credits/CR5Fg1H0FKSSDRvE2I4ZYPcw", 
      "updated_at": "2012-10-28T11:46:04.555393Z", 
      "transaction_number": "CR212-896-9238", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR5Fg1H0FKSSDRvE2I4ZYPcw", 
      "available_at": "2012-10-28T18:46:04.470357Z" 
    } 
 

