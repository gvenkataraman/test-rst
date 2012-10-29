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
        "id": "AK34oeD0jaL8fIkq6ofoHgnG",  
        "created_at": "2012-10-29T14:55:46.704770Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "64e54b24221311e2b4f580ee7316ae44",  
        "uri": "/v1/api_keys/AK34oeD0jaL8fIkq6ofoHgnG" 
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
        "created_at": "2012-10-29T14:55:47.935690Z",  
        "meta": {},  
        "id": "AK35M5ty2nuKBvlB1Ov5QCVe",  
        "uri": "/v1/api_keys/AK35M5ty2nuKBvlB1Ov5QCVe" 
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
                "id": "AK36V4XiaZZifRROeQRk1he4",  
                "created_at": "2012-10-29T14:55:48.954706Z",  
                "meta": {},  
                "secret": "663c44dc221311e28a7580ee7316ae44",  
                "uri": "/v1/api_keys/AK36V4XiaZZifRROeQRk1he4" 
            },  
            { 
                "created_at": "2012-10-29T14:55:49.120086Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK376GsXAbP8MY3m6prSYOWg",  
                "id": "AK376GsXAbP8MY3m6prSYOWg" 
            },  
            { 
                "created_at": "2012-10-29T14:55:49.121052Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK376KWVN21nT4Sl0hoaJeeM",  
                "id": "AK376KWVN21nT4Sl0hoaJeeM" 
            },  
            { 
                "created_at": "2012-10-29T14:55:49.122046Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK376PkJKLghMJGy2tB2FOVS",  
                "id": "AK376PkJKLghMJGy2tB2FOVS" 
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
        "created_at": "2012-10-29T14:55:51.672515Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK39YFL7pQLcPXxJvLLgGSi0",  
        "uri": "/v1/api_keys/AK39YFL7pQLcPXxJvLLgGSi0" 
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
 

