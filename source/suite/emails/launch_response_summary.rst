Querying a Response Summary
===========================

Returns the summary of the responses of a launched, paused, activated or deactivated email campaign.
Requires the use of the :doc:`launch_responses` endpoint to provide exact contact IDs.

Endpoint
--------

``GET /api/v2/email/<email_id>/responsesummary``

Parameters
----------

.. list-table:: **Required Parameters**
   :header-rows: 1
   :widths: 20 20 40 40

   * - Name
     - Type
     - Description
     - Comments
   * - email_id
     - int
     - ID of the email, part of the URI
     -

Result Example
--------------

.. code-block:: json

   {
     "replyCode": 0,
     "replyText": "OK",
     "data":
     {
       "sent": "1",
       "planned": "2",
       "soft_bounces": "3",
       "hard_bounces": "4",
       "block_bounces": "5",
       "opened": "6",
       "unsubscribe": "7",
       "total_clicks": "8",
       "unique_clicks": "9",
       "complained": "0"
     }
   }

Where:

* *sent* = The number of emails which have actually left the Suite mail servers.
* *planned* = The number of all contacts which are assigned to this launch.
* *soft_bounces* = The number of emails which were returned to sender due to temporary problems.
* *hard_bounces* = The number of emails which were returned to sender due to permanent problems.
* *block_bounces* = The number of emails which were returned to sender due to being blocked by spam filters.
* *opened* = The number of emails which were opened by recipients; the open rate refers to graphic (HTML) emails only, where the images were downloaded..
* *unsubscribe* = The number of clicks on the unsubscribe link.
* *total_clicks* = The number of total clicks on links tracked by the Suite within an email (multiple clicks per contact are counted).
* *unique_clicks* = The number of unique clicks on links tracked by the Suite within an email (one click per contact is counted).

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
     - 6400
     - Invalid email ID
     - No email with the provided ID exists.
   * - 400
     - 6003
     - Invalid email status
     - The status of the email is not one of the following: launched, paused, activated, deactivated.




