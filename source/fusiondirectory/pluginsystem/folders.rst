.. include:: /globals.rst

Plugin folder organization
==========================

The directories in a FusionDirectory plugin look like this:

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

addons, admin, config, personal
-------------------------------

These directories should contain a subdirectory named as the plugin, or as an other plugin which we extend.
For instance, argonaut plugin contains *admin/systems/argonaut/class_argonautClient.inc*

Installation of a plugin
------------------------

For **addons**, **admin**, **config**, and **personal** folders, the content should go into *<fd_dir>/plugins/<dir>*/

For **html**, **ihtml**, **include**, the content should go into *<fd_dir>/<dir>*/

For **contrib/openldap**, the content should go into *<ldap_schemas_dir>/fusiondirectory*/

For **contrib/etc**, the content should go into */etc/fusiondirectory/<plugin_name>*.

For **contrib/doc**, the content may go into *<doc_dir>/fusiondirectory-plugin-<plugin_name>*.

Special cases:

  * in **html/themes/<theme_name>**, svg folder may be ignored
  * content of **locale** goes into *<fd_dir>/locale/plugins/<plugin_name>/locale*/
