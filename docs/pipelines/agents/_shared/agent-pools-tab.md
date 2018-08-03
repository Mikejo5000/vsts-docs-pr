---
ms.topic: include
---

::: moniker range="vsts"
<!--TODO: when the new UI becomes the default, change this to https:&#x2F;&#x2F;{your_organization}.visualstudio.com/_settings/agentpools -->
In VSTS, the **Agent pools** hub can be found at <code>https:&#x2F;&#x2F;{your_organization}.visualstudio.com/_admin/_AgentPool</code>.
::: moniker-end

::: moniker range="< vsts"
In TFS, the **Agent pools** hub can be found at <code>{your_tfs_root}/_admin/_AgentPool</code>.
`{your_tfs_root}` may vary depending on the first version of TFS your administrator installed
as well as choices made at installation time. Defaults for TFS are:

| TFS version | Default root URL | Default URL to agent pool |
|-------------|------------------|---------------------------|
| TFS 2018 | <code>https:&#x2F;&#x2F;{your_server}/DefaultCollection</code> | <code>https:&#x2F;&#x2F;{your_server}/DefaultCollection/_admin/_AgentPool</code> |
| TFS 2017 | <code>https:&#x2F;&#x2F;{your_server}/tfs/DefaultCollection</code> | <code>https:&#x2F;&#x2F;{your_server}/DefaultCollection/_admin/_AgentPool</code> |
| TFS 2015 | <code>http:&#x2F;&#x2F;{your_server}:8080/tfs</code> | <code>https:&#x2F;&#x2F;{your_server}/DefaultCollection/_admin/_AgentPool</code> |

<p>[The TFS URL doesn't work for me. How can I get the correct URL?](../../../organizations/security/websitesettings.md)</p>
::: moniker-end