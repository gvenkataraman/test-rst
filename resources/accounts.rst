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
        "card_uri": "/v1/marketplaces/TEST-MP624DkfdUn1qcucANw1dqcc/cards/CCc654b3f6221b11e2af3980ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:55:47.545246Z",  
        "uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/transactions",  
        "email_address": "b@m.com",  
        "id": "AC63ORYenwarOQFVbXS2VAsk",  
        "credits_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP63y0LjKFeiiWF1oFnfbjBa/accounts/AC63ORYenwarOQFVbXS2VAsk/cards" 
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
                "tax_id": "473611400" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "760101400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:55:50.333947Z",  
        "uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/transactions",  
        "email_address": null,  
        "id": "AC66XkDNigQ1qkgvV4QDcqQQ",  
        "credits_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP66HL49qIj3ELHwEM94Rz9i/accounts/AC66XkDNigQ1qkgvV4QDcqQQ/cards" 
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
            "tax_id": "201500500" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:55:52.965238Z",  
        "uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/transactions",  
        "email_address": null,  
        "id": "AC69UOUejjcHBFbebjugrucY",  
        "credits_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP69Fn8qgRwCl81MDHNf21lG/accounts/AC69UOUejjcHBFbebjugrucY/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:55:54.218991Z",  
        "uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC6bkgb0fCGd8jo5vE9tlH8w",  
        "credits_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP6b8MtaFxHf6eC5mMzrjygA/accounts/AC6bkgb0fCGd8jo5vE9tlH8w/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.467762Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC6cJkP3qI7XHJCT4eXp3cHi",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJkP3qI7XHJCT4eXp3cHi/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.468914Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC6cJq6SPf6NteOhQ4JzOOXO",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cJq6SPf6NteOhQ4JzOOXO/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.500802Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC6cLDIKjm5gPSEpxMzJXp3e",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cLDIKjm5gPSEpxMzJXp3e/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.292308Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC6cx4eSJMqXH9ancoQFXeEA",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cx4eSJMqXH9ancoQFXeEA/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.369515Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC6cCuiEp5TtdnWCwASAMxUM",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCuiEp5TtdnWCwASAMxUM/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.370683Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC6cCzq1EaU7id1jS76T0UsI",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cCzq1EaU7id1jS76T0UsI/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:55:55.411167Z",  
                "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC6cFnXRKSBJtmN4trBfcH9W",  
                "credits_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts/AC6cFnXRKSBJtmN4trBfcH9W/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP6cviStIkpsqB7Kir1gB86U/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP6e59A65DdZoAoNUXBTvaTO/cards/CCccb5e15c221b11e28e1380ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:55:58.153094Z",  
        "uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/transactions",  
        "email_address": "new@email.com",  
        "id": "AC6fKAxP2QrYgy5hz8sycpla",  
        "credits_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP6fzDDYF0bZrN9O9ODiIVuY/accounts/AC6fKAxP2QrYgy5hz8sycpla/cards" 
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
            "tax_id": "315086700" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:56:00.732796Z",  
        "uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC6iEtV313H8xxw6oMCoxmKg",  
        "credits_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP6iuHM06by2uoEMTR5yQC8s/accounts/AC6iEtV313H8xxw6oMCoxmKg/cards" 
    } 
 

