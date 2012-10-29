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
        "id": "AK1mSGtWk3VE5p3YSCncJeNS",  
        "created_at": "2012-10-29T16:48:44.843727Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "2cfb37c2222311e296a680ee7316ae44",  
        "uri": "/v1/api_keys/AK1mSGtWk3VE5p3YSCncJeNS" 
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
        "created_at": "2012-10-29T16:48:46.209944Z",  
        "meta": {},  
        "id": "AK1opXLDuUdjZFuxWznH523q",  
        "uri": "/v1/api_keys/AK1opXLDuUdjZFuxWznH523q" 
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
                "id": "AK1pFXLfQIQL3oXsmrJ0ti7i",  
                "created_at": "2012-10-29T16:48:47.329410Z",  
                "meta": {},  
                "secret": "2e75d26a222311e2bae380ee7316ae44",  
                "uri": "/v1/api_keys/AK1pFXLfQIQL3oXsmrJ0ti7i" 
            },  
            { 
                "created_at": "2012-10-29T16:48:47.483304Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK1pQLvTOf3hoAJU7Q9Y1GqU",  
                "id": "AK1pQLvTOf3hoAJU7Q9Y1GqU" 
            },  
            { 
                "created_at": "2012-10-29T16:48:47.484442Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK1pQQTCPuqwPENXi3GhiMew",  
                "id": "AK1pQQTCPuqwPENXi3GhiMew" 
            },  
            { 
                "created_at": "2012-10-29T16:48:47.485468Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK1pQVwaR0EsUdONjdfuw3Lm",  
                "id": "AK1pQVwaR0EsUdONjdfuw3Lm" 
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
        "created_at": "2012-10-29T16:48:50.197343Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK1sU1PGPYEKBsK0WFfgaT9G",  
        "uri": "/v1/api_keys/AK1sU1PGPYEKBsK0WFfgaT9G" 
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
 

