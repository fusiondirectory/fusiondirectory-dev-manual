Testing
===========

The base project for testing is called `automated-testing`. Here all source code for the tests and test framework is placed.testing

#############
Prerequisites
#############

In order for the existing tests to be running properly, some prerequisites are needed:

    * Selenium server: we are using selenium as a running server for our tests, the last version can be downloaded from the official page https://www.selenium.dev/downloads/.
    * Java: tests are written using exclusively Java 17, the version can be installed using https://computingforgeeks.com/install-oracle-java-openjdk-on-debian-linux/ as reference for debian based systems.
    * Geckodriver: tests are written for Firefox browser, for which geckodriver driver is needed; we are using version 0.35 which can be downloaded from https://github.com/mozilla/geckodriver/releases.
    * Vnu jar: some tests need the vnu jar to be available on the machine, this can be downloaded using https://www.npmjs.com/package/vnu-jar as a reference.
    * DSA server: some tests need a dsa server to be available in on the machine, this is done by modifying the orchestrator.conf file from your configuration path to have `tester` as both username and password

.. setup:

#####
Setup
#####

In order to run the tests properly you need to follow the next steps:

1. Clone the automated-testing project
2. Run `cd ./automated-testing/qa`
3. Edit `qa/src/resources/testsConfig.ini` file to match your data:

    * Modify the ldap related values
    * Find the vnu jar path on your device and paste it under the correct variable name
    * Make sure that the folders for downloads and screenshots exist
    * Do not modify the name of the variables, the tests will not work anymore
4. Save the file modifications
5. Run `./gradlew clean` (if you are using a linux based system) or `gradle clean` (if you are using Windows)
6. Run the tests:

    * If you want to run all the tests run `./gradlew test` (this will take some time as the code base is big but you will see the progress of the tests)
    * If you want to run specific tess run `./gradlew test --tests "..."` where ... is the path to your test starting from `qa/src/test/java`, it can be a full subfolder (eg: `org.fd.tests.core.*` to run all tests in core folder), a specific class of tests (eg: `org.fd.tests.core.LoginTest` to run all tests from the `LoginTest` class), or a specific test (eg: `org.fd.tests.core.LoginTest.testGoodLogin` to only run `testGoodLogin` test from LoginTest class)
7. After tests are done the process is finished and you can see:

    * `BUILD SUCCESSFUL` (in green) if all tests passed
    * `BUILD FAILED` (in red) if any test failed
    * In both cases you can see which tests ran along with the running time and the result:

        * `PASSED` for successful test
        * `FAILED` for failed test along with a short message (for troubleshooting see :ref:troubleshooting)

.. troubleshooting:

###############
Troubleshooting
###############

For every failed test we have implemented in our framework some features to help us troubleshoot:

    * If the test is running in a visual interface we are taking a screenshot of the last visual screen of the driver (this is saved in the screenshots folder that you defined in `qa/src/resources/testsConfig.ini` file)
    * We are putting logs in a file (saved in the same screenshots folder, the logs help following the workflow of the test and monitor where it crashed and why)

#################
Project structure
#################

All important modifiable parts of the code base are inside `qa` folder:

    * `config` folder is where we define our lint rules in an xml format, these rules are checked by the pipeline whenever code is pushed to gitlab
    * `build.gradle` file is where we define the needed plugins for this project
    * `src/test` folder is where all the code is:

        * `resources` folder is where we place all of the additional files:

            * `testsConfig.ini` file is the initial configuration for the tests, should be modified as stated in :ref:setup
            * `ldifs` folder is where some ldif files are needed that will be inserted in the ldap server before the tests run
            * as a general rule, all additional files that are not java files, but needed for the tests should be placed here
        * `test/org/fd` folder is where we place all tests:

            * `Utils.java` is a class that only has static fields, these are useful because they can be accessed by anywhere in the project, most of the fields are a java translation of the `testsConfig.ini` file, this is why the name of the field is important to be kept in the ini file
            * `LdapConnection.java` is the class where all ldap related actions are defined like emptying the ldap (`emptyLdap()` method), inserting an ldif in the ldap (`insertLdif(String filename)` method) and so on
            * `Assertions.java` is the class where we define all methods that assert something like asserting that a user is logged in (`assertLoggedIn(String username)` method)
            * `ScreenshotTestWatcher.java` is the class where we define the actions to be done after a test finished, what is particularly interesting about this class is that it allows the developer to distinguish between failed, successful and aborted test and we defined some actions for failed tests to help us tackle the issues, see:ref:`troubleshooting`
            * `FusionDirectoryTestCase.java` is the main template of a test class inside FusionDirectory, it merges `LdapConnection`, `Assertions` and `ScreenshotTestWatcher` with the Selenium driver to have access to the web page of FusionDirectory and a lot fo needed operations like clicking buttons
            * `tests` folder is where all the explicit tests are:

                * `core` folder contains test that verify the functionality of core FusionDirectory
                * `plugins` folder contains one folder for each plugin of FusionDirectory that has tests
                * `tools` folder contains one folder for each tool that has tests (schema manager, plugin manager, configuration manager, migration manager and orchestrator client)

                    * this folder is particularly different from the other ones because the tests for schema manager, plugins manager, configuration manager and migration manager have no connection with the web interface, but they need access to a Unix console, that is why there are are files outside the subfolders
                    * `CommandLineTestCase.java` defines methods that interact with the command line:

                        * `executeCommandWithWait(String command)` method is used when no input from the user is needed to perform the action
                        * `executeCommandWithoutWait(String command)` method is used when some input is needed, this will be provided by using the `Response` object returned by this method through the `write(String message)` method
                    * `CommandLineTestWatcher.java` is a smaller version of `ScreenshotTestWatcher.java` file, only copying the log files into a safe space since no screenshot can be taken

                * `installation` folder has only one test that verifies the functionality of the installation page

###################
How to write a test
###################

Before starting writing a test you should decide where to place it and in order to figure this out you need to answer the question `What am I testing?` and if the answer is a plugin `abc`, you should place your test in `plugins/abc` folder. Then, create a class in the right folder with a proper name, ending in `Test`. In the class constructor define the `initLdifs` array with the names of all needed ldfis for your test, or leave it a n empty array if none is needed. If you are altering the FusionDirectory related concepts make sure to revert the changes before the test ends or create an `@AfterEach` annotated method that will be automatically called after the tests ends. If you need to fetch elements from the web interface, try first to look into `FusionDirectoryTestCase.java` file because most of the times the method already exists. We prefer this because the tests will be kept cleaner like that and if any name convention changes it is easier to maintain the tests. Any test method has to be annotated by `@Test` (or similar ones like `@RepeatedTes(n)` or `@ParameterizedTest(methodName)`) in order to be run with gradle. Before pushing to gitlab you should try 3 things:

    * Run `./gradlew checkstyleTest` and `./gradlew spotbugsTest` and fix the issues if any
    * Run the tests in your virtual machine and make sure they are passing
    * Run the tests in a bullseye docker image and ubuntu docker image to make sure everything works out smoothly

By doing so, we reduce the number of failed pipelines and the process of merging source code is faster, since the purpose of the tests is to ease the development process and not to make it slower. To do so we need reliable tests.
