Lab 2.1: Intro to ASM Rest API using curl
-------------------------------------------


Task 1 - Explore the API using curl 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|

Run the following command

.. code-block:: bash

        curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies/
|

The JSON output (#1) (truncated) should look something similar to

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate","selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0","totalItems":2,"items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0","isSubCollection":true},"dataGuardReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"},"createdDatetime":"2018-05-21T04:30:17Z","databaseProtectionReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"},"csrfUrlReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0","isSubCollection":true},"cookieSettingsReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"},"versionLastChange":" Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1, username = admin, client IP = 10.1.1.51 }","name":"ansible1"

|

Not terribly easy to read, lets get something that is easier to decipher, before we get to the output, the curl options deserve some explanation.


curl **\-k** -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies/


-k: This option tell curl to not verify the server ssl certificate, since we are connected to bigip which has a cert that was signed by its own CA

|

curl -k **\-u admin:password** -X GET https://10.1.1.245/mgmt/tm/asm/policies/

-u: How the logon credentials are specified, a : is used to separate the username and passsword

|

curl -k -u admin:password **\-X GET** https://10.1.1.245/mgmt/tm/asm/policies/
-X: The HTTP method/verb, since data is being retrieved, GET is used

|

curl -k -u admin:password -X GET **https://10.1.1.245/mgmt/tm/asm/policies/**

Lastly the full url to the resource

|
|

Now run

.. code-block:: bash

       curl -sk -u admin:password -X GET https://10.1.1.245/mgmt/tm/asm/policies  | sed 's/,/\'$'\n/g'


The JSON output (#2) (truncated) is now more readable

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"
        "selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"
        "totalItems":2
        "items":[{"plainTextProfileReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/plain-text-profiles?ver=13.1.0"
        "isSubCollection":true}
        "dataGuardReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/data-guard?ver=13.1.0"}
        "createdDatetime":"2018-05-21T04:30:17Z"
        "databaseProtectionReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/database-protection?ver=13.1.0"}
        "csrfUrlReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0"
        "isSubCollection":true}
        "cookieSettingsReference":{"link":"https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/cookie-settings?ver=13.1.0"}
        "versionLastChange":" Security Policy /Common/ansible1 [add] { audit: policy = /Common/ansible1
        username = admin
        client IP = 10.1.1.51 }"
        "name":"ansible1"

 
|

Time to decipher this JSON output (#2). 

JSON is comprised of key:value pairs ({"key":"value"}) sometimes referred to as a hash or in python a dictionary. Each key/value pair belonging to a set will be enclosed in curly braces "{ .... }", "{" being the opening curly brace, "}" being the closing curly brace. Note the word "pairs", most of the JSON will have multiple pairs, each pair separated by a comma ( eg { "key1":"value1","key2":"value2"}. The commas have been removed in the above output by the sed/awk commands to make the output prettier. Take a look at the output (#1) to see the commas. In the above example, each key/value pair is on a newline thanks to the sed/awk filter. 

To access a value in a collection, a key must be specified.

Lets step through output #2 to understand that key/value pairs 

After the opening "{", is the first key of collection "kind". The value is "tm:asm:policies:policycollectionstate" which tells us we are looking the asm policies.

.. code-block:: json

        {"kind":"tm:asm:policies:policycollectionstate"

Next is the key "selfLink" and its value of "https://localhost/mgmt/tm/asm/policies?ver=13.1.0". This tells us how to get to the resource, its usefulness may not be completely apprarent now, its usefulness will be apparent in subsequent excercises.
Also take note that is essential the same url used in the curl command. The "?" is a parameter passed to request to the Rest API to use version 13.1.0 of the API. Ignore this for now.

.. code-block:: json

        "selfLink":"https://localhost/mgmt/tm/asm/policies?ver=13.1.0"


Next is "totalItems" key which has value of 2, meaning there are two policies. Go to Security->Application Security->Security Policies in Web Gui to verify the value from your output of totalItems matches the number of asm security policies from the Web Gui. 

Now the interesting stuff, The next key is "items" which is a nested collection of polciies, the actual ASM policies and their settings. Items contains multiple collections, that is why the value begins with a opening square bracket "[". The value of items contains the two ASM policies with links to their policy settings such as the link to the csrfUrlReference "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/csrf-urls?ver=13.1.0"

If you followed this url, of course substituting localhost for the mgmt ip of the BIGIP, you would get the setting for the csrf Url for that policy. That is the power of the link value, you can use that to get to other configuration items. Later in the class, we will go into how to get at this data programmatically. This also demonstrated that not all configuration data can be retrieved by a single query, depending on the need, you may have to make more than one HTTP request.

What about the crazy string "u-6T62j_f0XMkjJ_s_Z-gg" after policies/ ? This is a randomly generated (as such your value will not be u-6T62j_f0XMkjJ_s_Z-gg, rather something similar) id for the ASM security policy, in other words you cannot simply access the ansible1 security policy by going to https://10.1.1.245/mgmt/tm/asm/polciies/ansible1, you have to search for the "name" key in the JSON output until it mateches ansible1 to figure which generated id is ansible1. 

.. note:: All ASM objects which includes policies, parameters, URLS have a randomly generated unique id, where the name you see in the Web Gui is just a display name. Thereforce to get at this objects via the Rest API, you must filter on each unique ID until you find the "name" key's value equals to the name you are looking for. 

Wouldn't it be nice if we had something that could do the filtering for us?

We have covered a lot, time for questions and a discussion as these are all important topics.


