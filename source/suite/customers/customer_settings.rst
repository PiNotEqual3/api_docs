Querying Customer Settings
==========================

Returns the current settings of the customer account (e.g. timezone, customer name, etc.).

Endpoint
--------

``GET /api/v2/settings``

Resulting Data Structure
------------------------

.. code-block:: json

   {
      "replyCode": 0,
      "replyText": "OK",
      "data":{
         "timezone": "America/New_York",
         "name": "Heimdall",
         "password_history_queue_size": 3,
         "country": "United States of America"
      }
   }

Where:

* *name* is the customer's name
* *password_history_queue_size* defines the number of the previous passwords which are no longer allowed to be used

For more information on the timezones available in Suite, see :doc:`../appendices/time_zones`.





