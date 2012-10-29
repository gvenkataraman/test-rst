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
        "card_uri": "/v1/marketplaces/TEST-MPuFgR6nfzC0Y7gbQlZhI1K/cards/CC1052026221fc11e2830880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:08:47.656942Z",  
        "uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/transactions",  
        "email_address": "b@m.com",  
        "id": "ACwecRcIC0AR6Aj24OBhXZa",  
        "credits_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPw2ClsmWj5RpEBixxtEVnu/accounts/ACwecRcIC0AR6Aj24OBhXZa/cards" 
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
                "tax_id": "632745800" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "176267400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:08:50.429557Z",  
        "uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/transactions",  
        "email_address": null,  
        "id": "ACzlxws2mRr4xte3yDzxC5K",  
        "credits_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPz7IyzrkkwgO9TuJMT5INK/accounts/ACzlxws2mRr4xte3yDzxC5K/cards" 
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
            "tax_id": "620355100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:08:53.069702Z",  
        "uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/transactions",  
        "email_address": null,  
        "id": "ACCjESTk5DdiV1nTySxBgZm",  
        "credits_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPC7FokHgSffnjivCNyOFxO/accounts/ACCjESTk5DdiV1nTySxBgZm/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:08:54.258034Z",  
        "uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/transactions",  
        "email_address": "email.9@y.com",  
        "id": "ACDEwNsMyVrKMn82ozZRCg4",  
        "credits_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPDwbF5Sj6b2G38KLCubn1y/accounts/ACDEwNsMyVrKMn82ozZRCg4/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.374417Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/transactions",  
                "email_address": "email.2@y.com",  
                "id": "ACEUk0bgta7GeBnQUsXhWfi",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACEUk0bgta7GeBnQUsXhWfi/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.455622Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/transactions",  
                "email_address": "email.7@y.com",  
                "id": "ACF01PEe60lr7GYPyHpRY3i",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF01PEe60lr7GYPyHpRY3i/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.456852Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/transactions",  
                "email_address": "email.8@y.com",  
                "id": "ACF07jgS3M0xKDGo9XRExo0",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF07jgS3M0xKDGo9XRExo0/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.528103Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/transactions",  
                "email_address": "email.10@y.com",  
                "id": "ACF56arWAC6l5jBePaxhBYw",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF56arWAC6l5jBePaxhBYw/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.528922Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/transactions",  
                "email_address": "email.11@y.com",  
                "id": "ACF59MxFNzPOsOmbnrKzIgc",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF59MxFNzPOsOmbnrKzIgc/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:08:55.551247Z",  
                "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/transactions",  
                "email_address": "email.13@y.com",  
                "id": "ACF6I59OnI7wIaSTQppjbbm",  
                "credits_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts/ACF6I59OnI7wIaSTQppjbbm/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MPESh2NIyi1oBuec5Ya0HWI/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MPGoe7JEmYoVop0trpU903O/cards/CC168b51e221fc11e2981380ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:08:58.136563Z",  
        "uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/transactions",  
        "email_address": "new@email.com",  
        "id": "ACI0YAJCzsxlTvWb2KUMIGE",  
        "credits_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPHQg5vu1av0cJNVScCkT0E/accounts/ACI0YAJCzsxlTvWb2KUMIGE/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

``merchant_uri`` 
    *optional* **string** or **null**.  
 
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
            "tax_id": "728223400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:09:00.710887Z",  
        "uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/transactions",  
        "email_address": "email.9@y.com",  
        "id": "ACKUuLAsRKx7nAdPbYAaAsY",  
        "credits_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MPKM1OzSjnBjAskp02HFVbe/accounts/ACKUuLAsRKx7nAdPbYAaAsY/cards" 
    } 
 

