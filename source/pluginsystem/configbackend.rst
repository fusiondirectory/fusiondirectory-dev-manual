Configuration back-end
======================

If your plugin needs to have some configuration stored into the LDAP and
to appear in the configuration page accessible from the menu, you
need to create another class for the configuration backend, inside your plugin.

Class for the configuration
---------------------------

You need to create a simplePlugin inheriting class that will have the
objectType **'configuration'** if you want a whole tab for your plugin
or simply **'smallConfig'** if you have only one or two sections that can be
displayed with the other plugins in the plugins tab of the configuration.

LDAP storage for the configuration
----------------------------------

To store your configuration options into the LDAP backend you will need to write your own schema.
The options needs to have a name which starts by the prefix 'fd'.

They will be accessible in the PHP code using:

.. code-block:: php

  <?php
  $config->get_cfg_value('option_name', default_value)

With *option_name* being the option name **without** the 'fd' prefix.
