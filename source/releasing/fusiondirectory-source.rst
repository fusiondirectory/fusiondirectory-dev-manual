How to release a FusionDirectory Version
========================================

-  Updates the locales
-  Increment FusionDirectory version
-  Update the AUTHORS.md file
-  Updates the Changelog.md in fusiondirectory and
   fusiondirectory-plugins
-  Write the upgrade documentation
-  Update the UPGRADE.md
-  Merge the branch into master for fusiondirectory and fusiondirectory
   plugins
   
All those operations have to be made onto a branch each one
of them inside a ticket with the label ~release and with a **MR**

Updates the locales
^^^^^^^^^^^^^^^^^^^

Update the locales from transifex in fusiondirectory and
fusiondirectory-plugins

.. code:: shell

   tx pull -a -f

Increment FusionDirectory version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

open **include/variables_common.inc**

Change the version number in :

.. code:: php

   define ("FD_VERSION", "1.2.x");

Update the AUTHORS file
^^^^^^^^^^^^^^^^^^^^^^^

Add the authors of all the patchs we received to the AUTHORS file

::

   * Markus Amersdorfer <der.plusch@subnet.at>
       Wiki setup, Testing, hints, proposals

Updates the Changelog.md
^^^^^^^^^^^^^^^^^^^^^^^^

To update the Changelog.md you must first run the following command, at the end you have to put the milestone you want a changelog for

.. code:: shell

   gitlab_changelog.py --config-file ~/.python-gitlab.cfg --gitlab fd --project "fusiondirectory/fd" --project "fusiondirectory/fd-plugins" "FusionDirectory 1.3.1"
 
Update the user documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

open an issue ins the  `user manual issues`_ to update the release notes for 
the supported version, label this issue ~release and with the correct
milestone

The content should got into **source/fusiondirectory/update/supported**

the file should be named like in this example current version to new version


1.3-to-1.3.1.rst
 
Update the UPGRADE documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Update UPGRADE.md with a new section for the new version corresponding
to what you have put into `user manual supported`_ after updating the documentation
for the release

you can run for example

.. code:: shell

   pandoc --from rst --to markdown -o 1.3-to-1.3.1.md 1.3-to-1.3.1.rst

directly in the user-manual source to generate the content to copy/paste at the end of UPGRADE.MD

Merge the branch into master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Only a gitlab master account user can do the merge on the master branch

Tag the release
^^^^^^^^^^^^^^^

After merging the release we need to tag the release. go to `FusionDirectory tags`_ and `FusionDirectory Plugin tags`_

-  Paste the Changelog.md corresponding to the release we just made

Run the ci for the schema-history website
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once the tags for a release are created in both fusiondirectory and
fusiondirectory-plugins, the CI of schema-history project needs to run
to update the schema website.

The CI is at `schema history`_

.. _user manual issues: https://gitlab.fusiondirectory.org/fusiondirectory/user-manual/-/issues
.. _user manual supported : https://fusiondirectory-user-manual.readthedocs.io/en/latest/fusiondirectory/update/supported/index.html
.. _FusionDirectory tags : https://gitlab.fusiondirectory.org/fusiondirectory/fd/tags
.. _FusionDirectory Plugin tags : https://gitlab.fusiondirectory.org/fusiondirectory/fd-plugins/tags
.. _schema history : https://gitlab.fusiondirectory.org/applications/schema-history
