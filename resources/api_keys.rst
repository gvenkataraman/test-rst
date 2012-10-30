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
    **object**. The merchant owning this API key.See `Merchant <./merchants.rst>`_. 
 
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
        "id": "AKapmlowSuGFpckONaptZzK",  
        "created_at": "2012-10-30T09:58:26.158220Z",  
        "meta": { 
            "some": "data" 
        },  
        "secret": "0583cb4c22b311e2b37680ee7316ae44",  
        "uri": "/v1/api_keys/AKapmlowSuGFpckONaptZzK" 
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
        "created_at": "2012-10-30T09:58:27.387191Z",  
        "meta": {},  
        "id": "AKbN4wLc8gLXa87VSBSmGLG",  
        "uri": "/v1/api_keys/AKbN4wLc8gLXa87VSBSmGLG" 
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
                "id": "AKcV3GfBnsykNLqcke80Mw4",  
                "created_at": "2012-10-30T09:58:28.392626Z",  
                "meta": {},  
                "secret": "06d7dbdc22b311e2b38c80ee7316ae44",  
                "uri": "/v1/api_keys/AKcV3GfBnsykNLqcke80Mw4" 
            },  
            { 
                "created_at": "2012-10-30T09:58:28.592606Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AKd97FSRycT3qlGTEEuFW9m",  
                "id": "AKd97FSRycT3qlGTEEuFW9m" 
            },  
            { 
                "created_at": "2012-10-30T09:58:28.593878Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AKd9dFFP3zTOL0R94wpXhQM",  
                "id": "AKd9dFFP3zTOL0R94wpXhQM" 
            },  
            { 
                "created_at": "2012-10-30T09:58:28.594999Z",  
                "meta": {},  
                "uri": "/v1/api_keys/AKd9iCAUGCmcTYR4hcPEoG8",  
                "id": "AKd9iCAUGCmcTYR4hcPEoG8" 
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
        "created_at": "2012-10-30T09:58:31.153720Z",  
        "meta": { 
            "some": "different data" 
        },  
        "id": "AKg1IK1sFa6PkAS5YgyW9yk",  
        "uri": "/v1/api_keys/AKg1IK1sFa6PkAS5YgyW9yk" 
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
 

