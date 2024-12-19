Creating the yaml file
======================

A yaml file must be created in the root folder of your plugin named "control.yaml"

There is 3 parts:

  * information : Mandatory to define the plugin
  * support : Mandatory, content must be equal to the support provided : community is a reserved word for non-company support.
  * requirement : Optional but it's encouraged to fill it

Information
-----------

Syntax
^^^^^^

+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| keyword       | presence    | description                                                                                                             |
+===============+=============+=========================================================================================================================+
| name          | mandatory   | identifier of plugin (small string)                                                                                     |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| description   | mandatory   | description of plugin (long string)                                                                                     |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| version       | mandatory   | version of plugin (small string like X.Y)                                                                               |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| authors       | mandatory   | Array of author(s) e-mail addresses                                                                                     |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| status        | mandatory   | "Development" or "Stable"                                                                                               |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| screenshotUrl | recommended | Array of Url of screenshots files ( png/gif/jpg)                                                                        |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| logoUrl       | recommended | url to the logo file                                                                                                    |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| tags          | recommended | Array of tags used to sort the plugins in FusionDirectory market                                                        |
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| license       | mandatory   | identifier of the license used like : GPLv2                                                                             | 
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+
| origin        | mandatory   | "Source" or "Package" Package is for distribution packaging, the tools will not attempt to insttall or remove the plugin|
+---------------+-------------+-------------------------------------------------------------------------------------------------------------------------+


Example
^^^^^^^

.. code-block:: yaml

    information:
      name : notes
      description : "This plugins provide a way to add some notes per each Fusion Directory Object"
      version : "0.1"
      authors :
        - "author@domain.fr"
      status : Development
      screenshotUrl:
        - https://raw.githubusercontent.com/gallak/fusiondirectory-plugins-notes/main/contrib/doc/capture1.png
      logoUrl : "https://github.com/gallak/fusiondirectory-plugins-notes/logo.png"
      tags: ["information","notes","plugin" ]
      license: "GPLv2"
      origin: "source"

support
-------

Syntax
^^^^^^
+---------------+----------------+--------------------------------------------------------------------+
| keyword       | presence       | description                                                        |
+===============+================+====================================================================+
| provider      | mandatory      | provider of support : "community" or name of the company           |
+---------------+----------------+--------------------------------------------------------------------+
| homeUrl       | mandatory      | Link to the homepage of the plugin                                 |     
+---------------+----------------+--------------------------------------------------------------------+
| ticketUrl     | recommended    | Link to the ticket system of the plugin                            |
+---------------+----------------+--------------------------------------------------------------------+
| discussionUrl | recommended    | Link to the discussion page of the plugin                          |
+---------------+----------------+--------------------------------------------------------------------+
| downloadUrl   | mandatory      | Link to the archive of the plugin                                  |
+---------------+----------------+--------------------------------------------------------------------+
| schemaUrl     | recommended    | Link to the LDAP schema used by plugin                             |
+---------------+----------------+--------------------------------------------------------------------+
| contractUrl   | none           | Link to the company professionnal support page for FusionDirectory |
+---------------+----------------+--------------------------------------------------------------------+

Example
^^^^^^^

Community support section
^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: yaml

    support:
      provider : community
      homeUrl : "https://github.com/gallak/fusiondirectory-plugins-notes"
      ticketUrl : "https://github.com/gallak/fusiondirectory-plugins-notes/issues"
      discussionUrl : "https://github.com/gallak/fusiondirectory-plugins-notes/wiki"
      downloadUrl: "https://github.com/gallak/fusiondirectory-plugins-notes/archive/refs/heads/main.zip"
      schemaUrl : "https://schemas.fusiondirectory.org/"


Professional support section
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: yaml

    support:
      provider: fusiondirectory
      homeUrl : "https://github.com/gallak/fusiondirectory-plugins-notes"
      ticketUrl : "https://github.com/gallak/fusiondirectory-plugins-notes/issues"
      discussionUrl : "https://github.com/gallak/fusiondirectory-plugins-notes/wiki"
      downloadUrl: "https://github.com/gallak/fusiondirectory-plugins-notes/archive/refs/heads/main.zip"
      schemaUrl: "https://schemas.fusiondirectory.org/"
      contractUrl: https://www.fusiondirectory.org/abonnements-fusiondirectory/

Requirement
-----------

Syntax
^^^^^^
+------------+-----------+-----------------------------------------------------------------------------+
| keyword    | presence  | description                                                                 |
+============+===========+=============================================================================+
| fdVersion  | mandatory | Minimal version  of FusionDirectory need for this plugin (small string)     |
+------------+-----------+-----------------------------------------------------------------------------+
| phpVersion | mandatory | Minimal version  of PHP need for this plugin using semantic versionning     |
+------------+-----------+-----------------------------------------------------------------------------+
| plugins    | optionnal | List of plugins dependencies                                                |
+------------+-----------+-----------------------------------------------------------------------------+


Example
^^^^^^^

.. code-block:: yaml

    requirement:
      fdVersion : 1.4
      phpVersion : 7.2.0

