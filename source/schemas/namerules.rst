LDAP naming rules
=================

When naming your LDAP objectClass and/or attributes, please follow these rules:

  * Two first letter of your attribute or objectClass shoud be fd
  * After that each letter that start a new word should be in uppercase
  * Choose a meaningful name, that says what the attribute does
  * If possible choose a first word that is common for all attributes of your objectClass
  * Fill the attribute description in your LDAP schema

Also, remember to use the :ref:`ldap-number-rules`

For plugins configuration objectClass, the following scheme shoud be used:
fdNamePluginConf (for instance fdSystemsPluginConf)

Examples:

fdCyrusConnect

The description field should always start with "FusionDirectory - "

Example:

|  attributetype ( 1.3.6.1.4.1.38414.2.10.2 NAME 'fdArgonautProtocol'
|  DESC 'FusionDirectory - Argonaut, protocol.'
|  EQUALITY caseExactIA5Match
|  SYNTAX 1.3.6.1.4.1.1466.115.121.1.26
|  SINGLE-VALUE )
