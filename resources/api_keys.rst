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
        "id": "AK21plN56EsbQHiq3XHdpmJu",  
        "created_at": "2012-10-29T15:59:14.399359Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "4275616a221c11e2bf2580ee7316ae44",  
        "uri": "/v1/api_keys/AK21plN56EsbQHiq3XHdpmJu" 
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
        "created_at": "2012-10-29T15:59:15.669268Z",  
        "meta": {},  
        "id": "AK22PVjZbkZb3SB0AGay4U8Q",  
        "uri": "/v1/api_keys/AK22PVjZbkZb3SB0AGay4U8Q" 
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
                "id": "AK246SMWx36Xhylq8z2vu9vu",  
                "created_at": "2012-10-29T15:59:16.803383Z",  
                "meta": {},  
                "secret": "43e33e82221c11e2af0e80ee7316ae44",  
                "uri": "/v1/api_keys/AK246SMWx36Xhylq8z2vu9vu" 
            },  
            { 
                "created_at": "2012-10-29T15:59:17.004249Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK24l0SGSNUWT95WGWrkzteA",  
                "id": "AK24l0SGSNUWT95WGWrkzteA" 
            },  
            { 
                "created_at": "2012-10-29T15:59:17.005350Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK24l6b3w81DIqxApmc3VLDK",  
                "id": "AK24l6b3w81DIqxApmc3VLDK" 
            },  
            { 
                "created_at": "2012-10-29T15:59:17.006389Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK24laIf9IZ1bcW0YHZHefM8",  
                "id": "AK24laIf9IZ1bcW0YHZHefM8" 
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
        "created_at": "2012-10-29T15:59:19.678833Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK27lwpjlIOemHZ9FajOXlVW",  
        "uri": "/v1/api_keys/AK27lwpjlIOemHZ9FajOXlVW" 
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
 

