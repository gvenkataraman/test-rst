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
    **object**. The merchant owning this API key. See `Merchant <./merchants.rst>`_. 
 
``secret`` 
    **string**. The secret associated with this API key. Will only be shown if passed 
    in the original request.  
 
``meta`` 
    **object**. A single-level dictionary of string-type key/value pairs. 
 

Create an API Key
-----------------

.. code:: 
 
    POST /v1/merchants/(merchant-id)/api_keys 
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
        "id": "AK4B4ZrYPnDTmVmvrYCMn9gU",  
        "created_at": "2012-10-30T10:09:39.867301Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "9713a7b622b411e291ef80ee7316ae44",  
        "uri": "/v1/api_keys/AK4B4ZrYPnDTmVmvrYCMn9gU" 
    } 
 

Retrieve an API Key
-------------------

.. code:: 
 
    GET /v1/merchants/(merchant-id)/api_keys/(api_key-id) 
    GET /v1/api_keys/(api_key-id) 
 

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
        "created_at": "2012-10-30T10:09:41.083732Z",  
        "meta": {},  
        "id": "AK4CrP0e6sSTCK3lt19xThoU",  
        "uri": "/v1/api_keys/AK4CrP0e6sSTCK3lt19xThoU" 
    } 
 

List all API Keys
-----------------

.. code:: 
 
    GET /v1/merchants/(merchant-id)/api_keys 
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
                "id": "AK4DD8nQNE21tBCSiXp9zPdW",  
                "created_at": "2012-10-30T10:09:42.136048Z",  
                "meta": {},  
                "secret": "986d58d222b411e2b6b480ee7316ae44",  
                "uri": "/v1/api_keys/AK4DD8nQNE21tBCSiXp9zPdW" 
            },  
            { 
                "created_at": "2012-10-30T10:09:42.336155Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK4DR9xUqjMzJNqczfrNuobW",  
                "id": "AK4DR9xUqjMzJNqczfrNuobW" 
            },  
            { 
                "created_at": "2012-10-30T10:09:42.337270Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK4DReZVlUaFF5Abi6MzuV6I",  
                "id": "AK4DReZVlUaFF5Abi6MzuV6I" 
            },  
            { 
                "created_at": "2012-10-30T10:09:42.338292Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AK4DRjys5tWGMjDddUwBh6AI",  
                "id": "AK4DRjys5tWGMjDddUwBh6AI" 
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
 
    PUT /v1/merchants/(merchant-id)/api_keys/(api_key-id) 
    PUT /v1/api_keys/(api_key-id) 
 

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
        "created_at": "2012-10-30T10:09:44.923203Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AK4GLyB9XmIxM2J0FEi3HiZu",  
        "uri": "/v1/api_keys/AK4GLyB9XmIxM2J0FEi3HiZu" 
    } 
 

Deactivate an API Key
---------------------

.. code:: 
 
    DELETE /v1/merchants/(merchant-id)/api_keys/(api_key-id) 
    DELETE /v1/api_keys/(api_key-id) 
 

Headers 
~~~~~~~ 
 
.. code::  
 
    Status: 204 NO CONTENT 
 

