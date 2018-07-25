Lab 4.5: Adding to a policy using Python 
-------------------------------------------

Task 1 - Using Python to make whitelisted ip the same across all policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This script uses the POST method to add the ip addresses found across all policies and adds the missing ip to each policy.
This script does not take any other settings into account other than ip and netmask. When the ip is added to the whitelist, it is added with the default settings

Before running the script, navigate to Security->Application Security->IP Addresses->IP Address Exceptions for both the "python1" and "ansible1" policies.
Note that select the different policies by using the "Current edited security policy" dropdown..


.. code-block:: bash
        
        python3 /home/f5student/agility2018/python/Module4Lab5-ex1-whitelistIpNormalizer.py

|

Wait until the script is finished.

Navigate to Security->Application Security->Attack Signatures, ensure the python1 policy is the "Current edited security policy"

Ensure the Staging column is set to "No" for the Attack Signatures. Looking at the first page is sufficient.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide the student to the flow.

