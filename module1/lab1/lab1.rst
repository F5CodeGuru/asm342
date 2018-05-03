Lab 1.1: Ansible Policy Creation 
----------------------------------------

Task 1 - Using Ansible to create a ASM Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following command to create an ASM policy named ansible1

.. code-block:: bash
        
        client01# ansible-playbook createasmpolicyansible1.yaml


Go to the Bigip WebUI and navigate to Security->Application Security->Security Policies->Policies List

You should now see a policy named ansible1

Inspect the policy
