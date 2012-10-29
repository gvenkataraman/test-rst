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
        "card_uri": "/v1/marketplaces/TEST-MP4IuLuUVhc2sd99m357Qxwg/cards/CC9b16749a21f811e293b880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:44:02.559944Z",  
        "uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/transactions",  
        "email_address": "b@m.com",  
        "id": "AC4KaidGMcNZUxPfwJZDMbLC",  
        "credits_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4JYBK1NNFYRK9dQOLxWaWM/accounts/AC4KaidGMcNZUxPfwJZDMbLC/cards" 
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
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
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
                "tax_id": "763587400" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "263208200" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T11:44:05.280066Z",  
        "uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/transactions",  
        "email_address": null,  
        "id": "AC4NdYqA8hLNA8mIOFZvIDHe",  
        "credits_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4N1GNxztKfcmd2CCHh2qMs/accounts/AC4NdYqA8hLNA8mIOFZvIDHe/cards" 
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
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
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
            "tax_id": "816161100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T11:44:07.868748Z",  
        "uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/transactions",  
        "email_address": null,  
        "id": "AC4Q8uv9oJAH6oqy1KrIZBC4",  
        "credits_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4PXvCgL2KNNunKMfXqK8LO/accounts/AC4Q8uv9oJAH6oqy1KrIZBC4/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:44:09.075556Z",  
        "uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC4RuE9XINWf5Ntq7pIdTzKY",  
        "credits_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4RmewOKwdWGUW5w2QAzU0Y/accounts/AC4RuE9XINWf5Ntq7pIdTzKY/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.161684Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC4SImH9pUdmFrTcfMG5PCIc",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SImH9pUdmFrTcfMG5PCIc/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.219569Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC4SMqAc3VKnrFGZ0l7QEHC4",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMqAc3VKnrFGZ0l7QEHC4/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.220383Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC4SMuhnyFpJZWG1VpbmzgdS",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SMuhnyFpJZWG1VpbmzgdS/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.288273Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/transactions",  
                "email_address": "email.10@y.com",  
                "id": "AC4SRcV5F77eZR3RIM0DDCio",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRcV5F77eZR3RIM0DDCio/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.289334Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC4SRhRtvX1QkdLCHoIuK2Z6",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4SRhRtvX1QkdLCHoIuK2Z6/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T11:44:10.315783Z",  
                "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/transactions",  
                "email_address": "email.13@y.com",  
                "id": "AC4ST7FHN4KarLAgIUzXtQgI",  
                "credits_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts/AC4ST7FHN4KarLAgIUzXtQgI/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP4SH3PdxiGNcMYOBOd3P1Ck/accounts?limit=10&offset=0" 
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
    *optional* **object** or **null**. See `Create a Card <./bank_accounts.rst#create-a-card>`_. 
 
``bank_account_uri`` 
    *optional* **string** or **null**. Tokenized bank account URI. 
 
``bank_account`` 
    *optional* **object** or **null**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "card_uri": "/v1/marketplaces/TEST-MP4UdPa08lNcVL1IQLBilvWA/cards/CCa152349821f811e29bb880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:44:13.016054Z",  
        "uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/transactions",  
        "email_address": "new@email.com",  
        "id": "AC4VVqhpL7SgjTs0dT7MuHWs",  
        "credits_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4VK1sKB82LfvOjoaog0UVm/accounts/AC4VVqhpL7SgjTs0dT7MuHWs/cards" 
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
    *optional* **object** or **null**. See `Create a Business Merchant <./bank_accounts.rst#create-a-business-merchant>`_ or `Create a Person Merchant <./bank_accounts.rst#create-a-person-merchant>`_. 
 
 

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
            "tax_id": "013036100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T11:44:15.642531Z",  
        "uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC4YSz9fTscIcssKL8ZAC21e",  
        "credits_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP4YJlYdOUsyBeWecPp1nRis/accounts/AC4YSz9fTscIcssKL8ZAC21e/cards" 
    } 
 

