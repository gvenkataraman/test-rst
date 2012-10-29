Accounts
========

- `Create a Buyer`_
- `Create a Person Merchant`_
- `Create a Business Merchant`_
- `Retrieve an Account`_
- `List all Accounts`_
- `Update an Account`_
- `Promote a Buyer Account to a Merchant`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the account. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    account was created. 
 
``name`` 
    **string**. The name of the account. 
 
``email_address`` 
    **string**. The email address of the account. 
 
``roles`` 
    **list**. A list of roles the account has. Can be zero, one, or both of 
    ``buyer``, ``merchant`` 
 
``debits_uri`` 
    **string**. URI for all debits associated with the account. 
 
``credits_uri`` 
    **string**. URI for all credits associated with the account. 
 
``refunds_uri`` 
    **string**. URI for all refunds associated with the account. 
 
``holds_uri`` 
    **string**. URI for all holds associated with the account. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``transactions_uri`` 
    **string**. URI for all transactions associated with the account. 
 
``bank_accounts_uri`` 
    **string**. URI for all bank accounts associated with the account. 
 
``cards_uri`` 
    **string**. URI for all cards associated with the account. 
 

Create a Buyer
--------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``card_uri`` 
    *optional* **string** or **null**. The URI of the tokenized card. 
 
``card`` 
    *optional* **object** or **null**. See `Create a Card <./cards.rst#create-a-card>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MPGNazYBCzlo3dI06vXsDWI/cards/CC16c89b08221311e2a68280ee7316ae44",  
        "email_address": "b@m.com",  
        "name": "Benny Riemann" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T14:53:37.042370Z",  
        "uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/transactions",  
        "email_address": "b@m.com",  
        "id": "ACIywmoSAWZy3aeC2Hmingo",  
        "credits_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPIi9TlqBshGqofJBvZIk6M/accounts/ACIywmoSAWZy3aeC2Hmingo/cards" 
    } 
 

Create a Business Merchant
--------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. The URI of the bank account created via *balanced.js*. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 
``merchant_uri`` 
    *optional* **string** or **null**. The URI of the merchant account created during a request for more 
    information. 
 
``merchant`` 
    *optional* **object** or **null**.  
        ``type`` 
            *required* **string** or **null**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string** or **null**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
        ``person`` 
            *optional* **object** or **null**.  
                ``name`` 
                    *required* **string** or **null**.  
 
                ``dob`` 
                    *required* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
                ``city`` 
                    *optional* **string** or **null**. City. 
 
                ``postal_code`` 
                    *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
                    *requires* ``country_code``. 
 
                ``street_address`` 
                    *required* **string** or **null**. Street address. 
                    *requires* ``postal_code``. 
 
                ``country_code`` 
                    *optional* **string** or **null**. `ISO-3166-3 
                    <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
                    three character country code. 
 
                ``tax_id`` 
                    *optional* **string** or **null**. Length must be **=** ``9``. 
 
 
        ``name`` 
            *optional* **string** or **null**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean** or **null**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string** or **null**. City. 
 
        ``postal_code`` 
            *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
            *requires* ``country_code``. 
 
        ``street_address`` 
            *required* **string** or **null**. Street address. 
            *requires* ``postal_code``. 
 
        ``country_code`` 
            *optional* **string** or **null**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "person": { 
                "city": "San Francisco",  
                "state": "CA",  
                "postal_code": "94110",  
                "name": "jo",  
                "dob": "1984-01",  
                "street_address": "Somewhere over the rainbow",  
                "tax_id": "115044400" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "322674300" 
        } 
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
        "holds_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T14:53:39.749696Z",  
        "uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/transactions",  
        "email_address": null,  
        "id": "ACLBj4PBFh3CxDFbrBR3qgA",  
        "credits_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPLnOHq5fqQVe2gifnBdOYI/accounts/ACLBj4PBFh3CxDFbrBR3qgA/cards" 
    } 
 

Create a Person Merchant
------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. The URI of the bank account created via *balanced.js*. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 
``merchant_uri`` 
    *optional* **string** or **null**. The URI of the merchant account created during a request for more 
    information. 
 
