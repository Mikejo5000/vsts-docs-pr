---
title: Deploy to Azure SQL Database
description: Deploy to an Azure SQL Database from VSTS
ms.assetid: BB1FC018-77A7-42E7-A270-4BC7CB3AD1C4
ms.prod: devops
ms.technology: devops-cicd
ms.topic: conceptual
ms.manager: douge
ms.author: ahomer
author: alexhomer1
ms.date: 04/09/2018
monikerRange: '>= tfs-2017'
---

# Azure SQL Database

VSTS can automatically deploy your database updates to Azure SQL Database whenever a new build is produced. If you are new to creating a VSTS pipeline, see the following topics first to understand how to create one.

* Build a repo with YAML file
* Build a repo without YAML
* [Deploy a VSTS build](../release/getting-started-vsts-build.md)

## Azure SQL Database

You need an Azure SQL Database server prior to setting up the VSTS pipeline. The steps below can help you create one:

1. Sign into the Azure management portal and choose
   the **+New** icon in the left panel, then choose
   **Data + Storage**. Select **SQL Database** from the
   list.

1. In the **SQL Database** blade, enter a name for
   Azure SQL Database and then
   choose **Server** to configure the required settings
   for the server.

1. In the **Server** blade, choose **Create a new server**.

1. In the **New server** blade, enter a name for the
   server and enter the admin
   login and password for the new server.
   Leave all other settings as they are and choose **OK**.  

1. Back in the **SQL Database** blade, leave all the
   other settings at their default values and choose
   **Create**.

1. After the Azure SQL Database server and database
   have been created, open its blade and make a note
   of the **Server name**.

## DACPAC

Data-tier application packages or DACPACs are a convenient way to package and deploy schema objects and data. The easiest way for a developer to create a DACPAC is to use a **SQL database project** in Visual Studio.

# [Web](#tab/web)

When you set up a build pipeline for your Visual Studio project, use the **.NET desktop** template. This templates automatically adds the tasks to build the project and publish artifacts including the DACPAC.

When you set up a release pipeline, choose **Start with an Empty process**, link the artifacts from build, and then add [SQL Database](../tasks/deploy/azure-sql-database-deployment.md) task.

# [YAML](#tab/yaml)

::: moniker range="vsts"

Here is an example of building a deploying a Visual Studio database project.

```yaml
queue:
  name: Hosted VS2017

variables:
  Solution: '<vs solution name>'
  BuildPlatform: 'any cpu'
  BuildConfiguration: 'release'
  AzureSubscription: '<Name of Azure service endpoint>'
  ServerName: '<Database server name>'
  DatabaseName: '<Database name>'
  AdminUser: '<SQL user name>'
  AdminPassword: '<SQL user password>'
  DacpacFile: '<Location of Dacpac file in $(Build.SourcesDirectory) after compilation>'

steps:
- task: NuGetToolInstaller@0
  displayName: Use NuGet 4.4.1
  inputs:
    versionSpec: 4.4.1

- task: NuGetCommand@2
  displayName: NuGet restore
  inputs:
    restoreSolution: '$(Parameters.solution)'

- task: VSBuild@1
  displayName: Build solution **\*.sln
  inputs:
    solution: '$(Parameters.solution)'
    platform: '$(BuildPlatform)'
    configuration: '$(BuildConfiguration)'

- task: SqlAzureDacpacDeployment@1
  displayName: Execute Azure SQL : DacpacTask
  inputs:
    azureSubscription: '$(AzureSubscription)'
    ServerName: '$(ServerName)'
    DatabaseName: '$(DatabaseName)'
    SqlUsername: '$(AdminUser)'
    SqlPassword: '$(AdminPassword)'
    DacpacFile: '$(DacpacFile)'
```

::: moniker-end

::: moniker range="< vsts"
YAML is not yet supported in TFS.
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

* Check the following PowerShell script into the same location that has your SQL script as `SetAzureFirewallRule.ps1`.

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

* Check the following PowerShell script into the same location that has your SQL script as `RemoveAzureFirewallRule.ps1`.

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

::: moniker range="vsts"

Here is an example of running a SQL script.

```yaml
queue:
  name: Hosted VS2017

variables:
  AzureSubscription: '<Name of Azure service endpoint>'
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

::: moniker range="< vsts"
YAML is not yet supported in TFS.
::: moniker-end

---