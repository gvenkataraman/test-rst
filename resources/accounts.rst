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
        "card_uri": "/v1/marketplaces/TEST-MP2Pr3YS1Rqbinxc3K6VSEao/cards/CC5d0e5b4021fd11e28f3580ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/holds",  
        "name": "Benny Riemann",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:18:05.934389Z",  
        "uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/transactions",  
        "email_address": "b@m.com",  
        "id": "AC2R4spKKnxVoI8X1EdSOlhy",  
        "credits_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP2QR1A92PEBGxWnwmsnxpac/accounts/AC2R4spKKnxVoI8X1EdSOlhy/cards" 
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
                "tax_id": "277665000" 
            },  
            "state": "CA",  
            "postal_code": "94110",  
            "type": "business",  
            "street_address": "Somewhere over the rainbow",  
            "tax_id": "270616700" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:18:08.709344Z",  
        "uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/transactions",  
        "email_address": null,  
        "id": "AC2UbXTFxnUoQXPUxhFWcvkg",  
        "credits_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP2TYUBBT3tyyxNAmMAozXPm/accounts/AC2UbXTFxnUoQXPUxhFWcvkg/cards" 
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
            "tax_id": "255103000" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/holds",  
        "name": "jo",  
        "roles": [ 
            "merchant" 
        ],  
        "created_at": "2012-10-29T12:18:11.288487Z",  
        "uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/transactions",  
        "email_address": null,  
        "id": "AC2X5NKaajsogoKtv2E8Vq4I",  
        "credits_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP2WSd23nuiNqogvvNscJXEg/accounts/AC2X5NKaajsogoKtv2E8Vq4I/cards" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/holds",  
        "name": null,  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:18:12.532168Z",  
        "uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC2YuxI7gsnWAHNAh9CQwg3a",  
        "credits_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP2Yjv0OpkFDpweulLovn3Io/accounts/AC2YuxI7gsnWAHNAh9CQwg3a/cards" 
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
        "first_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts?limit=10&offset=0",  
        "items": [ 
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.633990Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/transactions",  
                "email_address": "email.2@y.com",  
                "id": "AC2ZJiClCkqJlOhNeaZDumDq",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZJiClCkqJlOhNeaZDumDq/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.713712Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/transactions",  
                "email_address": "email.7@y.com",  
                "id": "AC2ZOVmjFEcNK6dxakUKUpnK",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZOVmjFEcNK6dxakUKUpnK/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.715101Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/transactions",  
                "email_address": "email.8@y.com",  
                "id": "AC2ZP1uX4ear0McG0koSWYnO",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZP1uX4ear0McG0koSWYnO/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.780291Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/transactions",  
                "email_address": "email.10@y.com",  
                "id": "AC2ZTzQa0XXEqABquAVFpQnW",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTzQa0XXEqABquAVFpQnW/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/holds",  
                "name": null,  
                "roles": [ 
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.781193Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/transactions",  
                "email_address": "email.11@y.com",  
                "id": "AC2ZTEdXYHcykfpDwN8xmr52",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZTEdXYHcykfpDwN8xmr52/cards" 
            },  
            { 
                "holds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/holds",  
                "name": null,  
                "roles": [ 
                    "merchant",  
                    "buyer" 
                ],  
                "created_at": "2012-10-29T12:18:13.806653Z",  
                "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G",  
                "bank_accounts_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/bank_accounts",  
                "refunds_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/refunds",  
                "meta": {},  
                "debits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/debits",  
                "transactions_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/transactions",  
                "email_address": "email.13@y.com",  
                "id": "AC2ZVpRNfTQn4AY68Cd4WD9G",  
                "credits_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/credits",  
                "cards_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts/AC2ZVpRNfTQn4AY68Cd4WD9G/cards" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 6,  
        "next_uri": null,  
        "last_uri": "/v1/marketplaces/TEST-MP2ZHfkRCHj2hulB8BmV1E6E/accounts?limit=10&offset=0" 
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
        "card_uri": "/v1/marketplaces/TEST-MP31f7S6D3rAJbohzEm8iBFi/cards/CC635340a621fd11e2b79880ee7316ae44",  
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
        "holds_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/holds",  
        "name": "my new name",  
        "roles": [ 
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:18:16.535472Z",  
        "uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/refunds",  
        "meta": { 
            "more-data": "here" 
        },  
        "debits_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/transactions",  
        "email_address": "new@email.com",  
        "id": "AC32ZHH15axVnauv7c7o3NqI",  
        "credits_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP32Pz4THkEtsNWPrr1M4Vus/accounts/AC32ZHH15axVnauv7c7o3NqI/cards" 
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
            "tax_id": "564200100" 
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
        "holds_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/holds",  
        "name": null,  
        "roles": [ 
            "merchant",  
            "buyer" 
        ],  
        "created_at": "2012-10-29T12:18:19.165441Z",  
        "uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm",  
        "bank_accounts_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/bank_accounts",  
        "refunds_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/refunds",  
        "meta": {},  
        "debits_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/debits",  
        "transactions_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/transactions",  
        "email_address": "email.9@y.com",  
        "id": "AC35X5RLvZ9b7yvmHNpprhnm",  
        "credits_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/credits",  
        "cards_uri": "/v1/marketplaces/TEST-MP35OxQ3SjoSxPBYEZ81FEeU/accounts/AC35X5RLvZ9b7yvmHNpprhnm/cards" 
    } 
 

