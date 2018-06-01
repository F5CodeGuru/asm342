Lab 2.2: Accessing data within the JSON payload using curl 
-----------------------------------------------------

Task 1 - Using jq 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

One way to parse JSON data is to use a program called jq

Run the following command

.. code-block:: bash

       curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq 

The output (truncated) will look something similar to:

.. code-block:: json


        {
          "kind": "tm:asm:policies:policycollectionstate",
          "selfLink": "https://localhost/mgmt/tm/asm/policies?ver=13.1.0",
          "totalItems": 2,
          "items": [
            {
              "plainTextProfileReference": {
              "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0",
              "isSubCollection": true
              },
              "dataGuardReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"
              },
              "createdDatetime": "2018-05-21T04:30:17Z",
              "databaseProtectionReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"
              },
              "csrfUrlReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0",
                "isSubCollection": true
              },
              "cookieSettingsReference": {
                "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"
              },
              "versionLastChange": " Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }",
              "name": "ansible1",


jq really helps to show JSON structure and different layers, which helps to give you an idea on how to access different items.

Recall from lab1 that there are 2 items (we know this from the totalItems value, 2) and that each item represents a policy.

To display the first policy (index start at 0), run the following command

.. code-block:: bash

        curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq .items[0]

The output should look similar to:

.. code-block:: json



        {
          "plainTextProfileReference": {
            "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0",
            "isSubCollection": true
        },
          "dataGuardReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"
        },
          "createdDatetime": "2018-05-21T04:30:17Z",
          "databaseProtectionReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"
        },
          "csrfUrlReference": {
           "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0",
           "isSubCollection": true
        },
         "cookieSettingsReference": {
          "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"
        },
         "versionLastChange": " Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }",
         "name": "ansible1"

Notice the lines leading up to and including items are not displayed
 
.. code-block:: json

       {
        "kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"
        "totalItems":2 
        "items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0"

We have told jq to only display collections wihtin the items values, specifically we are specifying the first one.
