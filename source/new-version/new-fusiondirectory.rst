Creating a new version of FusionDirectory
=========================================

-  Create the new milestone
-  Create the new branchs from master
-  Update include/variables_common.inc

Create the new milestone
^^^^^^^^^^^^^^^^^^^^^^^^

-  got to FusionDirectory `milestones`_ and create the new milestone

   -  FusionDirectory version
   -  Start date, date of the milestone creation
   -  Stop date is start date + 3 month

Create a new fixes branch from master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We need to create a branch for fusiondirectory and fusiondirectory-plugins

The branch should be named with the version of the release followed by **-fixes**.

ex: **1.3** is released the feature branch is **1.3-fixes**

Increment FusionDirectory version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Only if you create a new feature branch for FusionDirectory

open include/variables_common.inc

Change the version number in :

.. code:: php

   define ("FD_VERSION", "1.3-fixes");

.. _milestones :  https://gitlab.fusiondirectory.org/groups/fusiondirectory/-/milestones
