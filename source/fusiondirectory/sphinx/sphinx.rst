.. _sphinx:

How to Use Sphinx for Documentation
===================================

This guide explains how to effectively use Sphinx to create high-quality documentation for your developed plugin.

Why Use Sphinx?
---------------
Sphinx is a powerful documentation generator that supports reStructuredText (reST) and provides features such as:

- Automatic table of contents and cross-referencing
- Code highlighting and autodoc for API documentation
- Integration with Read the Docs and PDF/HTML outputs
- Easy customization with themes and extensions

Setting Up Sphinx
-----------------
To begin using Sphinx, follow these steps:

0. **Set Up a Python Virtual Environment**

   *We strongly recommend using a Python virtual environment before installing any packages to avoid dependency conflicts.*

   .. code-block:: bash

      python -m venv env
      source ./env/bin/activate

1. **Install Sphinx and a Theme**

   .. code-block:: bash

      pip install sphinx sphinx_rtd_theme

2. **Create a New Documentation Project OR use our user-manual, dev-manual respositories**

   .. code-block:: bash

      sphinx-quickstart #Only required if starting from empty docs directory.

   Follow the prompts to configure your documentation directory.

   *We recommend separating the source and build directories for better organization.*

3. **Organize Your Documentation**

   Structure your files as follows:

   .. code-block:: text

      docs/
      ├── build/           # Generated output files
      ├── source/
      │   ├── conf.py      # Sphinx configuration file
      │   ├── index.rst    # Main entry point
      │   ├── images/      # Store images and diagrams (create this directory)

Writing Good Documentation
--------------------------
1. Use Clear Headings and Structure
Use hierarchical headings to break your documentation into sections. Example:

.. code-block:: rst

   My Section
   ==========

   Subsection
   ----------

   Sub-subsection
   ~~~~~~~~~~~~~~

2. Formatting Text Properly
Use the following conventions for formatting:

- **Bold text**: ``**bold text**``
- *Italic text*: ``*italic text*``
- ``Inline code``: ````inline code````
- Lists:

  .. code-block:: rst

     - Item 1
     - Item 2

- Numbered lists:

  .. code-block:: rst

     1. First step
     2. Second step

3. Documenting Attributes and Fields
Each attribute should be clearly described with its purpose, type, and possible values. Example:

.. code-block:: rst

   - **supannMailPrivee**: Defines the user's private email address.
     - **Type**: String
     - **Example**: ``user@example.com``

4. Adding Code Examples
Use code blocks to demonstrate examples. Ensure the language is specified for syntax highlighting.

**Example (PHP):**

.. code-block:: php

   private static function example(string $myString): void {
       // This is an example function
       return "Hello, Sphinx!";
   }

5. Including Images and Diagrams
Place images inside the `images/` folder and reference them in your documentation as follows:

.. code-block:: rst

   .. image:: images/example.png
      :alt: Example Image

6. Cross-Referencing Sections and Files
To create cross-references, use:

.. code-block:: rst

   See :ref:`another-section` for more details.

Or reference a separate file:

.. code-block:: rst

   See :doc:`usage` for more information.

Building the Documentation
--------------------------
Once your documentation is written, build it using:

.. code-block:: bash

   make html

The generated HTML files will be available in the `build/html/` directory.


Guidelines for Your Plugin Documentation
----------------------------------------

When documenting your plugin, follow these best practices to ensure clarity, completeness, and ease of use:

- **Introduction**: Provide an overview of your plugin, its purpose, and the key benefits it offers.
- **Attribute Documentation**: Clearly describe each attribute, including its type, purpose, default values, and possible options.
- **Method Documentation**: Explain each method’s functionality, parameters, return values, and any references or inherited behaviors.
- **Workflow Explanation**: Outline the logical flow of your plugin, detailing how methods interact and contribute to its overall functionality.
- **Conclusion**: Summarize the plugin’s usage, highlighting its main features and potential applications.

By following these guidelines, you will create well-structured and user-friendly documentation for your plugin.



Conclusion
----------
By following these best practices, you can create clear, well-structured, and professional documentation using Sphinx.

For more details, visit the official Sphinx documentation:
📌 **https://www.sphinx-doc.org/**