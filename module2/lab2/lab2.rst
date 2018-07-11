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

We have told jq to only display collections wihtin the items values, specifically we are specifying the first one, which is the first ASM policy.


Recall that ASM policy id are actually a random string and not the actually name, think about how one could extract the name using jq.


`Answer jq Name <answermodule2lab2-jqName.html>`_

How would one extract the enforcement mode?

`Answer jq Enforcement Mode <answermodule2lab2-jqEnforcement.html>`_




|
|
|

Next take a look at the parameter settings for this policy, run the following


.. code-block:: bash

        curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies | jq .items[0].parameterReference


The output will look somehting like

.. code-block:: json

        {
          "link": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters?ver=13.1.0",
            "isSubCollection": true
        }


|

Recall any item with a "isSubCollection" with a value of true, will have a link to the actual items
|
What would the request look like?

`Answer jq Parameters <answermodule2lab2-jqParameters.html>`_
        


What if you wanted to filter on a specific value with jq? Lets filter on the parameter with the name "displaymode"

Run the following

.. code-block:: bash

        curl -sk -u admin:password https://10.1.1.245/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters | jq '.items[] | select(.name ==  "displaymode")'


The output should look something like:

.. code-block:: json

        {
          "isBase64": false,
          "dataType": "alpha-numeric",
          "sensitiveParameter": false,
          "valueType": "user-input",
          "kind": "tm:asm:policies:parameters:parameterstate",
          "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters/_Ott1aSMBOPupVbKbovX0A?ver=13.1.0",
          "inClassification": false,
          "metacharsOnParameterValueCheck": true,
          "id": "_Ott1aSMBOPupVbKbovX0A",
          "allowEmptyValue": false,
          "checkMaxValueLength": false,
          "valueMetacharOverrides": [],
          "name": "displaymode",
          "lastUpdateMicros": 1526877023000000,
          "allowRepeatedParameterName": false,
          "level": "global",
          "attackSignaturesCheck": true,
          "signatureOverrides": [],
          "performStaging": true,
          "type": "explicit",
          "enableRegularExpression": false
         }

|
|



.. code-block:: bash

        curl -sk -u admin:bigip123 -X GET https://10.4.6.10/mgmt/tm/asm/policies | jq '.items[] | "\(.name) \(.id)"'
