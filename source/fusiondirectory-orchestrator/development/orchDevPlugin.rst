===================
Orchestrator plugin
===================

This guide will help you get started with development within our GitLab environment.
It covers account creation, issue creation, project forking, and submitting a Merge Request (MR).

----------------------------
1. Orchestrator contribution
----------------------------

Please follow how to create an account, fork a project, create an MR and creating issues from FusionDirectory development section.
Exact same methodology will apply for your orchestrator plugin if you want it to be contributed within the main project.

With that said, let's see how to create a plugin, a new orchestrator endpoints.


------------------
2. Class structure
------------------

**Your class must implements the interface "EndPointInterface"**

In order to interact with many defined methods, including LDAP interaction, we received a "gateway" object.

class anOrchestratorPluginClass implements EndpointInterface
{

  private TaskGateway $gateway;

  public function __construct (TaskGateway $gateway)
  {
    $this->gateway = $gateway;
  }

  /**
   * @return array
   * Part of the interface of orchestrator plugin to treat GET method
   */
  public function processEndPointGet (): array
  {
  }

  /**
   * @param array|null $data
   * @return array
   */
  public function processEndPointPost (array $data = NULL): array
  {
    return [];
  }

  /**
   * @param array|NULL $data
   * @return array
   */
  public function processEndPointDelete (array $data = NULL): array
  {
    return [];
  }

  /**
   * @param array|NULL $data
   * @return array
   * @throws Exception
   */
  public function processEndPointPatch (array $data = NULL): array
  {
  }

}