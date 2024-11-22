.. include:: /globals.rst

Source Code management
======================

In order to contribute to the source code, you will have to know a few things about Git and the development model we follow.
You can read the CONTRIBUTING.MD in the source.

FusionDirectory source code management is handled by `GIT <https://en.wikipedia.org/wiki/Git>`_ and hosted on our own `GitLab <https://gitlab.fusiondirectory.org>`_.

A mirror is also available on `GitHub <https://github.com/fusiondirectory>`_.

Branches
--------

On the Git repository, you will  find several existing branches:

* `master` contains latest released official code,
* `dev` contains the current code in development,

The `dev` branch is where new features are added. This code is reputed as **non stable**.

The `master` branch is the released code. This code is reputed as *stable*.

There is five main repositories :

FusionDirectory
---------------

FusionDirectory web application

* `FusionDirectory Core <https://gitlab.fusiondirectory.org/fusiondirectory/fd>`_
* `FusionDirectory plugins <https://gitlab.fusiondirectory.org/fusiondirectory/fd-plugins>`_

FusionDirectory Integrator
--------------------------

FusionDirectory toolkit libraries

* `FusionDirectory Integrator <https://gitlab.fusiondirectory.org/fusiondirectory/fusiondirectory-integrator>`_

FusionDirectory Tools
---------------------

FusionDirectory set of tools for FusionDirectory and FusionDirectory Orchestrator

* `FusionDirectory Tools <https://gitlab.fusiondirectory.org/fusiondirectory/fusiondirectory-tools>`_

FusionDirectory Orchestrator
----------------------------

FusionDirectory REST Orchestrator handling the tasks 

* `FusionDirectory Orchestrator <https://gitlab.fusiondirectory.org/fusiondirectory/fusiondirectory-orchestrator>`_


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
  
  * |folder| `docs`

    * |file| `fusiondirectory-oid.pdf`: Registration of FusionDirectory oid at IANA

  * |folder| `lighttpd`
  
    * |file| `fusiondirectory-lighttpd.conf`: FusionDirectory lighttpd configuration file
  
  * |folder| `openldap` : FusionDirectory core schema
  
      * |file| `core-fd.schema`: FusionDirectory core schema
      * |file| `core-fd-conf.schema`: FusionDirectory core configuration schema
      * |file| `ldapns.schema`: LDAP Name Service Additional Schema
      * |file| `template-fd.schema`: FusionDirectory template schema
                  
  * |folder| `smarty`
  
    * |folder| `plugins`

      * |phpfile| `block.render.php`: FusionDirectory smarty block render
      * |phpfile| `function.filePath.php`: FusionDirectory smarty filepath function
      * |phpfile| `function.iconPath.php`: FusionDirectory smarty iconpath function
      * |phpfile| `function.msgPool.php`: FusionDirectory smarty message function

  * |file| `fusiondirectory.conf`: FusionDirectory configuration template

* |folder| `html`

  * |folder| `images`: static images and lists images 
  * |folder| `include`: FusionDirectory javascript libraries 
  
      * |file| `fusiondirectory.js`: FusionDirectory javascript functionalities
      * |file| `pulldow.js`: dropdown javascript class
      * |file| `pwstrength.js`: FusionDirectory password strength method based on prototype
      * |file| `tsorter.js`: list sorter javascript class
  
  * |folder| `plugins`: static image and javascript for the user photo
  
  * |folder| `themes` : FusionDirectory themes
  
    * |folder| `breezy`: default breezy theme
    
      * |phpfile| `*.css`: themes css
      * |file| `index.theme`: definition of the theme following free desktop specification
    
      * |folder| `icons`: icons for the theme following free desktop specification
      * |folder| `images`: static images for this theme if needed (not recommended)
      * |folder| `less`: FusionDirectory javascript for the theme compiled with **less**     
      * |folder| `svg`: icons in svg format
    
    
* |folder| `ihtml` : smarty theme tpl folders

  * |folder| `themes`
  
    * |folder| `breezy` : official theme
    
      * |folder| `management`: smarty templates for the management list system of FusionDirectory
      * |phpfile| `*.tpl`: smarty templates for FusionDirectory
    
* |folder| `include` : core FusionDirectory library and helpers

  * |folder| `errors`: library managing the errors in FusionDirectory
  * |folder| `exporter`: export to pdf and xls
  * |folder| `login`: all the authentification types provided by FusionDirectory
  * |folder| `management`: all object specific select dialog and methods
  * |folder| `password-methods`: all password methods understod by FusionDirectory
  * |folder| `simpleplugin`: FusionDirectory simpleplugin API
     
* |folder| `locale`

  * |folder| `ar`: ISO code of the language

    * |file| `fusiondirectory.po`: Gettext's translations
    
  * |folder| `...`
  
* |folder| `plugins`

  * |folder| `configuration` : FusionDirectory core configuration backend  
  * |folder| `dashboard`: FusionDirectory task and plugin manager dashboard
  * |folder| `generic`: References library
  * |folder| `management`: FusionDirectory classes that goes with the list management system
  * |folder| `personal` : FusionDiretory users and roles class
  * |folder| `workflow` : FusionDirectory core task and mail template 


* |file| `.gitignore`: Git ignore list
* |file| `AUTHORS.MD`: list of FusionDirectory authors
* |file| `CODE_OF_CONDUCT.MD`: FusionDirectory code of conduct
* |file| `CONTRIBUTING.MD`: How to contribute to FusionDirectory
* |file| `CHANGELOG.MD`: FusionDirectory Changelog
* |file| `Changelog`: pointing to CHANGELOG.MD
* |file| `LICENSE`: FusionDirectory licence
* |file| `README.md`: all about FusionDirectory :)
* |file| `SECURITY.md`: How to contact FusionDirectory securely for reporting security issues
* |file| `UPGRADE.md`: How to upgrade FusionDirectory
