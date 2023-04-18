How to release a FusionDirectory Orchestrator Version
=====================================================

-  Update the AUTHORS.md file
-  Updates the Changelog.md
-  Write the upgrade documentation
-  Update the UPGRADE.md
-  Merge the fixes branch into master

All those operations have to be made onto the 1.x-fixes branch each one
of them inside a ticket with the label ~release and with a **MR**

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

   gitlab_changelog.py --config-file ~/.python-gitlab.cfg --gitlab fd --project "fusiondirectory/fusiondirectory-orchestrator "FusionDirectory Orchestrator 1.1"
 
Update the user documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

open an issue ins the  `user manual issues`_ to update the release notes for 
the supported version, label this issue ~release and with the correct
milestone

The content should got into **source/fusiondirectory-orchestrator/update/supported**

the file should be named like in this example current version to new version

1.0-to-1.1.rst
 
Update the UPGRADE documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Update UPGRADE.md with a new section for the new version corresponding
to what you have put into `user manual supported`_ after updating the documentation
for the release

you can run for example

.. code:: shell

   pandoc --from rst --to markdown -o 1.0-to-1.1.md 1.0-to-1.1.rst

directly in the user-manual source to generate the content to copy/paste at the end of UPGRADE.MD

Merge the fixes branch into master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Only a gitlab master account user can do the merge on the master branch

Tag the release
^^^^^^^^^^^^^^^

After merging the release we need to tag the release. go to `FusionDirectory Orchestrator tags`_ 

-  Paste the Changelog.md corresponding to the release we just made

Run the ci for the FusionDirectory Orchestrator website
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once the tag for a release are created the CI of FusionDirectory Orchestrator project needs to run
to update the FusionDirectory Orchestrator API website

The CI is at `FusionDirectory Orchestrator API`_

.. _user manual issues: https://gitlab.fusiondirectory.org/fusiondirectory/user-manual/-/issues
.. _user manual supported : https://fusiondirectory-user-manual.readthedocs.io/en/latest/fusiondirectory-orchestrator/update/supported/index.html
.. _FusionDirectory Orchestrator tags : https://gitlab.fusiondirectory.org/fusiondirectory/fusiondirectory-orchestrator/-/tags
.. _FusionDirectory Orchestrator API : https://gitlab.fusiondirectory.org/applications/fusiondirectory-orchestrator/-/pipelines
