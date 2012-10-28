Cards
=====

- `Tokenize a Card`_
- `Retrieve a Card`_
- `Update a Card`_

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
    ``expiration_month`` and ``expiration_year`` will have the same `hash``. 
 

Tokenize a Card
---------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/cards 
 

Request
~~~~~~~

 ``card_number`` 
     *required* **string**. The digits of the credit card number. 
  
 ``expiration_year`` 
     *required* **integer**. Expiration year. The current year or later. Value must be **<=** ``9999``. 
  
 ``expiration_month`` 
     *required* **integer**. Expiration month (e.g. 1 for January). If ``expiration_year`` is the current year then current month or later, 
     otherwise 1. Value must be **<=** ``12``. 
  
 ``security_code`` 
     *optional* **string**. The 3-4 digit security code for the card. 
  
 ``name`` 
     *optional* **string**. Length must be **<=** ``128``. 
  
 ``phone_number`` 
     *optional* **string**. E.164 formatted phone number. Length must be **<=** ``15``. 
  
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
  
 ``meta`` 
     *optional* **object**. Single level mapping from string keys to string values. 
  
 ``is_valid`` 
     *optional* **boolean**. Indicates whether the card is active (``true``) or has been deactivated 
     (``false``). 
  

Response
~~~~~~~~
 
Retrieve a Card
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/cards/(card:card) 
 

Update a Card
-------------

Request
~~~~~~~

``is_valid`` 
    *optional* **boolean**. Indicates whether the card is active (``true``) or has been deactivated 
    (``false``). Setting this to ``false`` will deactivate the card. 
 
One of:  
    ``account_uri`` 
        *required* **string**.  
 
    ``account`` 
        *required* **object**.  
        ``uri`` 
            *optional* **string**.  
 
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 

Response
~~~~~~~~
