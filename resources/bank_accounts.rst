Bank Accounts
=============

- `Tokenize a Bank Account`_
- `Retrieve a Bank Account`_
- `Update a Bank Account`_
- `Associate a Bank Account with an Account`_


Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the bank account object  
 
``name`` 
    **string**. The name on the bank account. 
 
``last_four`` 
    **string**. The last four digits of the bank account number. 
 
``bank_code`` 
    **string**. The bank code (routing number in the USA) of the bank account. 
 
``bank_name`` 
    **string**. The name of the bank. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    bank account was tokenized. 
 
``account`` 
    **object**. The account to which this bank account is associated. 
 
``is_valid`` 
    **boolean**. Boolean flag indicating whether the bank account is currently valid. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 

Tokenize a Bank Account
-----------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/bank_accounts 
 

Request
~~~~~~~

``name`` 
    *required* **string** or **null**. Name on the bank account. Length must be **>=** ``2``. 
 
``account_number`` 
    *required* **string** or **null**. Bank account number. Length must be **>=** ``1``. 
 
``bank_code`` 
    #. If not a *production* bank account then `bank_code` is a: 
 
       ``bank_code`` 
           *required* **string** or **null**. Length must be **>=** ``1``. 
 
 
``account_type`` 
    *optional* **string** or **null**. Bank account type. It should be one of: ``checking``, ``savings`` 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "account_type": "checking",  
        "account_number": "12341234",  
        "name": "Fit Finlay",  
        "bank_code": "325182797" 
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
        "bank_name": "Banko De Ismus",  
        "account": null,  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-30T00:09:31.977726Z",  
        "uri": "/v1/marketplaces/TEST-MP5RrTmPWyvmmEwyy5tm4vRh/bank_accounts/BA5RCQ3OBnINIJafhtRdlGlZ",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA5RCQ3OBnINIJafhtRdlGlZ" 
    } 
 

Retrieve a Bank Account
-----------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/bank_accounts/(bank_account:bank_account) 
 

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
        "bank_name": null,  
        "account": null,  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-30T00:09:33.283192Z",  
        "uri": "/v1/marketplaces/TEST-MP5SWFZcwlnXckAcgXL8CEef/bank_accounts/BA5T5SJHhFmfhw8N3yv5zb35",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA5T5SJHhFmfhw8N3yv5zb35" 
    } 
 

Update a Bank Account
---------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/bank_accounts/(bank_account:bank_account) 
 

Request
~~~~~~~

``is_valid`` 
    *optional* **boolean** or **null**. Flag indicating whether the bank account is active (``true``) or not 
    (``false``). Setting this to ``false`` will deactivate the bank account. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "is_valid": "False",  
        "metadata": { 
            "my-own-field": "Customer request" 
        } 
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
        "bank_name": null,  
        "account": null,  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-30T00:09:36.073705Z",  
        "uri": "/v1/marketplaces/TEST-MP5W3ugc5TAT7Mi2cOg6Bzx1/bank_accounts/BA5Wetv3w4CRVB4Ic5Nh6U5J",  
        "is_valid": false,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA5Wetv3w4CRVB4Ic5Nh6U5J" 
    } 
 

Associate a Bank Account with an Account
----------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/bank_accounts/(bank_account:bank_account) 
 

Request
~~~~~~~

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "account_uri": "/v1/marketplaces/TEST-MP5XyjGNdcECLnSRKUIkELoT/accounts/AC5XFFJiSZJAo4nKfE0NkOr1" 
    } 
 

``account_uri`` 
    *optional* **string** or **null**. URI of an account with which to associate the bank account. 
 

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
        "bank_name": null,  
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T00:09:38.862982Z",  
            "uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC5ZmYgCMYwtOn89gZMPGRhN",  
            "credits_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/cards" 
        },  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-30T00:09:38.939656Z",  
        "uri": "/v1/marketplaces/TEST-MP5Zfafh35q4YIXfgvKUzp1V/accounts/AC5ZmYgCMYwtOn89gZMPGRhN/bank_accounts/BA5ZsjursXAEJAlwXwPAvTx1",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA5ZsjursXAEJAlwXwPAvTx1" 
    } 
 