``merchant`` 
    *optional* **object** or **null**.  
        ``type`` 
            *required* **string** or **null**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string** or **null**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string** or **null**. Date-of-birth formatted as ``YYYY-MM-DD``. 
 
        ``name`` 
            *optional* **string** or **null**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean** or **null**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string** or **null**. City. 
 
        ``postal_code`` 
            *required* **string** or **null**. Postal code. This is known as a zip code in the USA. 
            *requires* ``country_code``. 
 
        ``street_address`` 
            *required* **string** or **null**. Street address. 
            *requires* ``postal_code``. 
 
        ``country_code`` 
            *optional* **string** or **null**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "dob": "1984-01",  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "person",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "445502800" 
        } 
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
        "holds_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T14:53:42.304495Z",  
        "uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/transactions",  
        "email_address": null,  
        "id": "ACOtsOBEvgXhPoH6Mivs9OQ",  
        "credits_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPOfxnrYnoXmX0WkCRdbx9W/accounts/ACOtsOBEvgXhPoH6Mivs9OQ/cards" 
    } 
 

Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Body 
~~~~ 
 
Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 200 OK 
 
Body 
~~~~ 
 
.. code:: javascript 
 
    { 
        "holds_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T14:53:43.546540Z",  
        "uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/transactions",  
        "email_address": "email.10@y.com",  
        "id": "ACPS4FXzNUFYUA4XNQXz1uA",  
        "credits_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPPHCpxvjzS55KD8nCs9BGc/accounts/ACPS4FXzNUFYUA4XNQXz1uA/cards" 
    } 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts 
 

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
        "first_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.855510Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/transactions",  
                "email_address": "email.11@y.com",  
                "id": "ACRln0c6gT9QAGHcCbNy1FO",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRln0c6gT9QAGHcCbNy1FO/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.856342Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/transactions",  
                "email_address": "email.12@y.com",  
                "id": "ACRlqJfVMv175AAqIagwXLS",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRlqJfVMv175AAqIagwXLS/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.879292Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/transactions",  
                "email_address": "email.14@y.com",  
                "id": "ACRn1xlg9nuv4V19snIPx88",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRn1xlg9nuv4V19snIPx88/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.730007Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/transactions",  
                "email_address": "email.2@y.com",  
                "id": "ACRcAz4m7u8d8fBzMFCRJac",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRcAz4m7u8d8fBzMFCRJac/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.788073Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/transactions",  
                "email_address": "email.7@y.com",  
                "id": "ACRgFub0PEULSmceGl3o1Ja",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgFub0PEULSmceGl3o1Ja/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.788838Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/transactions",  
                "email_address": "email.8@y.com",  
                "id": "ACRgJ0Um7m5DtexJqQGLkCo",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRgJ0Um7m5DtexJqQGLkCo/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T14:53:44.816199Z",  
                "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/transactions",  
                "email_address": "email.9@y.com",  
                "id": "ACRiCwAKniHQbam9iKWI1A8",  
                "credits_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts/ACRiCwAKniHQbam9iKWI1A8/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MPRb9vrx8Y62jgXaieeBu1m/accounts?limit=10&offset=0" 
    } 
 

Update an Account
-----------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~   
 
``name`` 
    *optional* **string** or **null**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. RFC-2822 formatted email address. 
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``card_uri`` 
    *optional* **string** or **null**. Tokenized card URI. 
 
``card`` 
    *optional* **object** or **null**. See `Card <./cards.rst>`_. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. Tokenized bank account URI. 
 
``bank_account`` 
    *optional* **object** or **null**. See `BankAccount <./bank_accounts.rst>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MPSLd5Rp4zNObeiGFJ5s1WA/cards/CC1d18d0d6221311e2981b80ee7316ae44",  
        "meta": { 
            "more-data": "here" 
        },  
        "email_address": "new@email.com",  
        "name": "my new name" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T14:53:47.654409Z",  
        "uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/transactions",  
        "email_address": "new@email.com",  
        "id": "ACUuwGSZ2VrDGqyBshaZXWQ",  
        "credits_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPUh6yqZhJwkGjo9SDAlK3q/accounts/ACUuwGSZ2VrDGqyBshaZXWQ/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**. See `Merchant <./merchants.rst>`_. 
 
``merchant`` 
    *optional* **object** or **null**. See `Business Merchant <./accounts.rst#create-a-business-merchant>`_ or `Person Merchant <./accounts.rst#create-a-person-merchant>`_. 
 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "merchant": { 
            "phone_number": "+19046281796",  
            "city": "San Francisco",  
            "name": "jo",  
            "dob": "1984-01",  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "person",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "444382700" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T14:53:50.482223Z",  
        "uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/transactions",  
        "email_address": "email.10@y.com",  
        "id": "ACXFIwimRmsssbPdtU8ptCA",  
        "credits_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPXtb5fFBIsFJbvQH80gPOs/accounts/ACXFIwimRmsssbPdtU8ptCA/cards" 
    } 
 

