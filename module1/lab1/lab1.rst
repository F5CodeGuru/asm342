Lab 1.1: Ansible Policy Creation 
----------------------------------------

Task 1 - Using Ansible to create a ASM Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create asn ASM policy using ansible

.. code-block:: bash
        
        client01# ansible-playbook createasmpolicyansible1.yaml


Go to the Bigip WebUI and navigate to Security->Application Security->Security Policies->Policies List

You should now a policy named ansible1
