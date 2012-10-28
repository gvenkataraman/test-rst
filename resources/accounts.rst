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
    *optional* **string**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
One of:  
    ``card_uri`` 
        *required* **string**. The URI of the tokenized card. 
 
    ``card`` 
        *required* **object**. See `Create a Card <./cards.rst#create-a-card>`_. 
 

Response
~~~~~~~~
     
Create a Business Merchant
--------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
One of:  
    ``bank_account_uri`` 
        *required* **string**. The URI of the bank account created via *balanced.js*. 
 
    ``bank_account`` 
        *required* **object**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
One of:  
    ``merchant_uri`` 
        *required* **string**. The URI of the merchant account created during a request for more 
        information. 
 
    ``merchant`` 
        *required* **object**. ``type`` 
            *required* **string**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string**. Date-of-birth formatted as YYYY-MM-DD. 
 
        ``person`` 
            *optional* **object**. ``name`` 
                *required* **string**.  
 
            ``dob`` 
                *required* **string**. Date-of-birth formatted as YYYY-MM-DD. 
 
            ``city`` 
                *optional* **string**. City. 
 
            One of:  
                ``region`` 
                    *required* **string**. Region (e.g. state, province, etc). This field has been 
                    **deprecated**. 
 
                ``state`` 
                    *required* **string**. US state. This field has been **deprecated**. 
 
            ``postal_code`` 
                *required* **string**. Postal code. This is known as a zip code in the USA. 
                *requires* country_code 
 
            ``street_address`` 
                *required* **string**. Street address. 
                *requires* postal_code 
 
            ``country_code`` 
                *optional* **string**. `ISO-3166-3 
                <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
                three character country code. 
 
            ``tax_id`` 
                *optional* **string**. Length must be **=** ``9``. 
 
 
        ``name`` 
            *optional* **string**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string**. City. 
 
        One of:  
            ``region`` 
                *required* **string**. Region (e.g. state, province, etc). This field has been 
                **deprecated**. 
 
            ``state`` 
                *required* **string**. US state. This field has been **deprecated**. 
 
        ``postal_code`` 
            *required* **string**. Postal code. This is known as a zip code in the USA. 
            *requires* country_code 
 
        ``street_address`` 
            *required* **string**. Street address. 
            *requires* postal_code 
 
        ``country_code`` 
            *optional* **string**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Response
~~~~~~~~


Create a Person Merchant
------------------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Request
~~~~~~~

``name`` 
    *optional* **string**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. Email address of the account. It must be **unique** among all accounts 
    on your marketplace. 
 
One of:  
    ``bank_account_uri`` 
        *required* **string**. The URI of the bank account created via *balanced.js*. 
 
    ``bank_account`` 
        *required* **object**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 
One of:  
    ``merchant_uri`` 
        *required* **string**. The URI of the merchant account created during a request for more 
        information. 
 
    ``merchant`` 
        *required* **object**. ``type`` 
            *required* **string**. Merchant type. It should be one of: ``person`` or ``business``. 
 
        ``phone_number`` 
            *required* **string**. E.164 formatted phone number. Length must be **<=** ``15``. 
 
        ``email_address`` 
            *optional* **string**. RFC-2822 formatted email address. 
 
        ``meta`` 
            *optional* **object**. Single level mapping from string keys to string values. 
 
        ``tax_id`` 
            *optional* **string**. Length must be **=** ``9``. 
 
        ``dob`` 
            *optional* **string**. Date-of-birth formatted as YYYY-MM-DD. 
 
        ``name`` 
            *optional* **string**. Length must be **<=** ``128``. 
 
        ``production`` 
            *optional* **boolean**. Flag value, should be ``true`` or ``false``. 
 
        ``city`` 
            *optional* **string**. City. 
 
        One of:  
            ``region`` 
                *required* **string**. Region (e.g. state, province, etc). This field has been 
                **deprecated**. 
 
            ``state`` 
                *required* **string**. US state. This field has been **deprecated**. 
 
        ``postal_code`` 
            *required* **string**. Postal code. This is known as a zip code in the USA. 
            *requires* country_code 
 
        ``street_address`` 
            *required* **string**. Street address. 
            *requires* postal_code 
 
        ``country_code`` 
            *optional* **string**. `ISO-3166-3 
            <http://www.iso.org/iso/home/standards/country_codes.htm#2012_iso3166-3>`_ 
            three character country code. 
 
 

Response
~~~~~~~~


Retrieve an Account
-------------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

List all Accounts
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts 
 

Update an Account
-----------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~   
 
``name`` 
    *optional* **string**. The display ``name`` of the account. Length must be **<=** ``128``. 
 
``email_address`` 
    *optional* **string**. RFC-2822 formatted email address. 
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 
One of:  
    ``card_uri`` 
        *required* **string**. Tokenized card URI. 
 
    ``card`` 
        *required* **object**. See `Create a Card <./bank_accounts.rst#create-a-card>`_. 
 
One of:  
    ``bank_account_uri`` 
        *required* **string**. Tokenized bank account URI. 
 
    ``bank_account`` 
        *required* **object**. See `Create a BankAccount <./bank_accounts.rst#create-a-bankaccount>`_. 
 

Response
~~~~~~~~

Promote a Buyer Account to a Merchant
-------------------------------------

.. code:: 
 
    PUT /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account) 
 

Request
~~~~~~~

    #. If `account` is a merchant then: 
 
    #. If `account` is not a merchant then: 
 
       One of:  
           ``merchant_uri`` 
               *required* **string**.  
 
           ``merchant`` 
               *required* **object**. See `Create a Business Merchant <./bank_accounts.rst#create-a-business-merchant>`_ or `Create a Person Merchant <./bank_accounts.rst#create-a-person-merchant>`_. 
 
 

Response
~~~~~~~~
