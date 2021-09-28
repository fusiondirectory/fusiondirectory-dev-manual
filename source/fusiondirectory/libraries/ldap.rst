\\FusionDirectory\\Ldap
=======================

This library aim to contain an easy to use object oriented interface to bind to an LDAP server and send requests to it.
It also contains a few helpers related to LDAP protocol.

Example
-------

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;

    /* Open a connection */
    $link = new Ldap\Link('ldapi:///');
    /* Simple bind */
    $link->bind('cn=admin,dc=base', 'password');
    /* Run a search on the server */
    $list = $link->search(
      'ou=branch,dc=base',
      "(&(objectClass=myClass)(myAttribute=*))",
      ['myAttribute'],
      'subtree'
    );
    /* Throw Ldap\Exception if the search returned an error */
    $list->assert();

    /* Iterate on search results */
    foreach ($list as $dn => $entry) {
      echo $dn.': '.$entry['myAttribute'][0]."\n";
    }
    /* Throw if there was an error while iterating */
    $list->assertIterationWentFine();

    /* Read root DSE information */
    $dse = $link->getDSE();

    /* Add an entry */
    $add = $link->add(
      'ou=entry,ou=branch,dc=base',
      [
        'objectClass' => 'organizationalUnit',
        'ou' => 'entry'
      ]
    );
    $add->assert();

Other useful helpers
--------------------

Ldap\\Schema
++++++++++++

.. code-block:: php

  <?php
    /* Parse a schema file */
    $schema = Ldap\Schema::parseSchemaFile($cn, $filepath);

    /* Parse an objectClass or attribute definition */
    $infos = Ldap\Schema::parseDefinition("attributetype ( 2.5.4.3
        NAME ( 'cn' 'commonName' )
        DESC 'RFC4519: common name(s) for which the entity is known by'
        SUP name )");
        
Ldap\\Ldif
++++++++++

.. code-block:: php

  <?php
    /* Parse an LDIF file */
    $fh = fopen('/path/to/file.ldif', 'r');
    if ($fh === FALSE) {
      die('error');
    }
    $ldifData = Ldap\Ldif::parseFromFileHandle($fh);
    if (!feof($fh)) {
      die('error');
    }
    fclose($fh);

Ldap\\GeneralizedTime
+++++++++++++++++++++

.. code-block:: php

  <?php
    /* Convert from DateTime to LDAP generalized time format */
    $ldapValue = Ldap\GeneralizedTime::toString(new DateTime('tomorrow'));

    /* And back */
    $dateTime = Ldap\GeneralizedTime::fromString($ldapValue);
