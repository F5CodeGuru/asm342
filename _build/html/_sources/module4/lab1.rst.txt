Lab 1.1: Ansible Policy Creation 
----------------------------------------

Ansible is an automated configuration tool that uses config files written in YAML.

Task 1 - Using Ansible to create a ASM Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the following command to create an ASM policy named **ansible1**

.. code-block:: bash
        
       ansible-playbook /etc/ansible/playbooks/ansible1.yaml -i /etc/ansible/inventory/  -vvv 

