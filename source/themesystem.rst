FusionDirectory theme system
============================

A theme is defined by:

  - A folder in *html/themes*
  - A folder with the same name in *ihtml/themes*

The folder in *html/themes* contains:

  - An index.theme file following the `Icon Theme Specification <http://standards.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html#file_formats>`_
  - The icons as described in the index.theme file, usually in an icons folder
  - Replacements for any css file

The folder in ihtml should have the same name and should contain replacements for any template file.

Icon theme file
---------------

Here is the minimal index.theme file to inherit another icon theme.

.. code-block:: ini

  [Icon Theme]
  Name=MyTheme
  Comment=Example from documentation
  Inherits=oxygen

For an example of a more complex index.theme file look at `the one of the default theme <https://gitlab.fusiondirectory.org/fusiondirectory/fd/blob/e2d1369485f03dec3ac9886deba8606ceec897f2/html/themes/breezy/index.theme>`_

All main icon themes should be working, you can activate them by using a symlink in the right folder.
For instance on Debian if I want gnome icon theme:

.. code-block:: bash

  $ ls -l /usr/share/fusiondirectory/html/themes/
  drwxr-xr-x 4 root root 4096 Mar 16 10:24 breezy/
  drwxr-xr-x 4 root root 4096 Mar 16 10:24 legacy/
  lrwxrwxrwx 1 root root   23 Jun 12  2014 gnome -> /usr/share/icons/gnome/

Replacements of css and tpl files
---------------------------------

Any file you see in *html/themes/breezy* or *ihtml/themes/breezy* can be overridden by placing in your theme a file with the same name (css goes in *html*, tpl in *ihtml*).

**Note** that the file *html/themes/breezy/theme.css* is empty so that you can safely override it without losing anything from the default theme. Consider using it for theme making only small modifications.
