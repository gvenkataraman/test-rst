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
        "created_at": "2012-10-29T16:48:57.142707Z",  
        "uri": "/v1/marketplaces/TEST-MP1Av0VYkeomNBm4LDHJMkMA/bank_accounts/BA1AIloczpl14bmSrYCLK148",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA1AIloczpl14bmSrYCLK148" 
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
        "created_at": "2012-10-29T16:48:58.694036Z",  
        "uri": "/v1/marketplaces/TEST-MP1ChlQW1D9BlP3h3AjDQMzq/bank_accounts/BA1CswwgeV83bP0uEH77aioI",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA1CswwgeV83bP0uEH77aioI" 
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
        "created_at": "2012-10-29T16:49:02.310278Z",  
        "uri": "/v1/marketplaces/TEST-MP1GkYPuKWKgln4uIWm3SDic/bank_accounts/BA1GwGTND9bKBoWSfDiOzHLK",  
        "is_valid": false,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA1GwGTND9bKBoWSfDiOzHLK" 
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
        "account_uri": "/v1/marketplaces/TEST-MP1IfGesAd6h7e08DLAJmxso/accounts/AC1ImcSTkYa5yLItVX7q7jOk" 
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
            "holds_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T16:49:05.506238Z",  
            "uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC1K7yDHTzaaxmOXEAYT0Tis",  
            "credits_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/cards" 
        },  
        "name": "Fit Finlay",  
        "bank_code": "325182797",  
        "created_at": "2012-10-29T16:49:05.572628Z",  
        "uri": "/v1/marketplaces/TEST-MP1K0cmbxAxfcSZkHCkNLOmg/accounts/AC1K7yDHTzaaxmOXEAYT0Tis/bank_accounts/BA1Kcbc02bFaDgN6hsbnALcM",  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1234",  
        "id": "BA1Kcbc02bFaDgN6hsbnALcM" 
    } 
 

