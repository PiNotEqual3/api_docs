Updating Multiple Contacts
==========================

Updates multiple contacts all at once.

.. note:: Please note that read-only fields, which are listed in System Fields, cannot be updated.

Endpoint
--------

``PUT /api/v2/contact``

Parameters
----------

.. list-table:: **Optional Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - key_id
     - mixed
     - Key which identifies the contacts
     - This can be a `field id <../../suite/appendices/system_fields.html>`_, **id** or **uid**. If left empty, the internal ID will be used by default. Value provided
       for the key_id field identifies the contact which will be updated. The other fields contain the changes requested
       for the contact. If more than one contact with the requested external ID is found, an error message is returned, [field_id]
   * - field_id
     - int
     - ID of the field, [field_value]
     -
   * - source_id
     - int
     - ID assigned to a customers external application, and is used to identify contacts created or modified by the external (3rd party) applications, [source_id] 
     -

See :doc:`contact_multiple_create` for further information.

JSON Payload Example
--------------------

.. code-block:: json

   {
     "key_id": "3",
     "contacts":
     [
       {
         "3": "erik.selvig@example.com",
         "2": "Selvig"
       },
       {
         "3": "ian.boothby@example.com",
         "2": "Boothby"
       },
       {
         "3": "james.rhodes@example.com",
         "2": "Rhodes"
       },
       {
         "3": "pepper.potts@example.com",
         "2": "Potts"
       }
     ]
   }

Result Example
--------------

.. code-block:: json

   {
      "replyCode": 0,
      "replyText": "OK",
      "data": {
         "ids": [
            "285291248",
            "285292533"
         ],
         "errors": {
            "erik.selvig@example.com": {
               "2008": "No contact found with the external id: 3 - erik.selvig@example.com"
            },
            "james.rhodes@example.com": {
               "2008": "No contact found with the external id: 3 - james.rhodes@example.com"
            }
         }
      }
   }

.. list-table:: **Result Example Details**
   :header-rows: 1
   :widths: 10 40

   * - Name
     - Description
   * - *ids*
     - List of the IDs of successfully-created contacts expressed as an array
   * - *errors*
     - List of any error(s) that occurred during the updating of a contact; the error message is returned with the value of the key_id

Errors
------

.. list-table:: Possible Error Codes
   :header-rows: 1
   :widths: 20 20 40 40

   * - HTTP Code
     - Reply Code
     - Message
     - Description
   * - 400
     - 1000
     - The request exceeded the maximum batch size 1,000
     - Too many contacts were requested; contact creation is limited to 1,000.
   * - 400
     - 2008
     - No contact found with external ID: [id] - [value].
     -