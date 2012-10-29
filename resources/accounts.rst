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
        "card_uri": "/v1/marketplaces/TEST-MP1FUNuQaWZ54ChbATxn3Bfm/cards/CC372b0288221c11e2b4ed80ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:58:56.828574Z",  
        "uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/transactions",  
        "email_address": "b@m.com",  
        "id": "AC1HE6pfhVLbyLzhfsqInm6M",  
        "credits_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1HndcLar7guWaOFpijgq6U/accounts/AC1HE6pfhVLbyLzhfsqInm6M/cards" 
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
                "tax_id": "740568400" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "030223700" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:58:59.560822Z",  
        "uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/transactions",  
        "email_address": null,  
        "id": "AC1KIDzfKsG2rjUFO1DzcgjW",  
        "credits_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1KudLPokWfypOBGxRnNk5S/accounts/AC1KIDzfKsG2rjUFO1DzcgjW/cards" 
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
            "tax_id": "522432300" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T15:59:02.198668Z",  
        "uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/transactions",  
        "email_address": null,  
        "id": "AC1NGzSy7xw4MUbo2X71JytK",  
        "credits_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1Nt7b8SQfTUBoKskn0FOf2/accounts/AC1NGzSy7xw4MUbo2X71JytK/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:59:03.493634Z",  
        "uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC1P8T8NKjGKhpzSWvbitpWY",  
        "credits_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1OZNkNzgsG8imQRRLmAF6c/accounts/AC1P8T8NKjGKhpzSWvbitpWY/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.584090Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC1QmSxFiVBEdSmgNSl6Ih6I",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QmSxFiVBEdSmgNSl6Ih6I/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.660391Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC1QsflADURrixvLoB7XNGS0",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsflADURrixvLoB7XNGS0/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.661519Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC1QsklbVvxaZzMY2HHascoA",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QsklbVvxaZzMY2HHascoA/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.693549Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC1QuySXbcc4WhV7N51AubxG",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QuySXbcc4WhV7N51AubxG/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.740801Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC1QxR5DDIva9qbFcJJDTevO",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxR5DDIva9qbFcJJDTevO/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.741873Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC1QxVPqnVW9xZJKYIZo5GVm",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QxVPqnVW9xZJKYIZo5GVm/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T15:59:04.772790Z",  
                "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC1QA5f0xlTCPdoQXI7G0ijy",  
                "credits_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts/AC1QA5f0xlTCPdoQXI7G0ijy/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP1QkT2JbXpSjC1x5axu4UAc/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP1RTWLzAU06zONkCUQskbmA/cards/CC3d873174221c11e2962880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:59:07.441100Z",  
        "uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/transactions",  
        "email_address": "new@email.com",  
        "id": "AC1TA9AUKg6ZibMKeUOOYhsU",  
        "credits_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1ToCI3YZ40mxK9RNMKwmlS/accounts/AC1TA9AUKg6ZibMKeUOOYhsU/cards" 
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
            "tax_id": "117025400" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T15:59:10.072118Z",  
        "uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC1WxCiAch6GYw1e9eEJ4HNa",  
        "credits_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP1WmjC1c46Y726rcVqM2NDu/accounts/AC1WxCiAch6GYw1e9eEJ4HNa/cards" 
    } 
 

