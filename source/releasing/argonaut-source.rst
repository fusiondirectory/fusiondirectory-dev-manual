How to release a Argonaut  Version
==================================

-  Update AUTHORS.md file
-  Updates the Changelog.md
-  Regenerate the manpages with the new version
-  Merge the branch into master

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

   gitlab_changelog.py --config-file ~/.python-gitlab.cfg --gitlab fd --project "fusiondirectory/argonaut" "Argonaut 1.3.1"
 
Update the user documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

open an issue ins the  `user manual issues`_ to update the release notes for 
the supported version, label this issue ~release and with the correct
milestone

The content should got into **source/argonaut/update/supported**

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

Update manpages
^^^^^^^^^^^^^^^

Regenerate the manpages with the new version, use the
**update-manpages.sh** from the dev-tools

.. code:: shell

   update-manpages.sh fusiondirectory 1.2.3 

Merge the fixes branch into master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Only a gitlab master account user can do the merge on the master branch

Tag the release
^^^^^^^^^^^^^^^

After merging the release we need to tag the release. go to `Argonaut tags`_

-  Paste the Changelog.md corresponding to the release we just made
-  Upload the fusiondirectory-xxx.tar.gz and
   fusiondirectory-plugins-xxx.tar.gz to the tag

.. _user manual issues: https://gitlab.fusiondirectory.org/fusiondirectory/user-manual/-/issues
.. _user manual supported : https://fusiondirectory-user-manual.readthedocs.io/en/latest/fusiondirectory/update/supported/index.html
.. _Argonaut tags : https://gitlab.fusiondirectory.org/fusiondirectory/argonaut/-/tags
.. _schema history : https://gitlab.fusiondirectory.org/fusiondirectory/schema-history/pipelines
