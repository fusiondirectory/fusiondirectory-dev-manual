==========================
Creating an Orchestrator Plugin
==========================

This guide explains how to create an Orchestrator Plugin, implementing potential "Strategy development pattern" using
interfaces implementation.

-------------------------------
1. Implementing the Interface
-------------------------------

An Orchestrator Plugin must implement the ``EndpointInterface`` to define the required methods for handling API requests.
Each method corresponds to an HTTP operation (GET, POST, DELETE, PATCH), allowing structured API interactions.

To create a new plugin, define a class that implements this interface and ensure it includes the necessary methods.

.. code-block:: php

    class anOrchestratorPluginClass implements EndpointInterface
    {
        private TaskGateway $gateway;

        /**
         * Constructor to initialize the plugin with a TaskGateway.
         *
         * @param TaskGateway $gateway The gateway instance for interacting with external data sources (e.g., LDAP).
         */
        public function __construct(TaskGateway $gateway)
        {
            $this->gateway = $gateway;
        }
    }

The constructor takes a ``TaskGateway`` object, which serves as an interface to interact with external services such as LDAP.
This gateway will be used within the methods to fetch, update, and delete data.

----------------------------------
2. Handling GET Requests
----------------------------------

The **GET method** is used to retrieve existing data, such as tasks or configurations, from the system.

.. code-block:: php

    /**
     * Handles GET requests.
     *
     * This method retrieves data from the system.
     * It is used when clients need to fetch existing records.
     * For example, it can query LDAP to return a list of tasks or configurations.
     *
     * @return array The response data containing the requested information.
     */
    public function processEndPointGet(): array
    {
        // Implement logic to fetch and return data
    }

**Explanation:**
- This method is responsible for fetching data when an API request is made with ``GET``.
- It can retrieve information from LDAP or other sources via the ``TaskGateway``.
- The returned data should be formatted as an **array**.

----------------------------------
3. Handling POST Requests
----------------------------------

The **POST method** is used to create new records in the system.

.. code-block:: php

    /**
     * Handles POST requests.
     *
     * This method is responsible for creating new records in the system.
     * It is typically used when an administrator or an external service
     * submits new data to be stored (e.g., adding a new task to LDAP).
     *
     * @param array|null $data Input data to be processed and stored.
     * @return array The response indicating success or failure.
     */
    public function processEndPointPost(array $data = NULL): array
    {
        return [];
    }

**Explanation:**
- This method processes **new data submissions** (e.g., creating a new task).
- The input data is passed as an array, and it should be processed and stored accordingly.
- The return value should be an array indicating whether the operation was **successful or failed**.

----------------------------------
4. Handling DELETE Requests
----------------------------------

The **DELETE method** is used to remove existing records.

.. code-block:: php

    /**
     * Handles DELETE requests.
     *
     * This method removes existing records from the system.
     * It is used when an administrator or system process
     * wants to delete a task or configuration from the directory.
     *
     * @param array|null $data Information about what should be deleted.
     * @return array The response confirming the deletion.
     */
    public function processEndPointDelete(array $data = NULL): array
    {
        return [];
    }

**Explanation:**
- This method allows deleting records, such as removing a scheduled task.
- The ``$data`` array should contain information about what needs to be deleted.
- The method should return an array confirming the **successful deletion**.

----------------------------------
5. Handling PATCH Requests
----------------------------------

The **PATCH method** is used to update specific fields of an existing record.

.. code-block:: php

    /**
     * Handles PATCH requests.
     *
     * This method updates existing records with new values.
     * It is commonly used for modifying specific fields without replacing
     * the entire data structure.
     * For example, updating a task’s status or adjusting scheduling details.
     *
     * @param array|null $data Input data containing the fields to be updated.
     * @return array The updated response data.
     * @throws Exception If an error occurs during processing.
     */
    public function processEndPointPatch(array $data = NULL): array
    {
        // Implement update logic here
    }

**Explanation:**
- This method is used when modifying specific attributes of an existing record.
- Unlike ``POST``, which creates new data, ``PATCH`` **updates existing values**.
- The method should ensure only relevant fields are updated without affecting unrelated data.

-------------------------------
6. Understanding the Components
-------------------------------

The plugin interacts with the system using the ``TaskGateway`` class, which provides a bridge to external services like LDAP.

- **TaskGateway Integration**:
  - The ``TaskGateway`` object allows retrieving and modifying data.
  - It serves as an abstraction layer to interact with FusionDirectory’s tasks.

- **HTTP Method Mappings**:
  - ``processEndPointGet()`` → Handles GET requests to fetch existing records.
  - ``processEndPointPost()`` → Handles POST requests to create new entries.
  - ``processEndPointDelete()`` → Handles DELETE requests to remove entries.
  - ``processEndPointPatch()`` → Handles PATCH requests to update existing records.

-------------------------------
7. Summary
-------------------------------

To create a new orchestrator plugin:

1. **Define a class** that implements ``EndpointInterface``.
2. **Inject the TaskGateway** in the constructor to enable interaction with external data sources.
3. **Implement all required methods** to properly handle API requests.
4. **Use appropriate logic** within each method to interact with FusionDirectory (e.g., querying LDAP, managing tasks).

By following this structure, you can integrate new functionality into FusionDirectory’s Orchestrator efficiently.
