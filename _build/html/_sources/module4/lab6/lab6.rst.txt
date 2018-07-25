Lab 4.6: Getting data across all polciies and providing a report 
------------------------------------------------------------------

Task 1 - Using Python to report on the CVE that each policy provides protection against
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This script loops through all attack signatures installed and inventories which CVE each signatures protects against. Then it will loop through all policies, determineing if it has signatures applied to it that protect against a CVE.

Run the following script

.. code-block:: bash
        
        python3 /home/f5student/agility2018/python/Module4Lab6-ex1-getCveProtectedPerPolicy.py

|

Wait until the script is finished, this will take several minutes.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide the student to the flow.

