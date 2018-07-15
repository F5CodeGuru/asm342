Lab 3.2: Filtering JSON data in Postman
----------------------------------------

This lab builds off of the concepts in Lab 2.1-1 Filtering json data and demonstrates how to filter json data in Postman.

Two ways exists to filter on data

- Parameters
- Postman Tests (javascript based), more background on this in Task 2


Task 1 - Filtering JSON data in Postman using parameters 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This task demonstrates how to filter on the policy named ansible1 and display only the id value.


Click on the request Module3Lab1-ex2-GetAllASMPoliciesFilteredParam

.. code-block:: rest

        
.. image:: images/module3lab2-1.png

|

Notice the parameters passed to the url https://{bigipa_host}}/mgmt/tm/asm/policies/

|

.. image:: images/module3lab2-2.png

|

How does this compare to the url parameters used in Lab2.1-1?


The special characters $, & are not escaped. 

Run the request 

.. code-block:: rest

        Module3Lab1-ex2-GetAllASMPoliciesFilteredParam

|

Take a look at the response, this is show in the “Body” (response body) section

|

.. image:: images/module3lab2-3.png

|

Is the "id" (asm policy id) displayed the same as in lab2.1-1?
It should be the same id.


Task 2 - Filtering JSON data in Postman using Tests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Postman offers the ability to programmatically ingest responses to request and make decisions on the data retrieved. Tests are written in javascript, which is a very common language, rather than some proprietary or obsucre language. Even if you are not familiar with js, there are many examples written for Postman and many examples of javascript in general. 

`Writing Postman tests <https://www.getpostman.com/docs/v6/postman/scripts/test_scripts>`_
`Tests examples <https://www.getpostman.com/docs/v6/postman/scripts/test_examples>`_

.. note::

        Note that iRules LX (iLX) and iApps LX foundations are based on javascript.

|

Tests are executed post request, which means the Test has access to the response data. In addition a test is on a per request basis, meaning they only apply to the request to which they are assigned. Though Tests can influence the flow of the next request and can be used to provide Orchestration to a collection. More on this later.

.. note:: 

       Postman also suports Pre-Request Scripts, which are executed before the Request is sent. Use cases are a dynamically generated timestamp or dynamically gnereated Post data.

       `Pre-request scripts <https://www.getpostman.com/docs/v6/postman/scripts/pre_request_scripts>`_

|

Click on the request

.. code-block:: rest

        Module3Lab1-ex3-GetAllASMPoliciesFilteredTests
        
|

Notice this request is exactly the same as Module3Lab1-ex1-GetAllASMPolicies with the exception that there is a Test assigned.


The test, examine the comments to understand how it works.

|

.. image:: images/module3lab2-4.png

|

The console.log statement logs to the javascript console, to open it click View->Show Postman Console



.. image:: images/module3lab2-5.png


|

Execute the request, then view the Postman console (it must be open before running the request to display the data).

.. code-block:: rest

        Module3Lab1-ex3-GetAllASMPoliciesFilteredTests

|

The policy id should be displayed

|

.. image:: images/module3lab2-6.png
        
