.. include:: /globals.rst

Plugin folder organization
==========================

The directories in a FusionDirectory plugin look like this:

* |folder| `management`: management dir, used to store all management class files and related sub-classes. (Column, filter ...). 

  * |folder| `plugin_name`

* |folder| `configuration`: configuration dir, used if the plugin need to store option in ldap, also refered as backend configuration.

  * |folder| `core` : configuration files related to FusionDirectory core only.

  * |folder| `backend`: configuration files are included within the backend folder for all plugins.

    * |folder| `plugin_name`


* |folder| `dashboard`: dir containing classes related to dashboard logic, pannels, information states.

  * |folder| `plugin_name`

* |folder| `workflow`: dir containing classes related to a workflow logic, mainly combined with Orchestrator

  * |folder| `plugin_name`

* |folder| `contrib`: used to put all the contributed files like schema, docs, manpages etc..

  * |folder| `openldap`: Schemas for the openldap server
  * |folder| `docs`: Documentation how to use the plugin
  * |folder| `screenshots`: Images used to integrate with FusionDirectory marketplace.
  * |folder| `etc`: Files and information required by the plugin, such as autoloading specific data.
  * |folder| `yaml`: A yaml file describing plugins information, allowing the plugin to be automatically install via fusiondirectory-plugin-manager.

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

Management, configuration/backend, workflow, personal, dashboard
----------------------------------------------------------------

These directories should contain a subdirectory named as the plugin, or as an other plugin which we extend.
For instance, argonaut plugin contains *management/systems/argonaut/class_argonautClient.inc*

Installation of a plugin
------------------------

For **management**, **configuration/backend**, and **personal** folders, the content should go into *<fd_dir>/plugins/<dir>*/

For **html**, **ihtml**, **include**, the content should go into *<fd_dir>/<dir>*/

For **contrib/openldap**, the content should go into *<ldap_schemas_dir>/fusiondirectory*/

For **contrib/etc**, the content should go into */etc/fusiondirectory/<plugin_name>*.

For **contrib/doc**, the content may go into *<doc_dir>/fusiondirectory-plugin-<plugin_name>*.

Special cases:

  * in **html/themes/<theme_name>**, svg folder may be ignored
  * content of **locale** goes into *<fd_dir>/locale/plugins/<plugin_name>/locale*/
