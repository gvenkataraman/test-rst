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
        "created_at": "2012-10-29T15:56:16.095034Z",  
        "uri": "/v1/marketplaces/TEST-MP6zKjWr1Y9tElHhhUtMx3us/bank_accounts/BA6zVJrIEXyw47a8eLmF2SAQ",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA6zVJrIEXyw47a8eLmF2SAQ" 
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
        "created_at": "2012-10-29T15:56:17.674169Z",  
        "uri": "/v1/marketplaces/TEST-MP6Bw8FK5MKpQt5Ut1Eb9JyI/bank_accounts/BA6BHQzRqVMDWHZI2H2kBTo0",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA6BHQzRqVMDWHZI2H2kBTo0" 
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
        "created_at": "2012-10-29T15:56:21.283724Z",  
        "uri": "/v1/marketplaces/TEST-MP6FzOOfwI9nC1XG75SogUTi/bank_accounts/BA6FLyEbGX0nPKplRs4eWYSM",  
        "is_valid": false,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA6FLyEbGX0nPKplRs4eWYSM" 
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
        "account_uri": "/v1/marketplaces/TEST-MP6HC7xyQFBrKNCv2w7zcSPy/accounts/AC6HJmwBPTi3EimGxKoL8k5e" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:56:24.700135Z",  
            "uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC6JBNDfB0PmDevnisLrCX2Y",  
            "credits_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/cards" 
        },  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-29T15:56:24.753732Z",  
        "uri": "/v1/marketplaces/TEST-MP6JvhLBymiqJwCXZ57wI1nK/accounts/AC6JBNDfB0PmDevnisLrCX2Y/bank_accounts/BA6JFxrsfa99TY3s7DdGJQaM",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA6JFxrsfa99TY3s7DdGJQaM" 
    } 
 

