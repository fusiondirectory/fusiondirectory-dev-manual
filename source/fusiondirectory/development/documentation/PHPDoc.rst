.. _phpdoc_guide:

##############################
PHPDoc Guide for Doxygen Usage
##############################

This guide explains how to properly document PHP code using PHPDoc comments and generate documentation using `Doxygen <https://www.doxygen.nl/>`_.

.. contents:: Table of Contents
   :local:
   :depth: 2

----------------------
Introduction to PHPDoc
----------------------

PHPDoc is a standardized way of documenting PHP code using special comment blocks (`/** ... */`).
Doxygen can parse these comments to generate structured documentation.

**Basic Example:**

.. code-block:: php

   <?php
   /**
    * Adds two numbers.
    *
    * @param int $a First number.
    * @param int $b Second number.
    * @return int Sum of $a and $b.
    */
   function add(int $a, int $b): int {
       return $a + $b;
   }

-----------------
PHPDoc Syntax
-----------------

**General Structure**

A PHPDoc comment starts with `/**` and ends with `*/`. Each line inside the block should start with `*`. The first paragraph is usually a short description, followed by optional tags.

**Example:**

.. code-block:: php

   /**
    * Short description.
    *
    * Detailed description, spanning multiple lines.
    *
    * @tagname Type Description
    */

**Common Tags**

.. list-table:: Common PHPDoc Tags
   :widths: 15 40 45
   :header-rows: 1

   * - **Tag**
     - **Description**
     - **Example**
   * - ``@param``
     - Describes function parameters
     - ``@param string $name The name of the user.``
   * - ``@return``
     - Describes the return value
     - ``@return bool True on success, false otherwise.``
   * - ``@var``
     - Describes class properties
     - ``@var int $count Number of items.``
   * - ``@throws``
     - Documents exceptions thrown by the function
     - ``@throws Exception If an error occurs.``
   * - ``@deprecated``
     - Marks a function/class as deprecated
     - ``@deprecated Use newFunction() instead.``
   * - ``@author``
     - Specifies the author of the code
     - ``@author John Doe <john@example.com>``
   * - ``@version``
     - Specifies version information
     - ``@version 1.0.0``
   * - ``@since``
     - Indicates when a feature was added
     - ``@since 2.0``

---------------------------
Documenting Classes & Files
---------------------------

**Documenting a Class**

.. code-block:: php

   <?php
   /**
    * Description of your class user here and potential extensions.
    */
   class User {
       /**
        * The user's name.
        *
        * @var string
        */
       private string $name;

       /**
        * Constructor.
        *
        * @param string $name The user's name.
        */
       public function __construct(string $name) {
           $this->name = $name;
       }

       /**
        * Gets the user's name.
        *
        * @return string The name of the user.
        */
       public function getName(): string {
           return $this->name;
       }
   }

-------------------------
Generating Documentation
-------------------------

To generate documentation using Doxygen:

1. **Install Doxygen**: Download from `https://www.doxygen.nl/` and install it.
2. **Create a Doxygen configuration file**: Run:

   .. code-block:: bash

      doxygen -g Doxyfile

3. **Modify the `Doxyfile`**:

   - Set `INPUT` to the PHP source code directory.
   - Enable `EXTRACT_ALL = YES` to parse all comments.
   - Set `FILE_PATTERNS = *.php` to only parse PHP files.

4. **Generate the Documentation**:

   .. code-block:: bash

      doxygen Doxyfile

5. **View the Output**:

   - Open `html/index.html` in a browser.

-----------------
Best Practices
-----------------

- **Use meaningful descriptions**: Avoid generic comments.
- **Keep comments up-to-date**: Maintain consistency with code changes.
- **Use proper data types**: Always specify accurate types (`int`, `string`, `array`, etc.).
- **Be concise but informative**: Don’t over-explain obvious things.
- **Always generate comments above your methods**: Even if the method simply return void.

-----------------
Conclusion
-----------------

Using PHPDoc correctly helps create clean, well-documented code. With Doxygen, you can turn comments into structured, browsable documentation.

For more details, refer to:
- `Doxygen PHP Support <https://www.doxygen.nl/manual/docblocks.html>`_
- `PHPDoc Standard <https://www.phpdoc.org/>`_
