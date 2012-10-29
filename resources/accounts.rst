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
        "card_uri": "/v1/marketplaces/TEST-MP34r21KYOslYGrG2dYsecx6/cards/CC65071752221511e2926880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:10:07.290743Z",  
        "uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/transactions",  
        "email_address": "b@m.com",  
        "id": "AC36bjmJXfdRRmYNIFNxOc1S",  
        "credits_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP35UMEFoH8WjcViFUajt4I4/accounts/AC36bjmJXfdRRmYNIFNxOc1S/cards" 
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
                "tax_id": "820326200" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "075557100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:10:10.212482Z",  
        "uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/transactions",  
        "email_address": null,  
        "id": "AC39t2XtfDvas6pnQz4oXQmU",  
        "credits_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP39h2GVLTU6rofITH4ueprC/accounts/AC39t2XtfDvas6pnQz4oXQmU/cards" 
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
            "tax_id": "182180000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:10:13.016386Z",  
        "uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/transactions",  
        "email_address": null,  
        "id": "AC3cCyUDuKOcaG5Q20C7oqgc",  
        "credits_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3cnidA5krpYivaPJ7NPC1m/accounts/AC3cCyUDuKOcaG5Q20C7oqgc/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:10:14.291273Z",  
        "uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC3e3sZRGTwtf7Kvm3iy6yCo",  
        "credits_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3dR0m5N0DwKwZQU1CN0N80/accounts/AC3e3sZRGTwtf7Kvm3iy6yCo/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.612536Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC3fxBtm87FpExYBVwpT62na",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fxBtm87FpExYBVwpT62na/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.668615Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC3fBwegPpoG4L9QVjqtbo1K",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBwegPpoG4L9QVjqtbo1K/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.669726Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC3fBBjLJIsPrmjHXNJOln5q",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fBBjLJIsPrmjHXNJOln5q/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.494338Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC3fpjUFnvJwDOYikPQ52PNq",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fpjUFnvJwDOYikPQ52PNq/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.571128Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC3fuIOksfEqsRw7zYZXiJiQ",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuIOksfEqsRw7zYZXiJiQ/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.572283Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC3fuNNov3cj67x5hvABmyGM",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fuNNov3cj67x5hvABmyGM/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:10:15.701534Z",  
                "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC3fDOxvuaJN3YmZ9oCRRmTO",  
                "credits_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts/AC3fDOxvuaJN3YmZ9oCRRmTO/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP3fnkxve1SF7lr3jxHxZkig/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP3h52cKsCSzDGmLhR9BryHW/cards/CC6bba5ff0221511e2b20180ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:10:18.576823Z",  
        "uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/transactions",  
        "email_address": "new@email.com",  
        "id": "AC3iSjognnXglQfhErHa7ipC",  
        "credits_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3iEPOaNRLNg8K3GDkeIdX6/accounts/AC3iSjognnXglQfhErHa7ipC/cards" 
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
            "tax_id": "132880000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:10:21.411245Z",  
        "uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC3m3XMqOnU3sEg3wCG6IS4Q",  
        "credits_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP3lRt3J1W2MOlvqQ2BalE3i/accounts/AC3m3XMqOnU3sEg3wCG6IS4Q/cards" 
    } 
 

