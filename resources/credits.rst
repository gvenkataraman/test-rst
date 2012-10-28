Credits
=======

- `Credit an Account`_
- `Retrieve a Credit`_
- `List All Credits`_
- `Update a Credit`_

Fields
------

``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``amount`` 
    **integer**. Amount of the credit. 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit was created. 
 
``description`` 
    **string**. A description of the credit, used for display purposes. 
 
``account`` 
    **object**. The account to which the credit is associated. 
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 
``transaction_number`` 
    **string**. An identifier for this transaction. 
 
``available_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    credit will be available to the merchant. 
 
``fee`` 
    **integer**. The fee charged by Balanced for this credit. 
 
``destination`` 
    **object**. The funding destination for this credit (i.e., a bank account).  
 
``state`` 
    **string**. One of ``pending``, ``cleared``, ``rejected``.  
 

Credit an Account
-----------------

.. code:: 
 
    POST /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    POST /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``amount`` 
    *required* **integer**. USD cents. Must be **>=** your minimum credit amount but **<=** your maximum credit amount. 
 
``description`` 
    *optional* **string**.  
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 
``appears_on_statement_as`` 
    *optional* **string**. Text that will appear on the buyer's statement. Characters that can be 
    used are limited to: 
 
    - ASCII letters (``a-z`` and ``A-Z``) 
    - Digits (``0-9``) 
    - Special characters (``.<>(){}[]+&!$*;-%_?:#@~='" ^\`|``) 
 
    Any other characters will be rejected. Length must be **<=** ``22``. 
 
``account_uri`` 
    *optional* **string**.  
 
One of:  
    ``destination_uri`` 
        *required* **string**.  
 
    ``bank_account_uri`` 
        *required* **string**.  
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "amount": 1234, 
      "account_uri": "/v1/marketplaces/TEST-MPwePpkiVXGiUYRkJv0BMCo/accounts/ACwkuQyNtgLI4DO3WacBSS0" 
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
      "account": { 
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:33:10.105564Z", 
        "updated_at": "2012-10-28T14:33:10.105567Z", 
        "uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM", 
        "refunds_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "ACxKPabzZmrc9XihvA0wzsM", 
        "credits_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/cards" 
      }, 
      "fee": 25, 
      "description": null, 
      "amount": 1234, 
      "created_at": "2012-10-28T14:33:10.198158Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:33:10.102651Z", 
        "updated_at": "2012-10-28T14:33:10.102653Z", 
        "uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/accounts/ACxKPabzZmrc9XihvA0wzsM/bank_accounts/BAxKBXOSrrwFp5kYJ5kr3BW", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BAxKBXOSrrwFp5kYJ5kr3BW" 
      }, 
      "uri": "/v1/marketplaces/TEST-MPxF9TWtH9oxsFhVcrfEp4o/credits/CRxQJm16iPyzivsUEz1ObB2", 
      "updated_at": "2012-10-28T14:33:10.198161Z", 
      "transaction_number": "CR918-482-3881", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CRxQJm16iPyzivsUEz1ObB2", 
      "available_at": "2012-10-28T21:33:10.189630Z" 
    } 
 

Retrieve a Credit
-----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits/(credit:credit) 
    GET /v1/marketplaces/(marketplace:marketplace)/credits/(credit:credit) 
 

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
      "account": { 
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:33:11.417920Z", 
        "updated_at": "2012-10-28T14:33:11.417923Z", 
        "uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G", 
        "refunds_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "ACzekxWmVFd5d4wSN1zw67G", 
        "credits_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/cards" 
      }, 
      "fee": 25, 
      "description": "hiya", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:33:11.472034Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:33:11.414430Z", 
        "updated_at": "2012-10-28T14:33:11.414433Z", 
        "uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/accounts/ACzekxWmVFd5d4wSN1zw67G/bank_accounts/BAze4EQsXl8BmJBJxLnrcUc", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BAze4EQsXl8BmJBJxLnrcUc" 
      }, 
      "uri": "/v1/marketplaces/TEST-MPz6MYgq7yAa785XYKPDn4U/credits/CRzhzs6ja8ixSp6Q4BMdQTG", 
      "updated_at": "2012-10-28T14:33:11.472036Z", 
      "transaction_number": "CR921-263-2192", 
      "state": "cleared", 
      "meta": {}, 
      "id": "CRzhzs6ja8ixSp6Q4BMdQTG", 
      "available_at": "2012-10-28T21:33:11.458995Z" 
    } 
 

