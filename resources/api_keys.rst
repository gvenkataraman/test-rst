API Keys
========

- `Create an API Key`_
- `Retrieve an API Key`_
- `List all API Keys`_
- `Update an API Key`_
- `Deactivate an API Key`_


Fields
------
``id`` 
    **string**. The resource identifier. 
 
``uri`` 
    **string**. A URI for a Balanced entity 
 
``created_at`` 
    **string**. `ISO 8601 <http://www.w3.org/QA/Tips/iso-date>`_ date of when this 
    api key was created. 
 
``merchant`` 
    **object**. The merchant owning this API key. 
 
``secret`` 
    **string**. The secret associated with this API key. Will only be shown if passed 
    in the original request.  
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 

Create an API Key
-----------------

.. code:: 
 
    POST /v1/merchants/(merchant:merchant)/api_keys 
    POST /v1/api_keys 
 

Request
~~~~~~~

``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "meta": { 
            "some": "data" 
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
        "id": "AK6nrChaULjZjrR6GVsd2Zo0",  
        "created_at": "2012-10-29T15:56:04.994130Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "d1906f76221b11e294e280ee7316ae44",  
        "uri": "/v1/api_keys/AK6nrChaULjZjrR6GVsd2Zo0" 
    } 
 

Retrieve an API Key
-------------------

.. code:: 
 
    GET /v1/merchants/(merchant:merchant)/api_keys/(api_key:api_key) 
    GET /v1/api_keys/(api_key:api_key) 
 

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
        "created_at": "2012-10-29T15:56:06.216691Z",  
        "meta": {},  
        "id": "AK6oOT20MDbpia8WqgV1z81e",  
        "uri": "/v1/api_keys/AK6oOT20MDbpia8WqgV1z81e" 
    } 
 

List all API Keys
-----------------

.. code:: 
 
    GET /v1/merchants/(merchant:merchant)/api_keys 
    GET /v1/api_keys 
 

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
        "first_uri": "/v1/api_keys?limit=10&offset=0",  
        "items": [ 
            { 
                "id": "AK6pYxtPlu0PGIKW0UMtB5mQ",  
                "created_at": "2012-10-29T15:56:07.245175Z",  
                "meta": {},  
                "secret": "d2e791b0221b11e2abda80ee7316ae44",  
                "uri": "/v1/api_keys/AK6pYxtPlu0PGIKW0UMtB5mQ" 
            },  
            { 
                "created_at": "2012-10-29T15:56:07.443077Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK6qcpf8CR26HLOfes6EqQLy",  
                "id": "AK6qcpf8CR26HLOfes6EqQLy" 
            },  
            { 
                "created_at": "2012-10-29T15:56:07.444187Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK6qcuuP4dvwe9WGdXYAPKtu",  
                "id": "AK6qcuuP4dvwe9WGdXYAPKtu" 
            },  
            { 
                "created_at": "2012-10-29T15:56:07.445268Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK6qczeSqPvr9CCTtfdCkxXm",  
                "id": "AK6qczeSqPvr9CCTtfdCkxXm" 
            } 
        ],  
        "previous_uri": null,  
        "uri": "/v1/api_keys?limit=10&offset=0",  
        "limit": 10,  
        "offset": 0,  
        "total": 4,  
        "next_uri": null,  
        "last_uri": "/v1/api_keys?limit=10&offset=0" 
    } 
 

Update an API Key
-----------------

.. code:: 
 
    PUT /v1/merchants/(merchant:merchant)/api_keys/(api_key:api_key) 
    PUT /v1/api_keys/(api_key:api_key) 
 

Request
~~~~~~~
   
``meta`` 
    *optional* **object** or **null**. Single level mapping from string keys to string values. 
 

Body 
^^^^ 
 
.. code:: javascript 
 
    { 
        "meta": { 
            "some": "different data" 
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
        "created_at": "2012-10-29T15:56:10.134167Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK6te4bbXwPGYqNUWITWR0Og",  
        "uri": "/v1/api_keys/AK6te4bbXwPGYqNUWITWR0Og" 
    } 
 

Deactivate an API Key
---------------------

.. code:: 
 
    DELETE /v1/merchants/(merchant:merchant)/api_keys/(api_key:api_key) 
    DELETE /v1/api_keys/(api_key:api_key) 
 

Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 204 NO CONTENT 
 

