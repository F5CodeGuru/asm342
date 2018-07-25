Lab 4.3: Using Python to filter json data
----------------------------------------

Task 1 - Passing parameters - server side filtering 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following script that will filter on the "python1" policy using uri parameters

.. code-block:: bash
        
        python3 /home/f5student/agility2018/python/Module4Lab3-ex1-getSingleAsmPolicyFilterUri.py

|

The output should display only the "python1" policy in json format.
Open the script and analyze it.

|

Task 2 - Using Python to filter policies via the json output - client side filtering
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following script that will filter on the "python1" policy by looping through and filtering on the json data 

.. code-block:: bash
        
        python3 /home/f5student/agility2018/python/Module4Lab3-ex1-getSingleAsmPolicyFilterLogic.py

Open the script and analyze it.

The instructor will talk through the script after all students have completed this task. Feel free to open the script to analyze it and run any of the curl commands to guide the student to the flow.

 

        
