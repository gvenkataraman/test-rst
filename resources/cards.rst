Cards
=====

- `Tokenize a Card`_
- `Retrieve a Card`_
- `Update a Card`_
- `Associate a Card with an Account`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. The URI of the card  
 
``account`` 
    **object**. The account this card is associated with. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this card 
    was tokenized. 
 
``street_address`` 
    **string**. Street address. 
 
``postal_code`` 
    **string**. Postal code (zip code in the USA). 
 
``country_code`` 
    **string**. `ISO-3166-3`_ three character country code. 
 
``name`` 
    **string**. The name on the card. 
 
``expiration_month`` 
    **string**. Card's expiration month. 
 
``expiration_year`` 
    **string**. Card's expiration year. 
 
``card_type`` 
    **string**. **Deprecated** 
    The type of the card. This field has been deprecated in favor of 
    ``brand``. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``last_four`` 
    **string**. Last four digits of the card. 
 
``brand`` 
    **string**. The brand of the card. One of: ``Visa``, ``MasterCard``, 
    ``American Express``, or ``Discover``.  
 
``is_valid`` 
    **boolean**. A boolean value indicating whether or not the card is valid. Once 
    invalidated, ``is_valid`` can not be set to ``true`` again. 
 
``hash`` 
    **string**. A hash derived from ``card_number``, ``expiration_month`` and 
    ``expiration_year``. Cards with the same ``card_number``, 
    ``expiration_month`` and ``expiration_year`` will have the same 
    ``hash``. 
 

Tokenize a Card
---------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/cards 
 

Request
~~~~~~~

``card_number`` 
    *required* **string** or **null**. The digits of the credit card number. 
 
``expiration_year`` 
    *required* **integer** or **null**. Expiration year. The current year or later. Value must be **<=** ``9999``. 
 
``expiration_month`` 
    *required* **integer** or **null**. Expiration month (e.g. 1 for January). If ``expiration_year`` is the current year then current month or later, 
    otherwise 1. Value must be **<=** ``12``. 
 
``security_code`` 
    *optional* **string** or **null**. The 3-4 digit security code for the card. 
 
``name`` 
    *optional* **string** or **null**. Length must be **<=** ``128``. 
 
``phone_number`` 
    *optional* **string** or **null**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
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
 
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 
``is_valid`` 
    *optional* **boolean** or **null**. Indicates whether the card is active (``true``) or has been deactivated 
    (``false``). 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "expiration_month": 4,  
        "phone_number": "+16509241212",  
        "postal_code": "10023",  
        "name": "Benny Riemann",  
        "expiration_year": 2014,  
        "country_code": "USA",  
        "security_code": 323,  
        "card_number": 5105105105105100,  
        "street_address": "167 West 74th Street" 
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
        "created_at": "2012-10-29T15:59:39.124949Z",  
        "account": null,  
        "hash": "handcock",  
        "country_code": "USA",  
        "expiration_year": 2014,  
        "brand": "American Express",  
        "uri": "/v1/marketplaces/TEST-MP2t0N1wpkUpdb7hERjZw1HC/cards/CC2tdxYeoF27IGqeljKT2EnO",  
        "expiration_month": 4,  
        "is_valid": true,  
        "meta": {},  
        "postal_code": "10023",  
        "last_four": "1111",  
        "card_type": "amex",  
        "id": "CC2tdxYeoF27IGqeljKT2EnO",  
        "street_address": "167 West 74th Street",  
        "name": "Benny Riemann" 
    } 
 

Retrieve a Card
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/cards/(card:card) 
 

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
        "created_at": "2012-10-29T15:59:40.599326Z",  
        "account": null,  
        "hash": "handcock",  
        "country_code": "USA",  
        "expiration_year": 2014,  
        "brand": "American Express",  
        "uri": "/v1/marketplaces/TEST-MP2uG3P3p7GRWxj5zsr7sv0o/cards/CC2uSlRyNzezIMUdE4CReZxO",  
        "expiration_month": 4,  
        "is_valid": true,  
        "meta": {},  
        "postal_code": "10023",  
        "last_four": "1117",  
        "card_type": "amex",  
        "id": "CC2uSlRyNzezIMUdE4CReZxO",  
        "street_address": "167 West 74th Street",  
        "name": "Benny Riemann" 
    } 
 

Update a Card
-------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/cards/(card:card) 
 

Request
~~~~~~~

``is_valid`` 
    *optional* **boolean** or **null**. Indicates whether the card is active (``true``) or has been deactivated 
    (``false``). Setting this to ``false`` will deactivate the card. 
 
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
        "card_type": "amex",  
        "account": null,  
        "hash": "handcock",  
        "name": "Benny Riemann",  
        "expiration_year": 2014,  
        "created_at": "2012-10-29T15:59:43.433109Z",  
        "brand": "American Express",  
        "uri": "/v1/marketplaces/TEST-MP2xRcIIUkaL6n5WrBeKUSOM/cards/CC2y3XxojLoDHctgXm1hzjpi",  
        "expiration_month": 4,  
        "is_valid": false,  
        "meta": {},  
        "last_four": "1111",  
        "id": "CC2y3XxojLoDHctgXm1hzjpi" 
    } 
 

Associate a Card with an Account
--------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/cards/(card:card) 
 

Request
~~~~~~~

``account_uri`` 
    *optional* **string** or **null**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "account_uri": "/v1/marketplaces/TEST-MP2zBUltby7Yfo8Kb8VSrHnu/accounts/AC2zJ9YsrNKQbnoT4BtDrM1e" 
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
        "card_type": "amex",  
        "account": { 
            "holds_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/holds",  
            "name": null,  
            "roles": [ 
                "merchant",  
                "buyer" 
            ],  
            "created_at": "2012-10-29T15:59:46.442742Z",  
            "uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y",  
            "bank_accounts_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/bank_accounts",  
            "refunds_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/refunds",  
            "meta": {},  
            "debits_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/debits",  
            "transactions_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/transactions",  
            "email_address": "email.7@y.com",  
            "id": "AC2BrQD83lYN3LGxitc2ZD6Y",  
            "credits_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/credits",  
            "cards_uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/cards" 
        },  
        "hash": "handcock",  
        "name": "Benny Riemann",  
        "expiration_year": 2014,  
        "created_at": "2012-10-29T15:59:46.519765Z",  
        "brand": "American Express",  
        "uri": "/v1/marketplaces/TEST-MP2BkvaNZ2X637RVzUkffsuo/accounts/AC2BrQD83lYN3LGxitc2ZD6Y/cards/CC2Bxccoh27cq7nyMdj7tQW0",  
        "expiration_month": 4,  
        "is_valid": true,  
        "meta": {},  
        "last_four": "1117",  
        "id": "CC2Bxccoh27cq7nyMdj7tQW0" 
    } 
 

