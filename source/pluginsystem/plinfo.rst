.. _pl-info:

plInfo
======

plInfo is a static function that must be present on all plugin classes that want to appear in FusionDirectory in one of these ways:

* In FusionDirectory main menu: use plSection
* In an object tabs: use plObjectType
* In ACL settings: use plProvidedAcls

This static method returns an array containing keys from the following table. Some may be safely omitted. Do not fill a key if you intend to use the default value for it. Use translated strings (use the _() function) for all displayable strings.

.. csv-table:: plInfo keys
   :header: key, value, used in, default

    plShortName,    "A short name for this class",  "Used in main menu and ACL summaries or such", **mandatory**
    plTitle,        "A short title for this class", "Used in FD page header at top of the page if this plugin have its own page", plShortName value
    plDescription,  "A short description",          "Used as tooltip in the menus and description in ACL management", **mandatory**
    plIcon,         "A big icon (48x48)",           "Used for main menu and header at top of the page", no icon
    plSmallIcon,    "A small icon (16x16)",         "Used in listings", "empty icon"
    plSelfModify,   "TRUE for user tabs, omitted for others", Define if it should appear in «my account» menu section for logged in users, FALSE
    plPriority,     "an integer (safe to omit most of the time)", Defines tab order and menu items order, "no prority (at the end, in no specific order)"
    plDepends,      "Array of tabs this tab depends on", Listed tabs will need to be activated before this one can be used , empty
    plCategory,     "Array of ACL categories",      Should be omitted if you’ve listed objectTypes , categories of objectTypes and managed objects
    plObjectType,   "Array of objectTypes",         See full documentation below , empty
    plSection,      "menu section key or array (see below)", See full documentation below , empty
    plProvidedAcls, "Array of acls",                See full documentation below , empty
    plForeignKeys,  "Array of foreign keys",        See full documentation below , empty
    plManages,      "Array of managed objectTypes (only for management classes)", Used to create links to objects of these types, empty

plSection
---------

**plSection** can be used if your plugin should appear in the menu. Default menu sections are "*accounts*", "*systems*", "*conf*", "*reporting*" and "*personal*".
Usually the **plSection** is set on the management class if there is any.
No need to set any **plSection** on plugins with objectType *user* and selfModify TRUE,
they'll appear in the 'My account' section anyway.

You can also create a new menu section in this attribute using the following syntax:

.. code-block:: php

    <?php
    array('mysection' => array('name' => _('My section'), 'priority' => 100))
    
Replace *mysection* with a lowercase id for your section and *My section* with the name to display in the menu.

The existing sections are:

.. csv-table:: Menu sections
   :header: key, name, priority

    accounts,   Users and groups,   0
    systems,    Systems,            10
    conf,       Configuration,      20
    reporting,  Reporting,          30
    personal,   My account,         40

So you can for instance use a priority between 0 and 10 create a section between *accounts* and *systems*.

plObjectType
------------

**plObjectType** is used to know which object type should have this plugin in its tabs.
If this tab is the main tab of a new objectType, **plObjectType** must contain the definition for this object type.

ObjectType definition is an array containing the following keys:

.. csv-table:: ObjectType properties
   :header: key, value, default

    name,           Displayable name for this object type,              **mandatory**
    description,    Displayable description for this object type,       **mandatory**
    filter,         LDAP filter to find objects of this type,           **mandatory**
    mainAttr,       LDAP attribute to use in dn,                        cn
    nameAttr,       LDAP attribute to use in object links,              *mainAttr*
    tabClass,       PHP class to use for tab handling,                  simpleTabs
    icon,           Small icon (16x16),                                 no icon
    ou,             RDN for the LDAP branch to store these objets in,   empty string
    aclCategory,    The ACL category this objectType is in,             *key*

aclCategory should be the name of an existing ACL category. Most of the time omit this and a category will automagically be created for you.

For instance, this is the plObjectType of the user class:

.. code-block:: php

  <?php
  'plObjectType'  => array(
    'user' => array(
      'description' => _('Users'),
      'name'        => _('User'),
      'filter'      => 'objectClass=gosaAccount',
      'mainAttr'    => 'cn',
      'icon'        => 'geticon.php?context=types&amp;icon=user&amp;size=16',
      'ou'          => get_ou('userRDN'),
    )
  ),

plForeignKeys
-------------

plForeignKeys is to be used if some of your fields are foreign keys to fields of other objects.
For instance the manager field in a department is a foreign key on the dn of a user.

The syntax for this is:

.. code-block:: php

  <?php
  'plForeignKeys'  => array(
    'myfield' => array(
      array('class', 'hisfield', 'filter'),
    )
  )

But you can omit *filter* most of the time (defaults to '*myfield*=%oldvalue%') and *hisfield* if it is the *dn*, and if there is only one field you are referring to you can omit the array, so for our department example this gives us:

.. code-block:: php

  <?php
  'plForeignKeys'  => array(
    'manager' => 'user'
  )

Which is pretty straight forward.

Declaring a foreignKey ensure you that:

* If the referred field is modified through FD your object will be updated as well
* If the referred object is deleted your field will be emptied if possible (or the specific value referring the object will be removed in case of multi-value attributes)
* Your objects will appear in the references tab of referenced objects

plCategory
----------

ACL categories will be filled automagically if you use either **plManages** or **plObjectType**. This is the recommanded way to go.
If you do need to specify ACL categories, you can create an acl category by specifying a descriptive array for it:

.. code-block:: php

    <?php
    'plCategory' => array(
        'acl' => array(
            'description'  => _('ACL'), 
            'objectClass'  => array('gosaAcl','gosaRole')
        )
     ),
     
An ACL category only contains a description and a list of LDAP objectClasses (for some historical reason)
