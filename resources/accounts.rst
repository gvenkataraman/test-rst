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
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
        "card_uri": "/v1/marketplaces/TEST-MP7C7zMl3AYXZaECfMM5hFuk/cards/CCfa4b568222b211e2a07380ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T09:58:08.742071Z",  
        "uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/transactions",  
        "email_address": "b@m.com",  
        "id": "AC7DSVQscIxR9RNAL7QUE09m",  
        "credits_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7DFe6urHntM0lEC7zntYmo/accounts/AC7DSVQscIxR9RNAL7QUE09m/cards" 
    } 
 

Create a Business Merchant
--------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
                "tax_id": "585006500" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "130014800" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T09:58:11.517983Z",  
        "uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/transactions",  
        "email_address": null,  
        "id": "AC7H0uYBG6nuky0rKSSUr9A0",  
        "credits_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7GOMrCxvEIjn7aG9bj5IDW/accounts/AC7H0uYBG6nuky0rKSSUr9A0/cards" 
    } 
 

Create a Person Merchant
------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace-id)/accounts 
 

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
            "tax_id": "447055000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T09:58:14.103890Z",  
        "uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/transactions",  
        "email_address": null,  
        "id": "AC7JUPnaesA6377Rw9HfELB2",  
        "credits_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7JJpbg8tBwhXPQsaF16Upm/accounts/AC7JUPnaesA6377Rw9HfELB2/cards" 
    } 
 

Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

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
        "holds_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T09:58:15.361486Z",  
        "uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC7LkwnV1he81mJfD2mT4Cl6",  
        "credits_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP7La75V1mtJ5k0IPe8jb0uE/accounts/AC7LkwnV1he81mJfD2mT4Cl6/cards" 
    } 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace-id)/accounts 
 

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
        "first_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.457554Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC7MyVNofkhlhm095jqQGnkw",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MyVNofkhlhm095jqQGnkw/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.517998Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC7MDb3GfHZGJ5p1MdhyLyF6",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDb3GfHZGJ5p1MdhyLyF6/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.518952Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC7MDfjb19LPbb9vapQMxCcc",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MDfjb19LPbb9vapQMxCcc/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.548887Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC7MFk5WwEWqQWFDEXqzWAZe",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MFk5WwEWqQWFDEXqzWAZe/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.590993Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC7MIgMg8YSnnAWdmk1WPWTy",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIgMg8YSnnAWdmk1WPWTy/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.591779Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC7MIkwF4tiSixuHWRWOiAle",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MIkwF4tiSixuHWRWOiAle/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T09:58:16.613159Z",  
                "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC7MJOuXitwk0GKALUydVStu",  
                "credits_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts/AC7MJOuXitwk0GKALUydVStu/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP7MxdDSJQglCB8WICYqOqwc/accounts?limit=10&offset=0" 
    } 
 

Update an Account
-----------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

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
        "card_uri": "/v1/marketplaces/TEST-MPXKxQUgprJNy7lo4JksDO/cards/CC009d953622b311e2b71b80ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T09:58:19.268309Z",  
        "uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/transactions",  
        "email_address": "new@email.com",  
        "id": "AC2EUEtbGEUK41sPt7EcoRe",  
        "credits_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP2rjPEUXq7DPgu1YdJCrGI/accounts/AC2EUEtbGEUK41sPt7EcoRe/cards" 
    } 
 

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace-id)/accounts/(account-id) 
 

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
            "tax_id": "478221000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-30T09:58:21.875258Z",  
        "uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC5AHONNUt0HARDen9t6bsg",  
        "credits_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5o5hsla44XBj6pe69Uxnu/accounts/AC5AHONNUt0HARDen9t6bsg/cards" 
    } 
 

