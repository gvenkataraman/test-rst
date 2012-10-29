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
        "id": "AK3rv0zW4mHXPvQibpLjMie8",  
        "created_at": "2012-10-29T15:10:26.244818Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "712476ec221511e29d9e80ee7316ae44",  
        "uri": "/v1/api_keys/AK3rv0zW4mHXPvQibpLjMie8" 
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
        "created_at": "2012-10-29T15:10:27.554127Z",  
        "meta": {},  
        "id": "AK3sYkdVtFvsuq6nsnciLepm",  
        "uri": "/v1/api_keys/AK3sYkdVtFvsuq6nsnciLepm" 
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
                "id": "AK3ulVwhBNRnJI5lPWEc8UEQ",  
                "created_at": "2012-10-29T15:10:28.783568Z",  
                "meta": {},  
                "secret": "72a6f17a221511e2882980ee7316ae44",  
                "uri": "/v1/api_keys/AK3ulVwhBNRnJI5lPWEc8UEQ" 
            },  
            { 
                "created_at": "2012-10-29T15:10:28.983670Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK3uA0LnQtpSLjws47Ibihrm",  
                "id": "AK3uA0LnQtpSLjws47Ibihrm" 
            },  
            { 
                "created_at": "2012-10-29T15:10:28.984774Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK3uA6416c5v7u6dfPsbWUUQ",  
                "id": "AK3uA6416c5v7u6dfPsbWUUQ" 
            },  
            { 
                "created_at": "2012-10-29T15:10:28.985849Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK3uAaxZj2hKdAVc9HotHkdm",  
                "id": "AK3uAaxZj2hKdAVc9HotHkdm" 
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
        "created_at": "2012-10-29T15:10:31.908563Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK3xRYotZgU6NoUehE4I1M3i",  
        "uri": "/v1/api_keys/AK3xRYotZgU6NoUehE4I1M3i" 
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
 

