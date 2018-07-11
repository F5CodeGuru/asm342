Lab 2.1-1 Filtering json data
------------------------------


The output yields lots of good information that can be used, the problem is there can be a lot of output. Fortunately a way to filter exists


F5 has documented a number of query parameters that can be passed into iControl ReST calls in order to modify their behavior. The first set follows the OData (open data protocol) standard. The filter parameter also supports several operators.

$filter
$select
$skip
$top
Yes, the dollar sign is important and necessary on these parameters. The operators you can use on these parameters are below. Note that the eq operator can only be used with the filter.

eq - equal
ne - not equal
lt - less than
le - less than or equal
gt - greater than
ge - greater than or equal
Logical Operators:
and
or
not
Beyond the OData parameters, there are a few custom parameters as well.

expandSubcollections - allows you to get the subcollection data in the initial request for objects that have subcollections.
options - allows you to add arguments to the tmsh equivalent command. An example will be shown below.
ver - This is for the specific TMOS version. Setting this parameter guarantees consistent behavior through code upgrades. Please note that the JSON return data for a number of calls has changed between the initial release in 11.5.0 and the current release. No items have been removed, but key/value pairs in the output have been added.

Run the following code to get just the names of the existing policies

.. note::

        expandSubcoolections does not work on ASM data, if it did one could use it instead of following the link for a subCollection in order to retrieve the data.


.. code-block:: bash

        curl -sk -u admin:password https://10.1.1.245/mgmt/tm/asm/policies/?\$select=name | sed 's/,/\'$'\n/g'

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?$select=name&ver=13.1.0"
        "totalItems":2
        "items":[{"kind":"tm:asm:policies:policystate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg?ver=13.1.0"
        "name":"ansible1"}
        {"kind":"tm:asm:policies:policystate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies/r3deT9IMy0gBkM65PTVlzA?ver=13.1.0"
        "name":"WebScrapingPolicy"}]}
|
|

.. code-block:: bash

        curl -sk -u admin:f5DEMOs4u! https://10.1.1.245/mgmt/tm/asm/policies?\$filter=name+eq+ansible1\&\$select=name | jq

.. code-block:: json

        {
        "kind": "tm:asm:policies:policycollectionstate",
        "selfLink": "https://localhost/mgmt/tm/asm/policies?$select=name&ver=13.1.0&$filter=name%20eq%20ansible1",
        "totalItems": 1,
        "items": [
                {
                "kind": "tm:asm:policies:policystate",
                "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg?ver=13.1.0",
                "name": "ansible1"
                }
                ]
        }              

