Lab 4.1: Python Intro - Getting the data 
-------------------------------------------

Task 1 - Using Python to display an ASM Policy in json format
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following command to display all asm policy data in json format

.. code-block:: bash
        
        python3 /home/f5student/agility2018/python/Module4Lab1-ex1-getAllAsmPolicies.py 

|

You should see similar output to what was seen running curl (lab 2.1) and Postman (Lab 3.1) to get the configuration from policies.

|

.. note::
        If the output from the python script is all json, which in the Module4Lab1-ex1-getAllAsmPolicies.py script the output is, jq can be used to get syntax highlighting and other formatting features. To test run
       **python3 /home/f5student/agility2018/python/Module4Lab1-ex1-getAllAsmPolicies.py | jq**

|

Now double-click on the "Home" folder icon on your desktop and navigato to /home/f5student/pythong and double click on the script Module4Lab1-ex1-getAllAsmPolicies.py

|

.. image:: images/Module4Lab1-1.png
        :width: 600px

|

Notice the script is commented throughout to give the student a walk-through of what is occuring. Also note that the script has a curl command that can be used to simulate what is occuring, run the command.

|

.. note..

        Each script contains the equivalent curl commands so that the script can be debugged and to help the student understand the interaction

|

