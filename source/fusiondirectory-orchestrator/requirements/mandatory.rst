Mandatory Components
====================

FusionDirectory Orchestrator is a Web application that will need:

* A webserver;
* PHP;
* An ldap server;
* Fusion Directory 1.5 with configured tasks.

Web server
----------

FusionDirectory Orchestrator requires the following web server that supports PHP and URL Rewriting:

* `Apache 2 (or more recent) <http://httpd.apache.org>`_;
* `Nginx <http://nginx.org/>`_;

PHP
---

FusionDirectory Orchestrator 1.1 works with `PHP <https://www.php.net>`_ 7.4 and PHP 8.0.

Mandatory extensions
^^^^^^^^^^^^^^^^^^^^

Following PHP extensions are required for the app to work properly:

* ``curl``: to communicate with different types of servers and protocols
* ``filter``: to filters a variable with a specified filter;
* ``json``: to get support for JSON data format;
* ``mbstring``:  to manage multi bytes characters;
* ``ldap``: to connect and query the ldap server;
* ``openssl``: secured communications and generation of secure tokens;
* ``session``: to get user sessions support;
* ``simplexml``;
* ``xml``.

LDAP server
-----------

FusionDirectory Orchestrator will use the LDAP server managed by your FusionDirectory.

Servers know to work are :

* `OpenLDAP`_

.. _OpenLDAP : https://www.openldap.org/
