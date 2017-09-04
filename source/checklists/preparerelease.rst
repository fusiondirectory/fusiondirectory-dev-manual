Prepare for release
===================

How to release a FusionDirectory stable version
-----------------------------------------------

* Put yourself in the branch corresponding to the release you are about to make for example to release a fix version

.. code-block:: bash

  $ git checkout x.x-fixes

* Update the locales from transifex in fusiondirectory and fusiondirectory-plugins,
  this will get all the new strings from transifex

.. code-block:: bash

  $ tx pull -a -f

* Update the changelog

  - Go to the roadmap of fusiondirectory and fusiondirectory plugins, 
  - Copy the list of tickets inside this release and add them to the changelog. 
  - Add Fix or Feature in front of each ticket to mention the kind of ticket this is
  - Class them from increasing order

.. code-block:: bash
  
  [Feature] Bugs #2586: class_plugin should be reviewed
  [Feature] FusionDirectory plugins - Bugs #3615: Adding fdSystemLock to windows workstations
  [Feature] FusionDirectory plugins - Bugs #4024: We should be able to create a system with fusiondirectory-shell
  [Feature] FusionDirectory plugins - Bugs #5315: mail methods code should be reviewed and cleaned
  [Feature] FusionDirectory plugins - Bugs #5340: DHCP postLdapSave should lock the object modified
  [Feature] FusionDirectory plugins - Bugs #5341: DHCP tab should be able to load values from template
  [Fix] Bugs #5347: Template types needs their own icon somehow

* Open include/variables_common.inc and update the FD_VERSION variable to the released version

.. code-block:: bash

  define ("FD_VERSION", "1.2.1");
  
* Add the authors of the patch we received to the AUTHORS file
 
..

  * Markus Amersdorfer <der.plusch@subnet.at>
    Wiki setup, Testing, hints, proposals

* Write the upgrade documentation 
   
  * In `FusionDirectory Installation <http://documentation.fusiondirectory.org/en/documentation_admin] section installation>`_

* Update the contrib/docs/UPGRADE 

  * Put in it a section for the new version corresponding to what you have put into 
    `FusionDirectory Installation <http://documentation.fusiondirectory.org/en/documentation_admin] section installation>`_

* Regenerate the manpages with the new version

* How to generate man pages from perl programs for FusionDirectory

 *The manpages are inside the perl programs so you need to update them at each release* :

  This should be done for :
  - fusiondirectory-insert-schema
  - fusiondirectory-setup
  - fusiondirectory.conf.pod

.. code-block:: bash
  
  cd contrib
  pod2man -c "FusionDirectory Documentation" -r "FusionDirectory x.x" bin/fusiondirectory-insert-schema man/fusiondirectory-insert-schema.1
  pod2man -c "FusionDirectory Documentation" -r "FusionDirectory x.x" man/fusiondirectory.conf.pod man/fusiondirectory.conf.5
  pod2man -c "FusionDirectory Documentation" -r "FusionDirectory x.x" bin/fusiondirectory-setup man/fusiondirectory-setup.1

  *You need to check them with lexgrog to find any errors* :

  lexgrog man/fusiondirectory-insert-schema.1
  lexgrog man/fusiondirectory.conf.5
  lexgrog man/fusiondirectory-setup.1

  *And finally read the manual generated* :

  man -l man/fusiondirectory-insert-schema.1
  man -l man/fusiondirectory.conf.5
  man -l man/fusiondirectory-setup.1

- Merge the branch into master for fusiondirectory and fusiondirectory plugins

  - git checkout master
  - git merge --no-ff name_of_your_branch : commit message "Releasing FusionDirectory 1.0.7.3"
  - git tag -a fusiondirectory-version
  - git push
  - git push --tags

- Remove branch that we just merged

  - git branch -d name_of_your_branch
  - git push origin :name_of_your_branch

- Create the new fixes branch from master
  
  - git branch name_of_your_branch-fixes
  - git checkout name_of_your_branch-fixes
  - git checkout master

- Push the new branch to the git server

  - git push origin name_of_your_branch-fixes

- follow https://forge.fusiondirectory.org/projects/fd/wiki/How_to_release_FusionDirectory_Official_Tarballs#How-to-release-FusionDirectory-Official-Tarballs

- upload the tarballs to our repo site


