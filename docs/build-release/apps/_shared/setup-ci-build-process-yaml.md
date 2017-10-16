1. Navigate to the **Builds** tab of the **Build and Release** hub in VSTS or TFS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. In the right panel, select **YAML** and click **Apply**.

1. For the **Default agent queue**, select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, enter **.vsts-ci.yml**.

1. Click **Get sources**. Select your version control repository. You'll need to authorize access to your repo.
