.. _attributes:

Attributes Types
================

Here is a detailed description about each available attribute type for simple plugin.

StringAttribute
---------------

.. image:: /_static/images/attributes/string.png

The most simple class, allows to handle an LDAP attribute which is a string.
Specific constructor parameter :
as last parameter you can pass a pattern that the string must match in order to be valid

There are some attributes that are just like this one but with specific check for validity : MailAttribute, HostNameAttribute, IPv4Attribute, IPv6Attribute, MacAddressAttribute, IPAttribute (accepts both v4 and v6)

PasswordAttribute
-----------------

.. image:: /_static/images/attributes/password.png

Same thing as StringAttribute but input form is a hidden password input (html password input type). No specific constructor parameters

IntAttribute
------------

.. image:: /_static/images/attributes/int.png

Allow to handle an int.
Specific constructor parameters : min and max. Use "FALSE" to disable either one of them.
"intval" will be used on user input in order to convert it.
html5 "number" input type is displayed.

FloatAttribute
--------------

.. image:: /_static/images/attributes/float.png

The same that IntAttribute but for floats.
"floatval" will be used.

SelectAttribute
---------------

.. image:: /_static/images/attributes/select.png

Specific constructor attributes : an array containing the available choices.
An html select is displayed.

BooleanAttribute
----------------

.. image:: /_static/images/attributes/boolean-false.png

or

.. image:: /_static/images/attributes/boolean-true.png

Allow to handle booleans. No specific constructor parameters.
A checkbox is displayed.

ObjectClassBooleanAttribute
---------------------------

Special kind of boolean that adds or removes object classes from the object.

FileAttribute
-------------

.. image:: /_static/images/attributes/file.png

Allow the user to upload a file, store the file content in the LDAP.
If you need to do something else with the uploaded file, you'll have to inherit this class and the readFile function.

DateAttribute
-------------

.. image:: /_static/images/attributes/date1.png

Show a text input with a calendar in order for the user to choose a date.
You need to pass the wanted date format in LDAP in its constructor

BaseSelectorAttribute
---------------------

.. image:: /_static/images/attributes/base.png

Allow the user to select the base of the object.
Usually in the main tab of most objects.

ArrayAttribute and SetAttribute
-------------------------------

.. image:: /_static/images/attributes/set.png

Allow to handle a multi-valuated attribute.
The constructor takes only two parameters:

* An attribute, which is one of the above.
* An array of default values.

A multiple select will be used for displaying values, with remove and add buttons.
SetAttribute is the same, but does not allow several identical values.

CompositeAttribute
------------------

Allow to handle several UI attributes which are stored as only one LDAP field.
For instance let's say you store an FTP connection URL in an LDAP field as "ftp://user:password@host:port" but you want to display 4 inputs for the 4 parts.

.. image:: /_static/images/attributes/composite.png

That would look like :

.. code-block:: php

    <?php
    new CompositeAttribute (
      _('Informations for ftp login'),
      'ftpLoginInfo',
      [
        new StringAttribute (_('Login'),    _('Login for FTP'),     'ftpLogin'),
        new StringAttribute (_('Password'), _('Password for FTP'),  'ftpPassword'),
        new StringAttribute (_('Host'),     _('Host for FTP'),      'ftpHost'),
        new IntAttribute    (_('Port'),     _('Port for FTP'),      'ftpPort', FALSE, 0, FALSE, 21),
      ],
      'ftp://%[^@:]:%[^@:]@%[^@:]:%d', // sscanf format
      'ftp://%s:%s@%s:%d'              // sprintf format
    )

(If you need something else than scanf and printf for composition, you have to inherit CompositeAttribute in a new attribute class and write your own readValues and writeValues functions)

OrderedArrayAttribute
---------------------

This is an OrdreredArrayAttribute of CompositeAttribute (itself composed of a String and a Select attribute)

.. image:: /_static/images/attributes/orderedarray.png

Like a SetAttribute, but shows values as a table with button for removing entries and changing order.
It stores the order as "indice:value" in the LDAP.
You can pass FALSE as second parameter to disable the ordering if you just want a SetAttribute that looks different.

UsersAttribute
--------------

Allow the user to select a lists of users.
Their dn are stored in the LDAP.

A dialog is available to add users:

Before:

.. image:: /_static/images/attributes/users1.png

Selection:

.. image:: /_static/images/attributes/users2.png

After:

.. image:: /_static/images/attributes/users3.png
