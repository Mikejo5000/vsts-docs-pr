1. Navigate to the **Builds** tab of the **Build and Release** hub in VSTS, and then click **+ New**. You are asked to **Select a template** for the new build definition.

1. In the right panel, select **YAML** and click **Apply**.

1. For the **Default agent queue**, select _Hosted VS2017_. This is how you can use our pool of agents that have the software you need to build your app.

1. For the **Yaml path**, enter **.vsts-ci.yml**.

1. Click **Get sources**. Select your version control repository. You'll need to authorize access to your repo.

1. Click **Save and queue** to kick off your first build. On the **Queue build** dialog box, click **Queue**.

1. A new build is started. You'll see a link to the new build on the top of the page. Click the link to watch the new build as it happens.
