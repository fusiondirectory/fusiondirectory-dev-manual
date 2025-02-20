===============================
Creating an Orchestrator Plugin
===============================

This guide explains how to create an Orchestrator Plugin by implementing the **Strategy & Factory Design Pattern** using a mandatory interface implementation.

------------------
0. Plugin Location
------------------

A folder named ``fusiondirectory-orchestrator/plugins`` has been created to store your classes.

At the time of writing, the orchestrator is primarily used for **task processing**.

Therefore, it makes sense to place your classes within the ``tasks`` directory inside ``plugins``, though this is not mandatory.

.. note::
   Your plugin will be **automatically autoloaded**.
   It will be used as an argument for the endpoint tasks: ``<orchestrator_url>/api/tasks/your_plugin_name``

-------------------------------
1. Implementing the Interface
-------------------------------

An Orchestrator Plugin **must implement** the ``EndpointInterface`` to define the required methods for handling API requests. Each method corresponds to an HTTP operation (**GET, POST, DELETE, PATCH**), ensuring structured API interactions.

To create a new plugin, define a class that implements this interface and includes the necessary methods:

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

The constructor takes a ``TaskGateway`` object, which acts as an interface for interacting with external services such as **LDAP**. This gateway will be used within the methods to fetch, update, and delete data.

----------------------------------
2. Handling GET Requests
----------------------------------

The **GET method** retrieves existing data, often from **LDAP**.

If additional processing is required, you are free to extend the logic by calling new methods within your tasks.

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

----------------------------------
3. Handling POST Requests
----------------------------------

The **POST method** is used to create new records.

.. code-block:: php

    /**
     * Handles POST requests.
     *
     * This method is responsible for creating new records based on your data logic.
     * You might have developed a plugin with its own LDAP schema.
     *
     * @param array|null $data Input data to be processed and stored.
     * @return array The response indicating success or failure.
     */
    public function processEndPointPost(array $data = NULL): array
    {
        return [];
    }

----------------------------------
4. Handling DELETE Requests
----------------------------------

The **DELETE method** removes existing records.

.. code-block:: php

    /**
     * Handles DELETE requests.
     *
     * This method removes existing records based on your data handling logic.
     *
     * @param array|null $data Information about what should be deleted.
     * @return array The response confirming the deletion.
     */
    public function processEndPointDelete(array $data = NULL): array
    {
        return [];
    }

----------------------------------
5. Handling PATCH Requests
----------------------------------

The **PATCH method** updates specific fields of an existing record.

It can also be used to **trigger execution** of specific elements without necessarily updating data.

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

.. note::
   The **PATCH method** is **strongly recommended** in the official FusionDirectory Orchestrator client to execute task flows.

-------------------------------
6. Understanding the Components
-------------------------------

Your plugin interacts with key components such as ``TaskGateway``, which provides a bridge to **external services like LDAP**.

**Key Elements**

- **TaskGateway Integration**:

  - Allows retrieving and modifying data.
  - Acts as an abstraction layer for FusionDirectory’s tasks.

- **HTTP Method Mappings**:

  - ``processEndPointGet()`` → Handles **GET** requests for fetching records.
  - ``processEndPointPost()`` → Handles **POST** requests for creating entries.
  - ``processEndPointDelete()`` → Handles **DELETE** requests for removing entries.
  - ``processEndPointPatch()`` → Handles **PATCH** requests for updating records.

-------------------------------
7. Summary
-------------------------------

To create a new Orchestrator Plugin:

1. **Define a class** that implements ``EndpointInterface``.
2. **Inject the TaskGateway** in the constructor for interaction with external data sources.
3. **Implement all required methods** to handle API requests properly.
4. **Use appropriate logic** within each method to interact with FusionDirectory (e.g., querying LDAP, managing tasks).

By following this structure, you can efficiently integrate new functionality into FusionDirectory’s Orchestrator.