.. _ldap-number-rules:

LDAP number rules
=================

This page is here to help you choose ID numbers for your attributeTypes objectClasses in your schemas.
FusionDirectory project has '1.3.6.1.4.1.38414' prefix.
There are three number after this prefix :

#. The first one should be the one attributed to your schema
#. The second one should start by 1 for attributeTypes and 2 for objectClasses
#. The third one should be incremented for each attributeType or objectClass

The important thing is the first one, the two others are up to you, these are just advices and rules we use in FD schemas.

Example
-------

  * attribueType 1.3.6.1.4.1.38414.\ **42.1.1**
  * attribueType 1.3.6.1.4.1.38414.\ **42.1.2**
  * attribueType 1.3.6.1.4.1.38414.\ **42.1.3**
  * objectClass 1.3.6.1.4.1.38414.\ **42.2.1**
  * objectClass 1.3.6.1.4.1.38414.\ **42.2.2**

Or, if you have two groups of attributeTypes that are somehow related:

  * attribueType 1.3.6.1.4.1.38414.\ **42.10.1**
  * attribueType 1.3.6.1.4.1.38414.\ **42.10.2**
  * attribueType 1.3.6.1.4.1.38414.\ **42.11.1**
  * attribueType 1.3.6.1.4.1.38414.\ **42.11.2**
  * objectClass 1.3.6.1.4.1.38414.\ **42.2.1**
  * objectClass 1.3.6.1.4.1.38414.\ **42.2.2**

Attribution
-----------
===================================== =====================
Schema                                Number attributed
===================================== =====================
recovery-fd.schema                    1
argonaut-fd.schema                    2
quota-fd.schema                       3
debconf-fd.schema                     4
zimbra-fd.schema                      5
goto.schema                           6
puppet-fd.schema                      7
core-fd-conf.schema                   8
samba-fd-conf.schema                  9
mail-fd.schema, mail-fd-conf.schema   10
alias-fd.schema, alias-fd-conf.schema 11
sympa-fd.schema                       12
dsa-fd-conf.schema                    13
cyrus-fd.schema                       14
systems-fd.schema                     16
supann-fd-conf.schema                 17
system-fd-conf.schema                 18
asterisk-fd-conf.schema               19
opsi-fd.schema                        20
opsi-fd-conf.schema                   21
netgroup-fd-conf.schema               22
sudo-fd-conf.schema                   23
fax-fd-conf.schema                    24
fai-fd-conf.schema                    25
nagios-fd-conf.schema                 26
board-fd-conf.schema                  27
health-fd.schema                      28 *reserved for Harmo*
ipmi-fd.schema                        29
weblink-fd.schema                     30
dovecot-fd.schema                     31
sogo-fd-conf.schema                   32
repository-fd.schema                  33
repository-fd-conf.schema             34
gpg-fd.schema                         35
ipmi-fd-conf.schema                   36
desktop-fd-conf.schema                37
template-fd.schema                    38
inventory-fd.schema                   39
fusioninventory-fd.schema             40
fusioninventory-fd-conf.schema        41
voip-fd.schema                        42
dns-fd-conf.schema                    43
webservice-fd-conf.schema             44
ppolicy-fd-conf.schema                45
applications-fd.schema                46
ejbca-fd-conf.schema                  47
personal-fd.schema                    48
ejbca-fd.schema                       49
personal-fd-conf.schema               50
dns-fd.schema                         51
community-fd.schema                   52
community-fd-conf.schema              53
subcontracting-fd.schema              54
newsletter-fd-conf.schema             55
newsletter-fd.schema                  56
dhcp-fd-conf.schema                   57
spamassassin-fd.schema                58
user-reminder-fd-conf.schema          59
audit-fd.schema                       60
audit-fd-conf.schema                  61
core-fd.schema                        62
renater-partage-fd.schema             63
sympa-fd-conf.schema                  64
sinaps-fd-conf.schema                 65
supann-ext-fd.schema                  66
public-forms-fd.schema                67
public-forms-fd-conf.schema           68
invitations-fd.schema                 69
invitations-fd-conf.schema            70
seafile-fd.schema                     71
seafile-fd-conf.schema                72 (temporary waiting for confirmation)
webauthn-fd.schema                    73
webauthn-fd-conf.schema               74
totp-fd.schema                        75
totp-fd-conf.schema                   76
autofs5-fd-conf.schema                77
ipam-fd.schema                        78
ipam-fd-conf.schema                   79
===================================== =====================

===================================== =====================
demoplugin.schema                     1337
test-fd.schema                        1338
===================================== =====================

GOsa legacy Schemas
+++++++++++++++++++

=================== ======================================
Schema              Number attributed
=================== ======================================
core-fd.schema      1.3.6.1.4.1.10098.1.1.12
fai.schema          1.3.6.1.4.1.10098.1.1.5
mail-fd.schema      1.3.6.1.4.1.10098.1.1.12
proxy-fd.schema     1.3.6.1.4.1.10098.1.1.12
service-fd.schema   1.3.6.1.4.1.10098.1.1.9
system-fd.schema    1.3.6.1.4.1.10098.1.1.11
=================== ======================================
