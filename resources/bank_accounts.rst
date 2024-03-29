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
    **object**. The account to which this bank account is associated. See `Accounts <./accounts.rst>`_. 
 
``is_valid`` 
    **boolean**. Boolean flag indicating whether the bank account is currently valid. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 

Tokenize a Bank Account
-----------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/bank_accounts 
 

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
        "created_at": "2012-10-30T10:13:04.183353Z",  
        "uri": "/v1/marketplaces/TEST-MPvzoAZFvpnlK9lCywmCIbW/bank_accounts/BAvOuCuF9q4lyuySMIc8OmE",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BAvOuCuF9q4lyuySMIc8OmE" 
    } 
 

Retrieve a Bank Account
-----------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/bank_accounts/(bank_account-id) 
 

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
        "created_at": "2012-10-30T10:13:05.425435Z",  
        "uri": "/v1/marketplaces/TEST-MPx0UiykPRp3hYTdbJQHkCU/bank_accounts/BAxd7fPrmTSZPyhIBBwCbaY",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BAxd7fPrmTSZPyhIBBwCbaY" 
    } 
 

Update a Bank Account
---------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/bank_accounts/(bank_account-id) 
 

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
        "created_at": "2012-10-30T10:13:07.970949Z",  
        "uri": "/v1/marketplaces/TEST-MPzSZZXXDGDg0x8wc8iEGvW/bank_accounts/BAA4D3ksgDKaytI2kzsdy7i",  
        "is_valid": false,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BAA4D3ksgDKaytI2kzsdy7i" 
    } 
 

Associate a Bank Account with an Account
----------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/bank_accounts/(bank_account-id) 
 

Request
~~~~~~~

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "account_uri": "/v1/marketplaces/TEST-MPBhOz7Zk1u0u4d2vp1WpVO/accounts/ACBpaejME5ItOaBqZIdSTTS" 
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
            "holds_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-30T10:13:10.479903Z",  
            "uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/transactions",  
            "email_address": "email.7@y.com",  
            "id": "ACCTAj3mJEbr6ggHaVVTY2w",  
            "credits_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/cards" 
        },  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-30T10:13:10.550556Z",  
        "uri": "/v1/marketplaces/TEST-MPCMfGJrhUvkXR2CTOfxIWw/accounts/ACCTAj3mJEbr6ggHaVVTY2w/bank_accounts/BACYvmlsCJIpVG7Own7dZha",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BACYvmlsCJIpVG7Own7dZha" 
    } 
 

