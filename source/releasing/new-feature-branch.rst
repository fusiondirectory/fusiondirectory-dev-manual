Create the new features branch for FusionDirectory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Create the new milestone
-  Create the new features branch from master
-  Remove branch that we just merged
-  Merge Changelog.md, AUTHORS.md, UPGRADE.md into fusiondirectory developement 
   version
-  Merge Changelog.md into fusiondirectory-plugins -dev version
-  Update include/variables_common.inc, only if you create a new feature branch for FusionDirectory

Create the new milestone
^^^^^^^^^^^^^^^^^^^^^^^^

-  got to FusionDirectory `milestones`_ and create the new milestone

-  For FusionDirectory

   -  FusionDirectory 1.3.x
   -  Start date, date of the milestone creation
   -  Stop date is start date + 3 month

Create a new fixes branch from master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The branch should be named with the version of the release followed by **-fixes**.

ex: **1.3** is released the feature branch is **1.3-fixes**

Remove the branch we just merged
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Merge Changelog.md, Authors.md, UPGRADE.md into into the developement branch
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This operation have inside a ticket with the label ~release and with a
**MR**

Changelog.md, AUTHORS.md, UPGRADE.md have to be merged into the developement branch
after a release to ensure that the merge from the -dev to master will be easy.

* Create a new merge request from the developement branch 

* Push into the developpement branch the needed files

.. code:: bash

   git checkout 1.2.1-fixes -- AUTHORS.md

.. code:: bash

   git checkout 1.2.1-fixes -- Changelog.md

.. code:: bash

   git checkout 1.2.1-fixes -- UPGRADE.md

Increment FusionDirectory version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Only if you create a new feature branch for FusionDirectory

open include/variables_common.inc

Change the version number in :

.. code:: php

   define ("FD_VERSION", "1.2-fixes");

.. _milestones :  https://gitlab.fusiondirectory.org/groups/fusiondirectory/-/milestones
