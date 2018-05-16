---
title: Azure SQL database deployment
description: Deploy to an Azure SQL database from VSTS or TFS
ms.assetid: B4255EC0-1A25-48FB-B57D-EC7FDB7124D9
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
ms.manager: douge
ms.author: ahomer
author: alexhomer1
ms.date: 05/10/2018
monikerRange: '>= tfs-2017'
---

# Azure SQL database deployment

::: moniker range="vsts"

VSTS can automatically deploy your database updates to Azure SQL database after every successful build. Make sure that you have completed one of the following two quickstarts before trying the steps in this article.

* [Your first build and release](../build/hello-world.md), if you plan to use web UI to create you pipeline
* [Build a repo with YAML](../build/with-yaml.md), if you plan to use YAML to create your pipeline

::: moniker-end

::: moniker range="< vsts"

TFS can automatically deploy your database updates to Azure SQL database after every successful build. Make sure that you have completed the [Your first build and release](../build/hello-world.md) quickstart before trying the steps in this article.

::: moniker-end

## DACPAC

The simplest way to deploy a database is to create [data-tier package or DACPAC](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications). DACPACs can be used to package and deploy both schema changes as well as data. You can create a DACPAC using the **SQL database project** in Visual Studio.

# [Web](#tab/web)

When setting up a build pipeline for your Visual Studio database project, use the **.NET desktop** template. This templates automatically adds the tasks to build the project and publish artifacts including the DACPAC.

When setting up a release pipeline, choose **Start with an Empty process**, link the artifacts from build, and then add [Azure SQL Database Deployment](../tasks/deploy/azure-sql-database-deployment.md) task.

# [YAML](#tab/yaml)

::: moniker range="< vsts"

YAML is not supported in TFS.

::: moniker-end

::: moniker range="vsts"

To deploy a DACPAC to an Azure SQL database, add the following snippet to your .vsts-ci.yml file.

```yaml
- task: SqlAzureDacpacDeployment@1
  displayName: Execute Azure SQL : DacpacTask
  inputs:
    azureSubscription: '<Azure service endpoint>'
    ServerName: '<Database server name>'
    DatabaseName: '<Database name>'
    SqlUsername: '<SQL user name>'
    SqlPassword: '<SQL user password>'
    DacpacFile: '<Location of Dacpac file in $(Build.SourcesDirectory) after compilation>'
```

::: moniker-end
---

## SQL scripts

Instead of using a DACPAC, you can also use SQL scripts to deploy your database. Here is a simple example of a SQL script that creates an empty database.

```sql
  USE [master]
  GO
  IF NOT EXISTS (SELECT name FROM master.sys.databases WHERE name = N'DatabaseExample')
  CREATE DATABASE [DatabaseExample]
  GO
```

In order to run SQL scripts as part of VSTS pipeline, you will need Azure Powershell scripts to create and remove firewall rules in Azure. Without the firewall rules, the VSTS agent cannot communicate with Azure SQL Database.

The following Powershell script creates firewall rules. You can check-in this script as `SetAzureFirewallRule.ps1` into your repository.

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] $AzureFirewallName = "AzureWebAppFirewall"
)

$ErrorActionPreference = 'Stop'

function New-AzureSQLServerFirewallRule {
  $agentIP = (New-Object net.webclient).downloadstring("http://checkip.dyndns.com") -replace "[^\d\.]"
  New-AzureSqlDatabaseServerFirewallRule -StartIPAddress $agentIp -EndIPAddress $agentIp -RuleName $AzureFirewallName -ServerName $ServerName
}
function Update-AzureSQLServerFirewallRule{
  $agentIP= (New-Object net.webclient).downloadstring("http://checkip.dyndns.com") -replace "[^\d\.]"
  Set-AzureSqlDatabaseServerFirewallRule -StartIPAddress $agentIp -EndIPAddress $agentIp -RuleName $AzureFirewallName -ServerName $ServerName
}

If ((Get-AzureSqlDatabaseServerFirewallRule -ServerName $ServerName -RuleName $AzureFirewallName -ErrorAction SilentlyContinue) -eq $null)
{
  New-AzureSQLServerFirewallRule
}
else
{
  Update-AzureSQLServerFirewallRule
}
```

The following Powershell script removes firewall rules. You can check-in this script as `RemoveAzureFirewall.ps1` into your repository.

```powershell
[CmdletBinding(DefaultParameterSetName = 'None')]
param
(
  [String] [Parameter(Mandatory = $true)] $ServerName,
  [String] $AzureFirewallName = "AzureWebAppFirewall"
)

$ErrorActionPreference = 'Stop'

