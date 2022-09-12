New ticket opened
=================

First the label of the dolibarr project should be added to it.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The dolibarr label are made like this : **PJYYYY**-project number

We have some basic project number that should always be used by default if there is no customer project.

-  FusionDirectory / Automated Testing / FusionDirectory demo :
   **PJ1802-0188**

-  Argonaut : **PJ1802-0190**

-  Packaging Debian / Redhat / Centos / Ubuntu : **PJ1802-0189**

-  Gitlab-ci changes : **PJ1802-0188**

-  User-manual : **PJ2003-0342**

-  Dev Manual : **PJ2003-0343**

Second the component where the bug/enhancement is to be made should be specified
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Example : fusiondirectory-core or plugin-xxx

.. warning::

   It could be several component 

Third if this is a customer under contract the level of support should be added also
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Example : basic, intermediate, expert, premium 

Ticket as been treated
======================

you need to input you time into the ticket with **/spend** with a choice of xxmin, xxhours, xxdays

.. warning::

   Very important as it allow to caculate the time spend on this feature or fix

if some code has been commited and need to be tested
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The **to be tested** label should be added

if some more info is needed to act on the report
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The **need info** label should be added, don’t hesitate to ping the
   user reporting the bug with **@(useranme)** to ask him to check it out

If the change need to be cherry-picked in a -fixes version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The **fixes** label is added, when the cherry-pick as been merged we
   remove the **fixes** and add the **fixes-merged** label

if the change need a change in packaging
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The **packaging** label is added and a corresponding ticket is open
   in the corresponding distribution projects
   
   - `Debian Packaging`_ 
   - `Centos Packaging`_
   - `Ubuntu Packaging`_
   

-  The packaging ticket are linked back with the code fix ticket

The bug is closed
-----------------

-  Remove the **to be tested** label, and add one of the changelog label
   to specify what has been done.

   -  Added
   -  Changed
   -  Deprecated
   -  Fixed
   -  Removed
   -  Security

Those label are used to generate a changelog when we release a new
version of the software, and also used when we want to search in which
version something has been changed and what the type of change it was


.. _Debian Packaging : https://gitlab.fusiondirectory.org/debian
.. _Centos Packaging : https://gitlab.fusiondirectory.org/centos
.. _Ubuntu Packaging : https://gitlab.fusiondirectory.org/ubuntu
