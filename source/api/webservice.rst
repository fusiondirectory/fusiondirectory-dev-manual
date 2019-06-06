Fusiondirectory WebService
==========================

FusionDirectory WebService plugin exposes a JSON RPC webservice that you can use if you want to access LDAP content through FusionDirectory system.
This way, you ensure that your ldap objects are kept consistent, your are able to use the system templates and have restrictions applied by acls.

On top of that you have a nicer API than the low-level LDAP one.

The `JSON RPC webservice methods are detailed here <http://api.fusiondirectory.org/classfdRPCService.html#details>`_.

.. warning::

  This API is deprecated in favour of the REST API coming in FusionDirectory 1.4.
  So i will not evolve apart from eventual bugfixes

.. warning::

  Note that you can allow HTTP in plugin configuration, but please avoid doing this except for testing purposes.

Basically you first need to call **login** to get a session ticket you’ll use in the other method calls you make.
If you have several LDAP configured you might call **listLdaps** first to list them and specify which one to use as first parameter of **login** (otherwise just pass NULL as first parameter).

Then you can use **ls** to list objects of a given type (list types with **listTypes** first if needed).
**getfields** method will give you the fields of a given type (and tab) and **setfields** will allow you to change the value of these fields.

.. code-block:: php

  <?php

  /* You can find this file in FusionDirectory include directory if argonaut plugin is installed */
  require_once('jsonRPCClient.php');

  /* Connection information. Fill peer_name with the name matching the certificate. */
  $host       = 'https://localhost/fusiondirectory/jsonrpc.php';
  $ca_file    = '/etc/ssl/certs/fd.pem';
  $login      = 'fd-admin';
  $password   = 'adminpwd';

  /* DN of an existing user we can display and modify */
  $userdn     = 'uid=bilbo,dc=opensides,dc=be';

  $ssl_options = array(
    'cafile'            => $ca_file,
    'peer_name'         => 'localhost',
    'verify_peer'       => TRUE,
    'verify_peer_name'  => TRUE,
  );

  $http_options = array(
    'timeout' => 10
  );

  try {
    /* We create the connection object */
    $client = new jsonRPCClient($host, $http_options, $ssl_options);

    /* Then we need to login. Here we log in the default LDAP */
    $session_id = $client->login(NULL, $login, $password);

    /* Once we have a session ID, we can ask for the list of users */
    $users  = $client->ls($session_id, 'user');

    foreach ($users as $dn => $user) {
      echo "$user ($dn)\n";
    }
  
    /* We can get a user’s fields */
    /* Doing the same thing with NULL as dn would create a user, if you provide all needed fields. */
    $fields = $client->getfields($session_id, 'user', $userdn);

    /* Change a value. We can pass an array for each tab, main one is 'user'. 
      The array for each tab contains attribute ids and their new value. 
      Attribute ids can be found in getfields, they are used as keys in the 'attrs' array of each section. 
    */
    $result = $client->setfields($session_id, 'user', $userdn, 
    array(
      'user' => array('description' => 'Modified by webservice')
      )
    );

    if (isset($result['errors'])) {
      foreach($result['errors'] as $error) {
        print "Error: $error\n";
      }
    }

  } catch (jsonRPCClient_RequestErrorException $e) {
    die($e->getMessage());

  } catch (jsonRPCClient_NetworkErrorException $e) {
    die($e->getMessage());
  }
