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
 
``destination_uri`` 
    *required* **string**.  
 
``bank_account_uri`` 
    *required* **string**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MP5StWEYs2gSnaQpewhDFvjC/accounts/AC5Sz2VRC1gkVv91hLxJBotm" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:23:46.502201Z", 
        "updated_at": "2012-10-28T14:23:46.502204Z", 
        "uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5TZdjLSvkAV2zDLnNcVW16", 
        "credits_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:23:46.608502Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:23:46.498666Z", 
        "updated_at": "2012-10-28T14:23:46.498669Z", 
        "uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/accounts/AC5TZdjLSvkAV2zDLnNcVW16/bank_accounts/BA5TYX9MXzw41aZ7QRgrdDpi", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5TYX9MXzw41aZ7QRgrdDpi" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5TTwHTyBm2KUq20yhpLJS4/credits/CR5U5SJ0Hxbqzew2I5LNGSyg", 
      "updated_at": "2012-10-28T14:23:46.608504Z", 
      "transaction_number": "CR808-294-4060", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR5U5SJ0Hxbqzew2I5LNGSyg", 
      "available_at": "2012-10-28T21:23:46.597087Z" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:23:47.820101Z", 
        "updated_at": "2012-10-28T14:23:47.820103Z", 
        "uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5Vt7wq1VQvfa0ZqLcYrKTi", 
        "credits_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:23:47.878185Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:23:47.816939Z", 
        "updated_at": "2012-10-28T14:23:47.816942Z", 
        "uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/accounts/AC5Vt7wq1VQvfa0ZqLcYrKTi/bank_accounts/BA5VsTifW5QKsLYlGVtTXmrG", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5VsTifW5QKsLYlGVtTXmrG" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5VmxOK3t3AhPPyBJTkR3jC/credits/CR5VwCDf53LoUAfi1tcJPcYk", 
      "updated_at": "2012-10-28T14:23:47.878186Z", 
      "transaction_number": "CR708-756-2491", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CR5VwCDf53LoUAfi1tcJPcYk", 
      "available_at": "2012-10-28T21:23:47.864765Z" 
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
      "first_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:23:49.037873Z", 
            "updated_at": "2012-10-28T14:23:49.037875Z", 
            "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6", 
            "refunds_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC5WQ2beGUpmZ4kAQLjtF3X6", 
            "credits_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:23:49.100409Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:23:49.034355Z", 
            "updated_at": "2012-10-28T14:23:49.034357Z", 
            "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/bank_accounts/BA5WPMAU8FwfDta6LPeOhXCc", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA5WPMAU8FwfDta6LPeOhXCc" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/credits/CR5WToKVfYgzvc0YSKgz7Gpm", 
          "updated_at": "2012-10-28T14:23:49.100411Z", 
          "transaction_number": "CR358-854-6858", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR5WToKVfYgzvc0YSKgz7Gpm", 
          "available_at": "2012-10-28T21:23:49.079798Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:23:49.037873Z", 
            "updated_at": "2012-10-28T14:23:49.037875Z", 
            "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6", 
            "refunds_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "AC5WQ2beGUpmZ4kAQLjtF3X6", 
            "credits_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:23:49.101088Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:23:49.034355Z", 
            "updated_at": "2012-10-28T14:23:49.034357Z", 
            "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/accounts/AC5WQ2beGUpmZ4kAQLjtF3X6/bank_accounts/BA5WPMAU8FwfDta6LPeOhXCc", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BA5WPMAU8FwfDta6LPeOhXCc" 
          }, 
          "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/credits/CR5WTtZgBlVln8uOvOc72SLG", 
          "updated_at": "2012-10-28T14:23:49.101090Z", 
          "transaction_number": "CR878-327-8180", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CR5WTtZgBlVln8uOvOc72SLG", 
          "available_at": "2012-10-28T21:23:49.086528Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MP5WKl7KAcpfblGzr2ZX1RCQ/credits?limit=10&offset=0" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:23:51.731107Z", 
        "updated_at": "2012-10-28T14:23:51.731110Z", 
        "uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw", 
        "refunds_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "AC5ZRPCONgT5dHz5la4PMfAw", 
        "credits_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:23:51.805366Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:23:51.725422Z", 
        "updated_at": "2012-10-28T14:23:51.725425Z", 
        "uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/accounts/AC5ZRPCONgT5dHz5la4PMfAw/bank_accounts/BA5ZRqMQXcqeFc6GhkTbnU3i", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BA5ZRqMQXcqeFc6GhkTbnU3i" 
      }, 
      "uri": "/v1/marketplaces/TEST-MP5ZMaNnCB0PBVn8dRLYu4ao/credits/CR5ZVVANjRoq9DmQkgVLSN1y", 
      "updated_at": "2012-10-28T14:23:51.854521Z", 
      "transaction_number": "CR401-973-9766", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CR5ZVVANjRoq9DmQkgVLSN1y", 
      "available_at": "2012-10-28T21:23:51.782928Z" 
    } 
 

