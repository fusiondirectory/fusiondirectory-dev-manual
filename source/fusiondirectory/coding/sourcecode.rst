.. include:: /globals.rst

Source Code management
======================

FusionDirectory source code management is handled by `GIT <https://en.wikipedia.org/wiki/Git>`_ and hosted on `GitHub <https://github.com/fusiondirectory>`_.

There is two repositories :

* `FusionDirectory Core <https://gitlab.fusiondirectory.org/fusiondirectory/fd>`_
* `FusionDirectory plugins <https://gitlab.fusiondirectory.org/fusiondirectory/fd-plugins>`_

In order to contribute to the source code, you will have to know a few things about Git and the development model we follow.

Branches
--------

On the Git repository, you will  find several existing branches:

* `master` contains latest released official code,
* `dev` contains the current code in development,

The `dev` branch is where new features are added. This code is reputed as **non stable**.

The `master` branch is the released code. This code is reputed as *stable*.

.. _fhs:

File Hierarchy System
---------------------

.. note::

   This lists current files and directories listed in the FusionDirectory **core** source code.

This is a brieve description of FusionDirectory core main folders and files:

* |folder| `.tx`: Transifex configuration

* |folder| `contrib`

  * |folder| `apache`
  
    * |file| `fusiondirectory-apache.conf`: FusionDirectory apache configuration

  * |folder| `bin`

    * |file| `fusiondirectory-insert-schema`: FusionDirectory console schema management tool
    * |file| `fusiondirectory-setup`: FusionDirectory console management tool
  
  * |folder| `docs`

    * |file| `README`: Global Readme
    * |file| `README.cnconfig`: Readme about openldap and cn=config
    * |file| `README.ldap-migration`: Readme about ldap migration issue when using FusionDirectory
    * |file| `UPGRADE`: Full Documentation on how to upgrade from one version to another

  * |folder| `images`

    * |file| `favicon.png`: FusionDirectory favicon in png
    * |file| `favicon.svg`: FusionDirectory favicon in svg
    * |file| `Fusiondirectory-logo-noir.eps`: FusionDirectory logo in Encapsulated Postscript
    * |file| `Fusiondirectory-logo.png`: FusionDirectory logo in png

  * |folder| `lighttpd`
  
    * |file| `fusiondirectory-lighttpd.conf`: FusionDirectory lighttpd configuration file
  
  * |folder| `man`
  * |folder| `openldap` : FusionDirectory core schema
  
  * |folder| `smarty`
  
    * |folder| `plugins`

      * |file| `block.render.php`: FusionDirectory lighttpd configuration file
      * |file| `function.filePath.php`: FusionDirectory lighttpd configuration file
      * |file| `function.iconPath.php`: FusionDirectory lighttpd configuration file
      * |file| `function.msgPool.php`: FusionDirectory lighttpd configuration file

  * |file| `fusiondirectory.conf`: FusionDirectory configuration template

* |folder| `html`

  * |folder| `images`: static images
  * |folder| `include`: static images  
  * |folder| `plugins`: static images  
  * |folder| `themes`: static images 
    
    * |phpfile| `*.css`: themes css
    
      * |folder| `icons`: icons for the theme following free desktop specification
      * |folder| `images`: static images for this theme if needed (not recommended)
      * |folder| `svg`: icons in svg format
    
    
* |folder| `ihtml` : smarty theme tpl folders

  * |folder| `themes`
  
    * |folder| `breezy` : official theme
    * |folder| `legacy` : old one for testing only 

* |folder| `include` : core FusionDirectory library and helpers

  * |folder| `exporter`: export to pdf and xls
  * |folder| `password-methods`: all password methods understod by FusionDirectory
  * |folder| `select`: all object specific select dialog and methods
  * |folder| `simpleplugin`: core FusionDirectory library
     
* |folder| `locale`

  * |folder| `ar`: ISO code of the language

    * |file| `fusiondirectory.po`: Gettext's translations
    
  * |folder| `...`
  
* |folder| `plugins`

  * |folder| `addons`
  
  * |folder| `admin`: administration plugins

  * |folder| `config`: configuration plugins

  * |folder| `generic`: base core plugins 
  
  * |folder| `personal` : base personal plugins
  
* |file| `.gitignore`: Git ignore list
* |file| `AUTHORS.txt`: list of FusionDirectory authors
* |file| `Changelog`: Changes
* |file| `COPYING`: Licence
* |file| `README.md`: all about FusionDirectory :)


.. note::

   This lists current files and directories that can be listed in the FusionDirectory **plugin** source code.

This is a brieve description of a FusionDirectory plugin folders and files:

* |folder| `addons`: used if the plugin put things in the addons menu category

* |folder| `admin`: main dir for all plugins going into the admin menu category
* |folder| `config`: configuration dir, used if the plugin need to store option in ldap
* |folder| `contrib`: used to put all the contributed files like schema, docs, manpages etc..

  * |folder| `openldap`: Schemas for the openldap server
  * |folder| `docs`: Documentation how to use the plugin

* |folder| `html`: used to put all the images or other public files

  * |folder| `plugins`

    * |folder| `plugin_name`

      * |folder| `images`: images which are not icons

  * |folder| `themes`

    * |folder| `breezy`

      * |folder| `icons`: icons to add to default breezy theme

        * |folder| `48`: sorted by size, for instance 48x48

          * |folder| `apps`: then by category, use apps for application icons

            * |file| `myapp.png`: format should be png. This example file would be used as *geticon.php?context=applications&icon=myapp*

* |folder| `ihtml`: used to put all the smarty template files

  * |folder| `themes`

    * |folder| `breezy`: smarty templates

* |folder| `locale`: used for localization of the plugin

  * |folder| `en`: language iso code

    * |file| `fusiondirectory.po`: message file

* |folder| `personal`: used when plugin is to be used to manage user properties
* |folder| `includes`: used for files available for inclusion for other plugins

