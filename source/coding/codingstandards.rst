.. _coding-style-label:

Coding Style
============

Scope of style guidelines
-------------------------

In order to keep the code consistent, please use the following conventions.
These conventions are no judgement call on your coding abilities, but more
of a style and look call.

Performance and Readability
---------------------------

* It is more important to be correct than to be fast.
* It is more important to be maintainable than to be fast.
* Fast code that is difficult to maintain is likely going to be looked down upon.


Indentation and line length
---------------------------

- 2 spaces
- Max line width: 80

.. code-block:: php

   <?php
   // base level
       // level 1
           // level 2
       // level 1
   // base level

As a basic style rule, please use 2 spaces instead of tabulators. This will remove problems when using "diff".

.. note::

  For VI users, this can be achieved by the following settings:

  * set expandtab
  * set shiftwidth=2
  * set softtabstop=2
  * set tabstop=2


Spacing
-------

Use a space before affectations, around operators, before parenthesis or braces.

.. code-block:: php

  <?php
  // Methods
  foo($parameter);

  // Arrays
  $b = $value[0];

  // Readability
  if ($b + 5 > foo(bar() + 4)) {
  }


For vars declaration place values on the same column

.. code-block:: php

  <?php
  var $most           = "something";
  var $iHaveALongName = "value";
  var $otherName      = "otherValue";

Always use spaces to seperate arguments after commat:

.. code-block:: php

  <?php
  function foo ($param1, $param2)

Always use single spaces to split logical and mathematical operations:

.. code-block:: php

  <?php
  if ($a > 6 && $b == 17 && (foo($b) < 1)) {
  }


Braces
------

If statements with or without else clauses are formatted like this:

.. code-block:: php

  <?php
  if ($value) {
    foo();
    bar();
  }

  if ($value) {
    foo();
  } else {
    bar();
  }

Switches are formatted like this:

.. code-block:: php

  <?php
  switch ($reason) {
    case 'fine':
      foo();
      break;

    case 'well':
      bar();
      break;
  }


Always use use braces for single line blocks:

.. code-block:: php

  <?php
  if ($value) {
    foo();
  }

Function definitions, Classes and Methods have an opening brace on the next line:

.. code-block:: php

  <?php
  function bar ()
  {
  ...
  }


Casing
------

Always use camel casing with lowercase characters in the beginning for multiword identifiers.

.. code-block:: php

  <?php
  function checkForValidity ()
  {
    $testSucceeded = FALSE;
    ...
  }


Naming
------

Non trivial variable names should speak for themselves from within the context.

.. code-block:: php

  <?php
  // Use
  $hour = 5;
  // instead of
  $g = 5;

Find short function names that describe what the function does, in order to make the code read like a written sentence.

.. code-block:: php

  <?php
  if (configReadable("/etc/foo.conf")) {
  }

Use uppercase for constants/defines and _ to separate if there is more than one word :

.. code-block:: php

  <?php
  if ($speedUp == TRUE) {
    $wait = SHORT_WAIT;
  } else {
    $wait = LONG_WAIT;
  }

Arrays
------

Arrays must be declared using the short syntax (``[]``).


PHP specific
------------

Use return without parenthesis

.. code-block:: php

  <?php
  return TRUE; // good

  return(TRUE); // bad

Open and close tags

Short tag (``<?``) is not allowed; use complete tags (``<?php``).

.. code-block:: php

  <?php
    // Something here
  ?>

Including files
---------------

Use ``require_once`` in order to include the file once and to raise warning if file does not exists:

.. code-block:: php

  <?php
  require_once("class_setupStep.inc");

Quotes / double quotes
----------------------

* You must use single quotes for indexes, constants declaration, translations, ...
* When you have to use tabulation character (``\t``), carriage return (``\n``) and so on, you should use double quotes.
* For performances reasons since PHP7, you may avoid strings concatenation.

Examples:

.. code-block:: php

   <?php
   //for that one, you should use single, but this is at your option...
   $a = 'foo';

   //use double quotes here, for $foo to be interpreted
   //   => with double quotes, $a will be "Hello bar" if $foo = 'bar'
   //   => with single quotes, $a will be "Hello $foo"
   $a = "Hello $foo";

   //use single quotes for array keys
   $tab = [
      'lastname'  => 'john',
      'firstname' => 'doe',
   ];

   //Do not use concatenation to optimize PHP7
   //note that you cannot use functions call in {}
   $a = "Hello {$tab['firstname']}";

   //single quote translations
   $str = _('My string to translate');

   //Double quote for special characters
   $html = "<p>One paragraph</p>\n<p>Another one</p>";

   //single quote cases
   switch ($a) {
      case 'foo' : //use single quote here
         ...
      case 'bar' :
         ...
   }


Files Format
------------

* UTF-8, LF - not CR LF

.. _checking-standard-label:

Checking standards
------------------

In order to check some standards are respected, we provide some custom `PHP CodeSniffer <http://pear.php.net/package/PHP_CodeSniffer>`_ rules.

First clone the dev-tools that contains Fusiondirectory developement tools

.. code-block:: bash

    git clone https://gitlab.fusiondirectory.org/fusiondirectory/dev-tools.git

Then run the codesniffer rules from the top directory:

.. code-block:: bash

    find . -type f -name '*.php' -o -name '*.inc' -exec phpcs --standard=../dev-tools/php-codesniffer-rules/FDStandard/ruleset.xml "{}" \;

If the above command does not provide any output, then, all is OK :)

An example error output would looks like:

.. code-block:: bash

  FILE: fusiondirectory/fusiondirectory/include/class_ldap.inc
  --------------------------------------------------------------------------------
  FOUND 9 ERROR(S) AFFECTING 4 LINE(S)
  --------------------------------------------------------------------------------
  260 | ERROR | Case breaking statement indented incorrectly; expected 10
      |       | spaces, found 8
  802 | ERROR | Assignment blocks should have all assignment tokens on the same
      |       | column
  965 | ERROR | Expected 1 space before "?"; 0 found
  965 | ERROR | Expected 1 space after "?"; 0 found
  965 | ERROR | Expected 1 space before ":"; 0 found
  965 | ERROR | Expected 1 space after ":"; 0 found
  973 | ERROR | Expected 1 space before "?"; 0 found
  973 | ERROR | Expected 1 space after "?"; 0 found
  973 | ERROR | Expected 1 space before ":"; 0 found
  --------------------------------------------------------------------------------

