Lab 2.4: Curl Policy Creation and Modification
--------------------------------------------------

Task 1 - Using curl to create a ASM policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following command to create a new ASM policy "curl1":

.. code-block:: bash
        
        curl -sk -u admin:password -X POST https://<bigip>/mgmt/tm/asm/policies -d '{"name":"curl1"}'

|

Navigate to Security->Application Security->Security Policies->Policies List to verify the "curl1" policy was created


Before running the script, navigate to Security->Application Security->IP Addresses->IP Address Exceptions for the “curl1" policy. Note to select the different policies by using the “Current edited security policy” dropdown.

Run the following command to modify the policy by adding a whitelist ip:

.. code-block:: bash

        curl -sk -u admin:password -X POST https://<bigip>/mgmt/tm/asm/policies/<policyId>/whitelist-ips -H "Content-Type: application/json" -d '{"ipAddress":"165.25.76.234", "ipMask":"255.255.255.255"}'

|

Refresh the IP Address Exceptions to verify the whitelist ip 165.25.76.234/255.255.255.255 was added.