List All Credits
----------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

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
      "first_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/credits?limit=10&offset=0", 
      "items": [ 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:33:12.650104Z", 
            "updated_at": "2012-10-28T14:33:12.650106Z", 
            "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW", 
            "refunds_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "ACACgbdEI21FqwWsV1rwQHW", 
            "credits_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 1254, 
          "created_at": "2012-10-28T14:33:12.710632Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:33:12.646952Z", 
            "updated_at": "2012-10-28T14:33:12.646954Z", 
            "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/bank_accounts/BAAC26YtwSBvWkLcORGZ1Qg", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BAAC26YtwSBvWkLcORGZ1Qg" 
          }, 
          "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/credits/CRAFDPnO1BlK4HdER5IlKsc", 
          "updated_at": "2012-10-28T14:33:12.710634Z", 
          "transaction_number": "CR107-702-7912", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CRAFDPnO1BlK4HdER5IlKsc", 
          "available_at": "2012-10-28T21:33:12.692949Z" 
        }, 
        { 
          "account": { 
            "balance": 0, 
            "holds_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/holds", 
            "name": null, 
            "roles": [ 
              "merchant", 
              "buyer" 
            ], 
            "created_at": "2012-10-28T14:33:12.650104Z", 
            "updated_at": "2012-10-28T14:33:12.650106Z", 
            "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW", 
            "refunds_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/refunds", 
            "meta": {}, 
            "debits_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/debits", 
            "transactions_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/transactions", 
            "bank_accounts_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/bank_accounts", 
            "email_address": "email.7@y.com", 
            "id": "ACACgbdEI21FqwWsV1rwQHW", 
            "credits_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/credits", 
            "cards_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/cards" 
          }, 
          "fee": 25, 
          "description": "hiya", 
          "amount": 431, 
          "created_at": "2012-10-28T14:33:12.711212Z", 
          "destination": { 
            "bank_name": null, 
            "name": "Fit Finlay", 
            "bank_code": "325182797", 
            "created_at": "2012-10-28T14:33:12.646952Z", 
            "updated_at": "2012-10-28T14:33:12.646954Z", 
            "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/accounts/ACACgbdEI21FqwWsV1rwQHW/bank_accounts/BAAC26YtwSBvWkLcORGZ1Qg", 
            "is_valid": true, 
            "meta": {}, 
            "last_four": "x234", 
            "id": "BAAC26YtwSBvWkLcORGZ1Qg" 
          }, 
          "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/credits/CRAFIpfDAc0vKoQX6M8BDhO", 
          "updated_at": "2012-10-28T14:33:12.711213Z", 
          "transaction_number": "CR286-772-1951", 
          "state": "cleared", 
          "meta": {}, 
          "id": "CRAFIpfDAc0vKoQX6M8BDhO", 
          "available_at": "2012-10-28T21:33:12.698982Z" 
        } 
      ], 
      "previous_uri": null, 
      "uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/credits?limit=10&offset=0", 
      "limit": 10, 
      "offset": 0, 
      "total": 2, 
      "next_uri": null, 
      "last_uri": "/v1/marketplaces/TEST-MPAx1Vvhn5DRCrQk5enxCQI/credits?limit=10&offset=0" 
    } 
 

Update a Credit
---------------

.. code:: 
 
    GET /v1/marketplaces/(marketplace:marketplace)/accounts/(account:account)/credits 
    GET /v1/marketplaces/(marketplace:marketplace)/credits 
 

Request
~~~~~~~

``description`` 
    *optional* **string**.  
 
``meta`` 
    *optional* **object**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "description": "my new description" 
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
      "account": { 
        "balance": 0, 
        "holds_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/holds", 
        "name": null, 
        "roles": [ 
          "merchant", 
          "buyer" 
        ], 
        "created_at": "2012-10-28T14:33:15.301430Z", 
        "updated_at": "2012-10-28T14:33:15.301432Z", 
        "uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re", 
        "refunds_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/refunds", 
        "meta": {}, 
        "debits_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/debits", 
        "transactions_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/transactions", 
        "bank_accounts_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/bank_accounts", 
        "email_address": "email.7@y.com", 
        "id": "ACDB93PASCtj9eCCpnGS4Re", 
        "credits_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/credits", 
        "cards_uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/cards" 
      }, 
      "fee": 25, 
      "description": "my new description", 
      "amount": 1254, 
      "created_at": "2012-10-28T14:33:15.369830Z", 
      "destination": { 
        "bank_name": null, 
        "name": "Fit Finlay", 
        "bank_code": "325182797", 
        "created_at": "2012-10-28T14:33:15.298291Z", 
        "updated_at": "2012-10-28T14:33:15.298293Z", 
        "uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/accounts/ACDB93PASCtj9eCCpnGS4Re/bank_accounts/BADAUXYHk5tYkfIwzigydzC", 
        "is_valid": true, 
        "meta": {}, 
        "last_four": "x234", 
        "id": "BADAUXYHk5tYkfIwzigydzC" 
      }, 
      "uri": "/v1/marketplaces/TEST-MPDvvwgYgCJMm4AhzBXJade/credits/CRDEM1aF51wMubFEIgM8ktK", 
      "updated_at": "2012-10-28T14:33:15.408256Z", 
      "transaction_number": "CR910-484-6510", 
      "state": "cleared", 
      "meta": { 
        "my-id": "0987654321" 
      }, 
      "id": "CRDEM1aF51wMubFEIgM8ktK", 
      "available_at": "2012-10-28T21:33:15.347350Z" 
    } 
 

