Errors
======

**200** OK - Item or collection retrieved successfully.

**201** Created - Item created.

**204** No Content - Item deleted.

**400** Bad Request - Request does not meet the
[API specifications](./resources.md).

**404** Not Found - Requested URI doesn't exist.

**405** Method Not Allowed - The HTTP method used is not allowed for the requested URI.

**500, 502, 503, 504** Internal Server Error - Something went wrong on Balanced's side.

Fields
------

``status_code`` 
    **string**. HTTP response code of the exception. 
 
``status`` 
    **string**.  
``additional`` 
    **string**. Any additional information that may describe how to resolve the issue. 
 
``category_type`` 
    **string**. The type of the exception. Values: ``request``, 
    ``banking``, or ``logical`` 
 
``category_code`` 
    **string**. The code of the exception. 
 
``extras`` 
    **object**. Any extra information associated with this exception. 
 
``description`` 
    **string**. Description of the exception  
 
``request_id`` 
    **string**. An ID that can be used to identify and debug the exception.  
 

Logical
-------

.. wag-error-map: logical
   :categories: logical

Banking
-------

.. wag-error-map: logical
   :categories: banking
   
Errors related to banking/payment processing.

``status_code`` 402

``category_type`` banking

``category_code``
    card-declined - Card was declined by the processor.
     
    authorization-failed - The processor did not accept this hold.
    
    funding-destination-declined - The processor did not accept the transaction.

Request
-------

.. wag-error-map: balanced_service.response.convert_exception.CLASS_TO_EXCEPTION
   :categories: request
