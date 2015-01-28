Using the Media Database
========================

For this scenario, you will need to:

1. Upload a File
----------------

**Request**:

``POST /api/v2/file``

.. code-block:: json

   {
      "folder":"840559",
      "filename":"logo.png",
      "file":"Dm++/vUMBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAcO/w4Dvv70RCO+/veKCrO+/veKCrAMBIgRAQ==..."
   }

**Response**:

.. code-block:: json

   {
     "replyCode": 0,
     "replyText": "OK",
     "data":
     [
       {
         "id": "123",
         "folder": "1",
         "filename": "md_1234.png",
         "size": "96274211",
         "original_name": "logo.png"
       }
     ]
   }

Where *filename* is the resulting file name in the media database after upload, and *original_name* is the file name
provided in the request.

See :doc:`../../suite/emails/media_file_upload`.

2. Create an Email Campaign
---------------------------

**Request**:

``POST /api/v2/email``

.. code-block:: json

   {
      "name": "new item",
      "language": "en",
      "subject": "Informing",
      "fromname": "webshop_2",
      "fromemail": "webshop_2@example.com",
      "email_category": "111111111",
      "html_source": "<html>Hello $First Name$! <img src=”/custloads/<customer_id>/img.png”>... </html>",
      "text_source": "Hello $First Name$...",
      "browse": 0,
      "text_only": 0,
      "unsubscribe": 1,
      "filter": 0,
      "contactlist": "111111111"
   }

**Response**:

.. code-block:: json

   {
     "replyCode": 0,
     "replyText": "OK",
     "data":
     {
       "id": 222222222
     }
   }

Where *id* is the new email campaign ID.

See :doc:`../../suite/emails/email_create`.

3. Launch an Email Campaign
---------------------------

**Request**:

``POST /api/v2/email/222222222/launch``

.. code-block:: json

   {
     "schedule": "2011-08-12 08:35",
     "timezone": "America/New_York"
   }


**Response**:

.. code-block:: json

   {
     "replyCode": 0,
     "replyText": "OK",
     "data": ""
   }

See :doc:`../../suite/emails/launch`.
