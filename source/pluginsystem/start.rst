Getting started
===============
This page is a how-to to help you write a dummy plugin.

Directory organization
----------------------

Your plugin should take place in *{fd-directory}/plugins/addons/yourpluginname* for an addon.

Plugins adding a user tab should go into *{fd-directory}/plugins/personal/yourpluginname*.

Plugins adding a system tab should go into *{fd-directory}/plugins/admin/systems/yourpluginname*.

Plugins adding a service should go into *{fd-directory}/plugins/admin/systems/services/yourpluginname*.

Your main file should be named *class_MyPluginClass.inc*.

Your plugin should have a *main.inc* file if you intend it to display on its own (not as a tab of an other object).

Icons
-----
If your plugin packs some icons, they need to be placed in the default icon theme:
*{fd-directory}/html/themes/default/icons/{size}/{category}*
Most of the time your icons are those of an application and should therefore be placed in the *apps* folder, which is for the category *applications*.
For instance if the small icon for apache goes in *{fd-directory}/html/themes/default/icons/16/apps/apache.png* and is used in the code as *geticon.php?context=applications&icon=apache&size=16*

Basic plugin writing
--------------------

This is the code for an empty plugin:

.. code-block:: php

  <?php
  class demoPlugin extends simplePlugin
  {
    // We set displayHeader to FALSE, because we don't want a header allowing to activate/deactivate this plugin,
    // we want it activated on all objects
    var $displayHeader = FALSE;

    // Here we indicate which LDAP classes our plugin is using.
    var $objectclasses = array('demoPlugin');

    // We need this function that returns some information about the plugin
    static function plInfo ()
    {
      return array(
        'plShortName'       => _('Demo Plugin'),
        'plTitle'           => _('Demo Plugin informations'),
        'plDescription'     => _('Edit some useless personal information'),
        'plSelfModify'      => TRUE, // Does this plugin have an owner that might be able to edit its entry
        'plObjectType'      => array('user'),

        // simplePlugin can generate the ACL list for us
        'plProvidedAcls'    => parent::generatePlProvidedAcls(self::getAttributesInfo())
      );
    }

    // The main function : information about attributes
    static function getAttributesInfo ()
    {
      return array(
      );
    }
  }

With this code you'll have an empty plugin, just adding the "demoPlugin" objectClass.
The [[en:documentation_dev:plInfo|plInfo]] static function must provide informations about your plugin.
Please fill **plShortName** and **plDescription** with something meaningful (and **plTitle** as well if your plugin have its own page).
See [[en:documentation_dev:plInfo|plInfo]] for more details about other fields

Attributes
----------
You might have noticed the empty getAttributesInfo method. This is where the magic happens.
You should fill this function with an array of sections containing attributes.
Available attribute types are BooleanAttribute, IntAttribute, FloatAttribute, StringAttribute, SelectAttribute, PasswordAttribute…
The names are pretty clear about what these attributes are.
There are also three special kind of attributes, SetAttribute, ArrayAttribute and CompositeAttribute.
SetAttribute and ArrayAttribute might both be used for multi-valuated attribute. Array will allow several identical values while Set won't.
A composite attribute is a unique LDAP attribute composed of several displayed attributes. You'll see one in the following example.

For more information about each type of attribute, see [[en:documentation_dev:simple_plugin_attributes|Simple Plugin Attributes]]

Example
-------

.. code-block:: php

  <?php
  // The main function : information about attributes
  static function getAttributesInfo ()
  {
    return array(
      // Attributes are grouped by section
      'section1' => array(
        'name'  => _('Hair Information'),
        'attrs' => array(
          new SetAttribute(                 // This attribute is multi-valuated
            new SelectAttribute (
              _('Color'),                     // Label of the attribute
              _('Color of the hair'),         // Description
              'hairColor',                    // LDAP name
              TRUE,                           // Mandatory
              array('blond','black','brown'), // [SelectAttribute] Choices
              "", // We don't set any default value, it will be the first one
              array('Blond','Black','Brown')  // [SelectAttribute] Output choices
            )
          ),
          new FloatAttribute  (
            _('Length'),                    // Label
            _('Length of the hair in cm'),  // Description
            'hairLength',                   // LDAP name
            FALSE,                          // Not mandatory
            0,                              // [FloatAttribute] Minimum value
            FALSE,                          // [FloatAttribute] No maximum value
            10                              // [FloatAttribute] Default value
          ),
        )
      ),
      'section2' => array(
        'name'  => _('Bicycle'),
        'attrs' => array(
          new StringAttribute (
            _('Brand'),                     // Label
            _('Brand of the bicycle'),      // Description
            'bicycleBrand',                 // LDAP name
            TRUE,                           // Mandatory
            'GreatBicycleBrand'             // Default value
          ),
          new BooleanAttribute (
            _('Has a bell'),                    // Label
            _('Does the bicycle have a bell'),  // Description
            'bicycleBell',                      // LDAP name
            FALSE,                              // Not mandatory
            FALSE                               // Default value
          ),
        )
      ),
      'ftp' => array(
        'name'  => _('FTP informations'),
        'attrs' => array(
          new CompositeAttribute (
            _('Informations for ftp login'),
            'ftpLoginInfo',
            array(
              new StringAttribute (_('Login'),    _('Login for FTP'),     'ftpLogin'),
              new StringAttribute (_('Password'), _('Password for FTP'),  'ftpPassword'),
              new StringAttribute (_('Host'),     _('Host for FTP'),      'ftpHost'),
              new IntAttribute    (_('Port'),     _('Port for FTP'),      'ftpPort', FALSE, 0, FALSE, 21),
            ),
            'ftp://%[^@:]:%[^@:]@%[^@:]:%d',    // scanf format
            'ftp://%s:%s@%s:%d'                 // printf format
          )
        )
      ),
    );
  }

As you can see, attribute constructor take 5 arguments being label, description,
ldap name, whether this attribute is mandatory or not, default value.
Some attributes takes other arguments before and after the default value.
For each section you might also specify keys 'icon' with a section icon path, or 'class' with an array of css class this section should have. (Only useful class for now is 'fullwidth' which means your section will fill the whole page width)

Displaying the plugin in FusionDirectory
----------------------------------------
Put the plugin code into a directory FusionDirectory is reading (see above).
Run <code>"fusiondirectory-setup --update-cache"</code> as root.
Log out, log in.
A tab should now show in user edition mode, with the attributes we specified:
{{:en:documentation_dev:demoplugin.png?800|}}

Displaying the plugin in the "My account" menu
----------------------------------------------
You may also want the plugin to show in the "My Account" menu, if your plugin is for users and you've set plModifySelf to TRUE.
For this, you need your plugin to have a main.inc PHP file.
Just put this in it:

.. code-block:: php

    <?php
        simplePlugin::mainInc('demoPlugin', $ui->dn);
    ?>
