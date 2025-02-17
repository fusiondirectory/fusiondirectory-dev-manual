Testing
========

The base project for testing is called `automated-testing`. Here all source code for the tests and test framework is placed.

Prerequisites
-------------

In order for the existing tests to run properly, some prerequisites are needed:

* **Selenium server**: We are using Selenium as a running server for our tests. The latest version can be downloaded from the official page: `<https://www.selenium.dev/downloads/>`_.
* **Java**: Tests are written exclusively using Java 17. The version can be installed using `<https://computingforgeeks.com/install-oracle-java-openjdk-on-debian-linux/>`_ as a reference for Debian-based systems.
* **Geckodriver**: Tests are written for the Firefox browser, for which the Geckodriver is needed. We are using version 0.35, which can be downloaded from `<https://github.com/mozilla/geckodriver/releases>`_.
* **VNU Jar**: Some tests need the VNU jar to be available on the machine. This can be downloaded using `<https://www.npmjs.com/package/vnu-jar>`_ as a reference.
* **DSA server**: Some tests need a DSA server to be available on the machine. This is done by modifying the ``orchestrator.conf`` file from your configuration path to have ``tester`` as both username and password.

.. _setup:

Setup
-----

In order to run the tests properly, follow these steps:

1. Clone the `automated-testing` project.
2. Run ``cd ./automated-testing/qa``.
3. Edit ``qa/src/resources/testsConfig.ini`` file to match your data:

   * Modify the LDAP-related values.
   * Find the VNU jar path on your device and paste it under the correct variable name.
   * Make sure that the folders for downloads and screenshots exist.
   * Do not modify the name of the variables, as the tests will not work otherwise.

4. Save the file modifications.
5. Run ``./gradlew clean`` (if using a Linux-based system) or ``gradle clean`` (if using Windows).
6. Run the tests:

   * To run all the tests, execute ``./gradlew test`` (this will take some time as the code base is large, but you will see the test progress).
   * To run specific tests, execute ``./gradlew test --tests "..."``, where ``...`` is the path to your test starting from ``qa/src/test/java``. This can be:
     * A full subfolder (e.g., ``org.fd.tests.core.*`` to run all tests in the core folder).
     * A specific class of tests (e.g., ``org.fd.tests.core.LoginTest`` to run all tests from the ``LoginTest`` class).
     * A specific test (e.g., ``org.fd.tests.core.LoginTest.testGoodLogin`` to only run ``testGoodLogin`` from the ``LoginTest`` class).

7. After tests complete, you will see:

   * ``BUILD SUCCESSFUL`` (in green) if all tests passed.
   * ``BUILD FAILED`` (in red) if any test failed.
   * In both cases, the test results will display:

     * ``PASSED`` for successful tests.
     * ``FAILED`` for failed tests, along with a short message (for troubleshooting, see :ref:`troubleshooting`).

.. _troubleshooting:

Troubleshooting
---------------

For every failed test, we have implemented features in our framework to aid troubleshooting:

* If the test is running in a visual interface, we take a screenshot of the last visual screen of the driver (saved in the ``screenshots`` folder defined in ``qa/src/resources/testsConfig.ini``).
* Logs are saved in a file in the same ``screenshots`` folder. These logs help track the workflow of the test and identify where and why it crashed.

Project Structure
-----------------

All important modifiable parts of the code base are inside the ``qa`` folder:

* ``config`` folder: Defines lint rules in XML format, checked by the pipeline whenever code is pushed to GitLab.
* ``build.gradle`` file: Defines the needed plugins for this project.
* ``src/test`` folder: Contains all the test code:

  * ``resources`` folder: Stores additional files:

    * ``testsConfig.ini``: The initial configuration for the tests, should be modified as stated in :ref:`setup`.
    * ``ldifs`` folder: Contains LDIF files inserted into the LDAP server before the tests run.
    * General rule: All additional non-Java files required for tests should be placed here.

  * ``test/org/fd`` folder: Contains all test classes:

    * ``Utils.java``: A class with static fields, mainly Java translations of ``testsConfig.ini`` variables.
    * ``LdapConnection.java``: Defines LDAP-related actions like emptying the LDAP (``emptyLdap()``) and inserting an LDIF (``insertLdif(String filename)``).
    * ``Assertions.java``: Contains methods for assertions, such as checking if a user is logged in (``assertLoggedIn(String username)``).
    * ``ScreenshotTestWatcher.java``: Defines actions executed after a test completes, including distinguishing between failed, successful, and aborted tests. See :ref:`troubleshooting`.
    * ``FusionDirectoryTestCase.java``: The main test class template in FusionDirectory. It integrates ``LdapConnection``, ``Assertions``, and ``ScreenshotTestWatcher`` with Selenium to interact with FusionDirectory’s web interface.

  * ``tests`` folder: Contains explicit tests:

    * ``core`` folder: Tests verifying the core functionality of FusionDirectory.
    * ``plugins`` folder: Contains one subfolder for each FusionDirectory plugin that has tests.
    * ``tools`` folder: Contains tests for various tools (schema manager, plugin manager, configuration manager, migration manager, and orchestrator client):

      * Unlike other folders, these tests often require Unix console access rather than web interface interaction.
      * ``CommandLineTestCase.java``: Defines methods for interacting with the command line:

        * ``executeCommandWithWait(String command)``: Used when no user input is required.
        * ``executeCommandWithoutWait(String command)``: Used when user input is required, handled through the returned ``Response`` object.
      * ``CommandLineTestWatcher.java``: A smaller version of ``ScreenshotTestWatcher.java`` that only copies log files, as screenshots are not applicable.

    * ``installation`` folder: Contains a single test verifying the installation page functionality.

How to Write a Test
-------------------

Before writing a test, determine where it should be placed by asking, *What am I testing?* If the answer is a plugin ``abc``, place the test in the ``plugins/abc`` folder. Then:

1. Create a class in the appropriate folder, ensuring the name ends in ``Test``.
2. In the class constructor, define the ``initLdifs`` array with required LDIF files, or leave it empty if none are needed.
3. If altering FusionDirectory-related concepts, revert changes before the test ends or use an ``@AfterEach`` annotated method to clean up automatically.
4. When fetching web interface elements, check ``FusionDirectoryTestCase.java`` for existing methods before writing new ones to maintain clean tests and ensure easy maintenance.
5. Annotate test methods with ``@Test`` (or similar annotations like ``@RepeatedTest(n)`` or ``@ParameterizedTest(methodName)``) for Gradle compatibility.

Before pushing to GitLab, perform these checks:

* Run ``./gradlew checkstyleTest`` and ``./gradlew spotbugsTest`` and fix any issues.
* Run the tests in your virtual machine and ensure they pass.
* Run the tests in a Bullseye Docker image and an Ubuntu Docker image to verify cross-platform compatibility.

By following these steps, we minimize failed pipelines and expedite code merging, ensuring tests facilitate development rather than hinder it. Reliable tests are key to this process.

