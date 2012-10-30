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
        "id": "AK5FnRML3Tz6cmWXOteC6zBh",  
        "created_at": "2012-10-30T00:09:21.093932Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "ba36e1da226011e2bcfc80ee7316ae43",  
        "uri": "/v1/api_keys/AK5FnRML3Tz6cmWXOteC6zBh" 
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
        "created_at": "2012-10-30T00:09:22.272080Z",  
        "meta": {},  
        "id": "AK5GI2FoH9NPRTtzS8xeHgDF",  
        "uri": "/v1/api_keys/AK5GI2FoH9NPRTtzS8xeHgDF" 
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
                "id": "AK5HRKO88lJHhQ11WOSgOEyT",  
                "created_at": "2012-10-30T00:09:23.302289Z",  
                "meta": {},  
                "secret": "bb86fb2e226011e29a1d80ee7316ae43",  
                "uri": "/v1/api_keys/AK5HRKO88lJHhQ11WOSgOEyT" 
            },  
            { 
                "created_at": "2012-10-30T00:09:23.445642Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK5I1STxXQTWtIzZZbnQI3ZN",  
                "id": "AK5I1STxXQTWtIzZZbnQI3ZN" 
            },  
            { 
                "created_at": "2012-10-30T00:09:23.446420Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK5I1WLIQPFlMrVZh8XNKysP",  
                "id": "AK5I1WLIQPFlMrVZh8XNKysP" 
            },  
            { 
                "created_at": "2012-10-30T00:09:23.447138Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK5I1ZV8jElNuGpQFEuaoihZ",  
                "id": "AK5I1ZV8jElNuGpQFEuaoihZ" 
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
        "created_at": "2012-10-30T00:09:26.043253Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK5KX0PsnG0ykQzCqHu6ysan",  
        "uri": "/v1/api_keys/AK5KX0PsnG0ykQzCqHu6ysan" 
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
 

