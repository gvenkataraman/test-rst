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
        "card_uri": "/v1/marketplaces/TEST-MP5k8TuXVmXKeIxpu4a3cbTR/cards/CCaf0946cc226011e28f3180ee7316ae43",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T00:09:03.740033Z",  
        "uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/transactions",  
        "email_address": "b@m.com",  
        "id": "AC5lRJKYYQoAi5kztxEwoicj",  
        "credits_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5lBn1j8hYlxkr7j7bRtaIH/accounts/AC5lRJKYYQoAi5kztxEwoicj/cards" 
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
                "tax_id": "641536700" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "540062200" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T00:09:06.534175Z",  
        "uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/transactions",  
        "email_address": null,  
        "id": "AC5p0B3UD33owhoaUbCyLPID",  
        "credits_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5oLaWLMl8HqjoTiHtnEwyT/accounts/AC5p0B3UD33owhoaUbCyLPID/cards" 
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
            "tax_id": "310544600" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-30T00:09:09.064425Z",  
        "uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/transactions",  
        "email_address": null,  
        "id": "AC5rR2n1x2YUzSL2hD4eCUZJ",  
        "credits_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5rGqp5LwtSiG18l8VJqUJt/accounts/AC5rR2n1x2YUzSL2hD4eCUZJ/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T00:09:10.286644Z",  
        "uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC5teg1FmQV1d1VJk7GBkW0H",  
        "credits_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5t40oLupguSmWznLsvyQZd/accounts/AC5teg1FmQV1d1VJk7GBkW0H/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.377741Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC5uskLQn98OOClV5PiW7cI3",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uskLQn98OOClV5PiW7cI3/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.436613Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC5uwssvnpRsSshE6pwTWZTt",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwssvnpRsSshE6pwTWZTt/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.437799Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC5uwxaX1EtOCAb8vWQfFKXp",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uwxaX1EtOCAb8vWQfFKXp/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.476549Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/transactions",  
                "email_address": "email.9@y.com",  
                "id": "AC5uzeqAnZO2TDZz8OWZQf2r",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uzeqAnZO2TDZz8OWZQf2r/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.533088Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC5uDbblcjO0oFGuoEAsAAU3",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDbblcjO0oFGuoEAsAAU3/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.534239Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/transactions",  
                "email_address": "email.12@y.com",  
                "id": "AC5uDgp9iUkVcPU558xrV77J",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uDgp9iUkVcPU558xrV77J/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-30T00:09:11.565959Z",  
                "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/transactions",  
                "email_address": "email.14@y.com",  
                "id": "AC5uFtc57Kh5MwRj1IABR7XR",  
                "credits_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts/AC5uFtc57Kh5MwRj1IABR7XR/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 7,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP5uqZZHnPb2pOGo6TXSEJRV/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP5vYIxJOZY7tjDEKUyMR0ll/cards/CCb5549306226011e2830980ee7316ae43",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-30T00:09:14.281148Z",  
        "uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/transactions",  
        "email_address": "new@email.com",  
        "id": "AC5xINNMuuJ3dwBNsHLnfBIL",  
        "credits_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5xyuGyQkrHNgVnhcV9LhqX/accounts/AC5xINNMuuJ3dwBNsHLnfBIL/cards" 
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
            "tax_id": "685726300" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-30T00:09:16.886086Z",  
        "uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/transactions",  
        "email_address": "email.10@y.com",  
        "id": "AC5AEsFbrEkD8S6nR8G07uEj",  
        "credits_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP5AttzHHl17UaTVp0JAY3wT/accounts/AC5AEsFbrEkD8S6nR8G07uEj/cards" 
    } 
 

