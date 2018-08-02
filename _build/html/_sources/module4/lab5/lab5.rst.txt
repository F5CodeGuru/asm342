Lab 4.5: Adding to a policy using Python 
-------------------------------------------

Task 1 - Using Python to make whitelisted ip the same across all policies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This script uses the POST method to add the ip addresses found across all policies and adds the missing ip to each policy.
This script does not take any other settings into account other than ip and netmask. When the ip is added to the whitelist, it is added with the default settings.

Before running the script, navigate to Security->Application Security->IP Addresses->IP Address Exceptions for the "python1", "curl1" and "ansible1" policies.
Note in order to select the different policies by using the "Current edited security policy" dropdown.


.. code-block:: bash
        
        python3 /home/f5student/agility2018/asm342/python/Module4Lab5-ex1-whitelistIpNormalizer.py

|

Wait until the script is finished.

Look at the whitelist ip in Security->Application Security->IP Addresses->IP Address Exceptions  for each policy. All policies should have the exact same list of ip.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide the student to the flow.

