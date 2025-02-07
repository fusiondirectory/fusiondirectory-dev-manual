\\FusionDirectory\\Ldap
=======================

This library aim to contain an easy to use object oriented interface to bind to an LDAP server and send requests to it.
It also contains a few helpers related to LDAP protocol.

Requirements
------------

This library needs PHP 7.3 or newer.

Installation
------------

You must put the src/FusionDirectory folder in the include_path of your PHP configuration.

Example
-------

- Connect and bind to LDAP as external

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;
    /* Open a connection */
    $ldap = new Ldap\Link('ldapi:///');

    /* External bind */
    $ldap->saslBind('', '', 'EXTERNAL');

- Connect and bind to LDAP as user

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;
    /* Open a connection */
    $ldap = new Ldap\Link('ldap://localhost:389/');
    
    /* Simple bind */
    $ldap->bind('cn=admin,dc=fusiondirectory', 'password');

- Add an entry

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;
    /* Open a connection */
    $ldap = new Ldap\Link('ldap://localhost:389/');
    
    /* Simple bind */
    $ldap->bind('cn=admin,dc=fusiondirectory', 'password');
    
    /* Add an entry */
    $add = $ldap->add(
      'ou=entry,ou=branch,dc=fusiondirectory',
      [
        'objectClass' => 'organizationalUnit',
        'ou' => 'entry'
      ]
    );

    /* Throw Ldap\Exception if the add operation returned an error */
    $add->assert();

- Delete an entry

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;
    /* Open a connection */
    $ldap = new Ldap\Link('ldap://localhost:389/');
    
    /* Simple bind */
    $ldap->bind('cn=admin,dc=fusiondirectory', 'password');
    
    /* Delete an entry */
    $delete = $ldap->delete('ou=entry,ou=branch,dc=fusiondirectory');

    /* Throw Ldap\Exception if the delete operation returned an error */
    $delete->assert();

- Make a search

.. code-block:: php

  <?php
    require 'FusionDirectory/Ldap/autoload.php';

    use \FusionDirectory\Ldap;
    /* Open a connection */
    $ldap = new Ldap\Link('ldap://localhost:389/');
    
    /* Simple bind */
    $ldap->bind('cn=admin,dc=fusiondirectory', 'password');
    
    /* Make a search */
    $list = $ldap->search('dc=fusiondirectory', '(ou=*)', ['ou'], 'subtree');

    /* Throw FusionDirectory\Ldap\Exception if there was an error */
    $list->assert();

    /* Browse results, Ldap\Result is Traversable */
    foreach ($list as $dn => $attributes) {
      echo $dn.': '.$attributes['ou'][0]."\n";
    }

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
