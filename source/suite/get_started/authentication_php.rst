PHP
===

.. code-block:: php

   <?php
   echo "Hello World aka Requesting the languages\n";

   /**
    * Connection data. Change with your own ones.
    */
   $username = "ani001";   // TODO change with your data
   $secret = "XXXuv21JlSHv4mM9vA";  // TODO change with your data
   $suiteApiUrl = "https://suite5.emarsys.net/api/v2/"; // TODO change with your data

   $ch = curl_init();
   curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
   curl_setopt($ch, CURLOPT_HTTPGET, 1);
   curl_setopt($ch, CURLOPT_HEADER, true);

   $requestUri = $suiteApiUrl . "language";
   curl_setopt($ch, CURLOPT_URL, $requestUri);

   /**
    * We add X-WSSE header for authentication.
    * Always use random 'nonce' for increased security.
    * timestamp: the current date/time in UTC format encoded as
    *   an ISO 8601 date string like '2010-12-31T15:30:59+00:00' or '2010-12-31T15:30:59Z'
    * passwordDigest looks sg like 'MDBhOTMwZGE0OTMxMjJlODAyNmE1ZWJhNTdmOTkxOWU4YzNjNWZkMw=='
    */
   $nonce = base64_encode(openssl_random_pseudo_bytes(16));
   $timestamp = gmdate("c");
   $passwordDigest = base64_encode(sha1($nonce . $timestamp . $secret, false));
   curl_setopt($ch,CURLOPT_HTTPHEADER, array("X-WSSE: UsernameToken ".
       "Username=\"$username\", ".
       "PasswordDigest=\"$passwordDigest\", ".
       "Nonce=\"$nonce\", ".
       "Created=\"$timestamp\""));

   $output = curl_exec($ch);
   curl_close($ch);

   echo $output;
