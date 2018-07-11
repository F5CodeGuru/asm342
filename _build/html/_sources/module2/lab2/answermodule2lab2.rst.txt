Answer Module 2 Lab 2
======================

To get Parameters sub-collection of a policy

.. code-block:: bash

        curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/<policy id>/parameters | jq 