If ((Get-AzureSqlDatabaseServerFirewallRule -ServerName $ServerName -RuleName $AzureFirewallName -ErrorAction SilentlyContinue))
{
  Remove-AzureSqlDatabaseServerFirewallRule -RuleName $AzureFirewallName -ServerName $ServerName
}
```

# [Web](#tab/web)

When you set up a build pipeline, make sure that the SQL script to deploy the database and the Azure powershell scripts to configure firewall rules are part of the build artifact.

When you set up a release pipeline, choose **Start with an Empty process**, link the artifacts from build, and then use the following tasks:

- First, use a [Azure Powershell](../tasks/deploy/azure-powershell.md) task to add a firewall rule in Azure to allow VSTS agent to connect to Azure SQL Database. The script requires one argument - the name of the SQL server you created.
- Second, use a [Command line](../tasks/utility/command-line.md) task to run the SQL script using **SQLCMD** tool. The argument to this tool is `-S {database-server-name}.database.windows.net -U {username}@{database-server-name} -P {password} -d {database-name} -i {SQL file}`. For example, when the SQL script is coming from an artifact source, **{SQL file}** will be of the form: `$(System.DefaultWorkingDirectory)/contoso-repo/DatabaseExample.sql`.
- Third, use another [Azure Powershell](../tasks/deploy/azure-powershell.md) task to remove the firewall rule in Azure.

# [YAML](#tab/yaml)

::: moniker range="< vsts"

YAML is not supported in TFS.

::: moniker-end

::: moniker range="vsts"

Add the following to your .vsts-ci.yml file to run a SQL script.

```yaml
variables:
  AzureSubscription: '<Azure service endpoint>'
  ServerName: '<Database server name>'
  DatabaseName: '<Database name>'
  AdminUser: '<SQL user name>'
  AdminPassword: '<SQL user password>'
  SQLFile: '<Location of SQL file in $(Build.SourcesDirectory)>'

steps:
- task: AzurePowerShell@2
  displayName: Azure PowerShell script: FilePath
  inputs:
    azureSubscription: '$(AzureSubscription)'
    ScriptPath: '$(Build.SourcesDirectory)\scripts\SetAzureFirewallRule.ps1'
    ScriptArguments: '$(ServerName)'
    azurePowerShellVersion: LatestVersion

- task: CmdLine@1
  displayName: Run Sqlcmd
  inputs:
    filename: Sqlcmd
    arguments: '-S $(ServerName) -U $(AdminUser) -P $(AdminPassword) -d $(DatabaseName) -i $(SQLFile)'

- task: AzurePowerShell@2
  displayName: Azure PowerShell script: FilePath
  inputs:
    azureSubscription: '$(AzureSubscription)'
    ScriptPath: '$(Build.SourcesDirectory)\scripts\RemoveAzureFirewallRule.ps1'
    ScriptArguments: '$(ServerName)'
    azurePowerShellVersion: LatestVersion
```
::: moniker-end
---

## Azure service endpoint

The **Azure SQL Database Deployment** task is the primary mechanism to deploy a database to Azure. This task, similar to other built-in Azure tasks, requires an Azure service endpoint as an input. The Azure service endpoint stores the credentials to connect from VSTS to Azure. For more information about creating an Azure service endpoint in VSTS, see the topic _Create an Azure service endpoint_.

## Deploying conditionally

# [Web](#tab/web)

You may choose to deploy only certain builds to the Azure SQL database. Release pipelines support various checks and conditions to control the deployment.

* Set _Branch filters_ when configuring the continuous deployment trigger on the artifact of the release pipeline.
* Set _Pre-deployment approvals_ as a pre-condition for deployment to an environment.
* Configure _Gates_ as a pre-condition for deployment to an environment.
* Set [conditions](../concepts/process/conditions.md) on the task.

# [YAML](#tab/yaml)

::: moniker range="< vsts"

YAML is not supported in TFS.

::: moniker-end

::: moniker range="vsts"

You may choose to deploy only certain builds to the Azure database. To do this, you can use one of these techniques:

* Isolate the deployment steps into a separate phase, and add a [condition](../concepts/process/conditions.md) to that phase.
* Add a condition to the step.

 The following example shows how to use step conditions to deploy only those builds that originate from master branch.

```yaml
- task: SqlAzureDacpacDeployment@1
  condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/master'))
  inputs:
    azureSubscription: '<Azure service endpoint>'
    ServerName: '<Database server name>'
    DatabaseName: '<Database name>'
    SqlUsername: '<SQL user name>'
    SqlPassword: '<SQL user password>'
    DacpacFile: '<Location of Dacpac file in $(Build.SourcesDirectory) after compilation>'
```
::: moniker-end
---